# PCB Design

## Revision 1
The PCB design is maintained in the [`crimpdeq-pcb` repository](https://github.com/crimpdeq/crimpdeq-pcb) and was created with KiCad.

It is a two-layer board derived from the [ESP32-C3-DevKit-RUST-1](https://github.com/esp-rs/esp-rust-board). This version removes unused sensors from the original design and keeps only what this project needs.

![PCB](../../assets/pcb_v1.png)

The PCB was sponsored by [PCBWay](https://www.pcbway.com/). Working with them was fast and easy, and the resulting boards are high quality.

[![PCBWay](../../assets/PCBWay.png)](https://www.pcbway.com/)

Revision 1 has been tested and works as expected, but there is still room for improvement. See the [Revision 2 issue](https://github.com/crimpdeq/crimpdeq-hardware/issues/2).

You can find the schematic, layout, and production files in the repository [GitHub Releases](https://github.com/crimpdeq/crimpdeq-pcb/releases).

## How to Manufacture
1. Download the production files from the [GitHub Releases](https://github.com/crimpdeq/crimpdeq-pcb/releases) page.
   - It is recommended to use the [latest release](https://github.com/crimpdeq/crimpdeq-pcb/releases/latest).
   - The release includes the files typically needed by PCB manufacturers:
     - `gerber.zip`: PCB fabrication files
     - `bom.csv`: bill of materials for assembly
     - `positions.csv`: component placement file for assembly

2. Submit the order and wait for the manufacturer review.
   - Some manufacturers may contact you with questions about substitutions, assembly notes, or file interpretation.

> ⚠️ **Note**: If the manufacturer comes back with questions or suggestions and you are unsure how to answer, feel free to contact me at sergio.gasquez@gmail.com.
