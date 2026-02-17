# PCB

## Revision 1

The PCB design is maintained in the [`crimpdeq-hardware` repository](https://github.com/crimpdeq/crimpdeq-hardware) and was created with KiCad. It is a two-layer board derived from the [ESP32-C3-DevKit-RUST-1](https://github.com/esp-rs/esp-rust-board). This variant removes unused sensors from the original design and adds only the components required for this project.

![PCB](assets/pcb_v1.png)

The PCB was sponsored by [PCBWay](https://www.pcbway.com/), thank you! Working with them was incredibly easy and fast, and the resulting boards are high quality.

[![PCBWay](assets/PCBWay.png)](https://www.pcbway.com/)

This PCB version is tested and working as expected, although there is definetly room for improvement, see [Revision 2](https://github.com/crimpdeq/crimpdeq-hardware/issues/2) issue.

## Revision 2

The [`crimpdeq-board` repository](https://github.com/crimpdeq/crimpdeq-board) contains an advanced version (Revision 2) of the PCB that includes additional sensors and other improvements.

> ⚠️ **Status**: This version is still a work in progress: routing is incomplete, and it has not been fabricated or tested. There is no estimated timeline for availability. Please, use [revision 1](https://github.com/crimpdeq/crimpdeq-hardware/tree/v1.0.0), unless you have hardwared knowledge and want to try this new untested version.
