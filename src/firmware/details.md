# Firmware Internals

This chapter describes the firmware for PCB V3. Firmware for PCB V1 and V2 uses an `hx711` module instead of `ads1220` and has no `storage` module.

## Code Structure

### `ads1220`
This module implements the ADS1220 load-cell ADC driver over SPI. It configures the ADC for ratiometric measurements, selects the sampling rate (20 to 1000 SPS), tares the load cell, and fits the calibration factor from the calibration points.

### `ble`
This module implements the Bluetooth Low Energy (BLE) functionality:
- Defines the GATT server and services
- Handles advertising and connections
- Defines the Progressor service with data point and control point characteristics

### `progressor`
The `progressor` module implements the [Tindeq API](https://tindeq.com/progressor_api/) used for BLE communication between the ESP32-C3 and a smartphone.

### `storage`
This module stores the calibration factor and the sampling rate in separate flash partitions, so they persist across reboots and writing one cannot erase the other.

### Main Tasks
The `main.rs` file defines several asynchronous tasks that run concurrently:
- `measurement_task`:
  - Initializes the ADS1220.
  - Handles taring, calibration, and sampling-rate changes, and reads measurements from the sensor.
  - Runs on a higher-priority executor so high sampling rates are not delayed by BLE.
- `ble_task`:
  - Long-running background task required alongside other BLE tasks.
- `gatt_events_task`:
  - Processes GATT events such as control-point writes.
- `data_processing_task`:
  - Sends notifications with batches of data points sized to the connection's packet size.
- `connection_state_task`:
  - Tracks the BLE connection until it closes.
- `battery_gauge_task`:
  - Periodically reads the battery voltage and charge from the MAX17048 fuel gauge.
  - Puts the device to sleep when the battery is too low.
- `status_led_task`:
  - Sets the RGB LED color from the connection and battery state.
- `storage_task`:
  - Writes changed settings to flash.
- `deep_sleep_task`:
  - Monitors inactivity; after a timeout, the device enters deep sleep.

Communication between tasks occurs via [`Channel`](https://docs.embassy.dev/embassy-sync/git/default/channel/struct.Channel.html)s and a shared device state.

## BLE Protocol

The device implements the [Tindeq Progressor API](https://tindeq.com/progressor_api/) on the Progressor service (`7e4e1701-1ea6-40c9-9dcc-13d34ffead57`). Apps write commands to the control point characteristic (`7e4e1703-…`): one opcode byte followed by its payload. The device answers with notifications on the data point characteristic (`7e4e1702-…`), each made of a response code byte, a payload length byte, and the payload. During a measurement, each `0x01` notification carries as many samples as fit in the connection's packet size, each a weight in kg (`f32`) followed by the microseconds since the measurement started (`u32`). Multi-byte values are little-endian.

It supports these standard commands: tare (`0x64`), start measurement (`0x65`), stop measurement (`0x66`), add calibration point (`0x69`, followed by the weight in kg as an `f32`), get app version (`0x6B`), shutdown (`0x6E`, which closes the connection), sample battery (`0x6F`), and get Progressor ID (`0x70`).

Crimpdeq adds these commands, which the Tindeq and Frez apps do not use:

| Opcode | Command                 | Payload               | Response                                                                                                 |
| ------ | ----------------------- | --------------------- | -------------------------------------------------------------------------------------------------------- |
| `0x72` | Get calibration         | none                  | `0x05` with the calibration factor (`f32`), then one `0x06` per point with its raw value and weight in kg (`f32`, `f32`) |
| `0x74` | Default calibration     | none                  | `0x05` with the default calibration factor; clears the calibration points                                 |
| `0x75` | Set sample rate         | samples per second (`u16`) | `0x07` with the rate in use (`u16`), which stays unchanged for unsupported rates                       |
| `0x76` | Get sample rate         | none                  | `0x07` with the rate in use (`u16`)                                                                      |
| `0x77` | Get battery status      | none                  | `0x08` with the state of charge in percent (`u8`) and a charging flag (`u8`)                             |
| `0x78` | Remove calibration point | point index (`u8`)   | If removed, the new calibration factor and points, then `0x09` with `1`; otherwise only `0x09` with `0`    |

The supported sample rates are 20, 45, 90, 175, 330, 600, and 1000 SPS. The sample rate commands and `0x77` and `0x78` need firmware `v3.x`.
