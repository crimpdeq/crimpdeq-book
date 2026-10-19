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
