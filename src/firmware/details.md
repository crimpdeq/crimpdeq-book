# Firmware details

# Code Structure

### `hx711`
This module implements the load cell functionality. It's an `async` version of the [loadcell](https://crates.io/crates/loadcell) crate with additional modifications.

### `ble`
This module implements the Bluetooth Low Energy (BLE) functionality:
- Defines the GATT server and services
- Handles advertising and connections
- Defines the Progressor service with data point and control point characteristics

### `progressor`
The `progressor` module implements the [Tindeq API](https://tindeq.com/progressor_api/) used for BLE communication between the ESP32-C3 and a smartphone.

### Main Tasks
The `main.rs` file defines several asynchronous tasks that run concurrently:
- `measurement_task`:
  - Initializes the load cell.
  - Handles taring and reads measurements from the sensor.
- `ble_task`:
  - Long-running background task required alongside other BLE tasks.
- `gatt_events_task`:
  - Processes GATT events such as control-point writes.
- `data_processing_task`:
  - Handles sending notifications with data points.
- `battery_voltage_task`:
  - Periodically reads the battery voltage.
- `deep_sleep_task`:
  - Monitors inactivity; after a timeout, the device enters deep sleep.

Communication between tasks occurs via a [`Channel`](https://docs.embassy.dev/embassy-sync/git/default/channel/struct.Channel.html).
