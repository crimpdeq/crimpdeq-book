# Flash with Local Setup

This chapter covers how to compile and flash the Crimpdeq firmware to your device.

## Prerequisites

To build and upload the firmware, install:
- [Rust](https://rustup.rs/)
  - The repository's `rust-toolchain.toml` installs the `stable` toolchain, `rust-src`, and the ESP32-C3 target on the first build.
- [`probe-rs`](https://probe.rs/), see [installation instructions](https://probe.rs/docs/getting-started/installation/)
  > ⚠️ **Note**: Depending on your OS, you may need extra setup steps:
  > - Linux: set up udev rules for your debug probe or USB-serial device (see the [`probe-rs` udev guide](https://probe.rs/docs/getting-started/installation/#udev-rules)).
  > - Windows/macOS: ensure the correct USB drivers are installed and select the appropriate serial port in your tooling.

## How to Build the Firmware

The `main` branch of the [firmware repository](https://github.com/crimpdeq/crimpdeq-firmware) targets PCB V3. For an older PCB, check out the [release tag for your revision](./index.md#choose-the-firmware-for-your-pcb) first, for example:

```bash
git checkout v2.1.0
```

To build the firmware, run:

```bash
cargo build --release
```

This compiles the firmware only. To build and flash the device, see [Build and Flash your Device](#build-and-flash-your-device).

## How to Flash Your Crimpdeq

### Erase Device Memory
If this board was previously used for other projects, erase its flash once:
```bash
probe-rs erase
```

> ⚠️ **Note**: Erasing is only needed once. Avoid erasing routinely, or you will lose your [calibration values](../calibration/index.md).

### Build and Flash Your Device
The [custom runner](https://doc.rust-lang.org/cargo/reference/config.html#targettriplerunner) configured in `.cargo/config.toml` builds, flashes, and starts the firmware with:
```bash
cargo run --release
```
Logging is off by default (`DEFMT_LOG = "off"` in `.cargo/config.toml`), so the command exits once the firmware starts.

To see log messages, set the [log level](https://defmt.ferrous-systems.com/filtering) in `.cargo/config.toml` or when running the command. The runner then keeps a log monitor open:
```bash
DEFMT_LOG=debug cargo run --release
```

> ⚠️ **Note**: On release tags up to `v3.0.0`, `cargo run --release` opens a serial monitor even with logging off.

> ⚠️ **Note**: If your DevKit does not include USB-Serial-JTAG, flash over UART by replacing the runner in `.cargo/config.toml` with [`espflash`](https://github.com/esp-rs/espflash/tree/main/espflash#cargo-runner) instead of `probe-rs`.

### Try the Firmware Without a Load Cell
On `main`, the `mock` feature simulates the load cell and battery, so you can test the firmware and apps on PCB V3 or on an [ESP32-C3 Rust board](https://github.com/esp-rs/esp-rust-board) without a load cell or battery:
```bash
cargo run --release --features mock
```
The simulated load cell repeats pulls up to 30 kg, the battery discharges to 20 % and charges back, and the device logs the idle timeout instead of going to sleep.

### Configuring Environment Variables

If you need to change `DEVICE_ID`, `DEVICE_NAME`, or `DEVICE_VERSION_NUMBER`, update their values in [`.cargo/config.toml`](https://github.com/crimpdeq/crimpdeq-firmware/blob/main/.cargo/config.toml).

After making changes, rebuild and flash the device for the new values to take effect.
