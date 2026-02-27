# Flash with Local Setup

This chapter covers how to compile and flash the Crimpdeq firmware to your device.

## Prerequisites

To build and upload the firmware, install:
- [Rust](https://rustup.rs/)
- The `stable` toolchain with the ESP32-C3 target:
  ```bash
  rustup toolchain install stable --component rust-src --target riscv32imc-unknown-none-elf
  ```
- [`probe-rs`](https://probe.rs/), see [installation instructions](https://probe.rs/docs/getting-started/installation/)
    > ⚠️ **Note**: Dependeing on the OS you may need aditional steps:
    > - Linux: set up udev rules for your debug probe or USB-Serial device (see [`probe-rs` udev guide](https://probe.rs/docs/getting-started/installation/#udev-rules)).
    > - Windows/macOS: ensure the correct USB drivers are installed and select the appropriate serial port in your tooling.

## How to Build the Firmware

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

> ⚠️ **Note**: Erasing is only needed once. Avoid erasing routinely, or you will lose your [calibration values](./calibration.md).

### Build and Flash Your Device
With a [custom runner](https://doc.rust-lang.org/cargo/reference/config.html#targettriplerunner) configured in `.cargo/config.toml`, you can build, flash, and open a serial monitor with:
```bash
cargo run --release
```
This opens a serial monitor, allowing you to view log messages in real time.

To modify the [log level](https://defmt.ferrous-systems.com/filtering), update the `DEFMT_LOG` value in `.cargo/config.toml` or set it when running the command:
```bash
DEFMT_LOG=debug cargo run --release
```

> ⚠️ **Note**: If your DevKit does not include USB-Serial-JTAG, flash over UART by updating the custom runner in `.cargo/config.toml` to use [`espflash`](https://github.com/esp-rs/espflash/tree/main/espflash#cargo-runner) instead of `probe-rs`.

### Configuring Environment Variables

If you need to change `DEVICE_ID`, `DEVICE_NAME`, or `DEVICE_VERSION_NUMBER`, update their values in [`.cargo/config.toml`](https://github.com/crimpdeq/crimpdeq-firmware/blob/main/.cargo/config.toml).

After making changes, rebuild and flash the device for the new values to take effect.

#
