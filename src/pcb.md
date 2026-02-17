# PCB

## Revision 1

The PCB design is maintained in the [`crimpdeq-hardware` repository](https://github.com/crimpdeq/crimpdeq-hardware) and was created with KiCad.

It is a two-layer board derived from the [ESP32-C3-DevKit-RUST-1](https://github.com/esp-rs/esp-rust-board). This version removes unused sensors from the original design and keeps only what this project needs.

![PCB](assets/pcb_v1.png)

The PCB was sponsored by [PCBWay](https://www.pcbway.com/). Working with them was fast and easy, and the resulting boards are high quality.

[![PCBWay](assets/PCBWay.png)](https://www.pcbway.com/)

Revision 1 has been tested and works as expected, but there is still room for improvement. See the [Revision 2 issue](https://github.com/crimpdeq/crimpdeq-hardware/issues/2).

## Revision 2

The [`crimpdeq-board` repository](https://github.com/crimpdeq/crimpdeq-board) contains an advanced version (Revision 2) of the PCB that includes additional sensors and other improvements.

> ⚠️ **Status**: This version is still a work in progress. Routing is incomplete, and it has not been fabricated or tested yet. There is no estimated timeline for availability. Use [revision 1](https://github.com/crimpdeq/crimpdeq-hardware/tree/v1.0.0) unless you have hardware experience and want to try this untested version.
