# Crimpdeq

<p style="text-align:center;"><img src="assets/logo.png" width="40%"></p>

Meet Crimpdeq, a portable digital force sensor for climbers, coaches, and therapists who want to measure and train finger strength, pulling power, and endurance. It is inspired by the [Tindeq Progressor](https://tindeq.com/product/progressor/) and is compatible with both the [Tindeq](https://tindeq.com/) and [Frez](https://www.frez.app/) apps.

## Specs

- Rechargeable battery with USB-C charging
- Communicates via Bluetooth Low Energy (BLE)
- Open-source firmware written in Rust
- Open-source PCB design
- Open-source 3D printable case design
- Automatic sleep when inactive
- Compatible with the Tindeq Progressor app ([Android](https://play.google.com/store/apps/details?id=com.progressor&hl=es_419) | [iOS](https://apps.apple.com/es/app/tindeq-progressor/id1380412428))
- Compatible with the Frez app (formerly ClimbHarder) ([Android](https://play.google.com/store/apps/details?id=com.holdtight.climbharder&pcampaignid=web_share) | [iOS](https://apps.apple.com/us/app/climbharder-no-hang-training/id6730120024))
- Sampling rate: 80 Hz
- Full-scale design load: 1500 N (~150 kg)
- Precision:
  - 0.05 kg between 0 and 99 kg
  - 0.1 kg between 100 and 150 kg
- Operating temperature: 0-40 ºC
- Dimensions: 80 x 90 x 35 mm
- Uses the [Tindeq Progressor API](https://tindeq.com/progressor_api/)
load cell
> ⚠️ **Warning**: Some values come from the load cell used in this project. If you use a different  cell, those values may change.

## Book Contents

This book is a practical guide to understanding Crimpdeq and building your own. It covers assembly, calibration, firmware internals, and the PCB and 3D-printable case design.

> ⚠️ **Note**: If you want to reproduce this project, feel free to reach out by email (sergio.gasquez@gmail.com), [X (formerly Twitter)](https://x.com/Sergio_Gasquez), or [Bluesky](https://bsky.app/profile/sergiogasquez.bsky.social).
