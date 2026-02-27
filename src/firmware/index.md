# Firmware & Flashing

The Crimpdeq firmware is written in async Rust (`no_std`) using [`esp-hal`](https://github.com/esp-rs/esp-hal) and a small set of supporting crates.

This section explains how to flash the firmware to your device and, optionally, how the code is organized.

## Choose a Flashing Method

There are two supported ways to flash the firmware:

### 1. Web Tools

- No local setup required
- Fastest way to install the latest release
- Best if you do not plan to modify the firmware

See [Flashing with Web Tools](./web_tools.md)

### 2. Local Setup

- Requires installing Rust and `probe-rs`
- Lets you build from source and modify the code
- Better for development and debugging

See [Flashing with Local Setup](./local.md)

## Firmware Internals

If you want to understand or modify the firmware, see [Firmware Details](./details.md) chapter

If you only want a working device, you can flash the firmware and continue to [Calibration](../calibration/index.md).
