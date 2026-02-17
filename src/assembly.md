# Making Your Own Crimpdeq

This chapter explains how to build your own Crimpdeq prototype.

## 1. Required Materials
- [ESP32-C3-DevKit-RUST-1](https://github.com/esp-rs/esp-rust-board?tab=readme-ov-file#where-to-buy)
  - Other ESP32 boards can work, but you must provide your own battery charging solution.
- [Battery Holder](https://www.aliexpress.com/item/1005006283753220.html)
- [18650 Battery](https://www.aliexpress.com/item/1005007923191656.html)
  - Other batteries may also work if they can power the device.
- [Crane Scale](https://www.aliexpress.com/item/1005002719645426.html) or [Amazon alternative](https://www.amazon.es/dp/B08133JCM6)
  - Other crane scales may also work.
- HX711 module:
  - [Amazon](https://www.amazon.es/dp/B0DJX8BPQL)
  - [AliExpress](https://www.aliexpress.com/wholesale?SearchText=HX711+module)
- [Optional] Resistors:
  - 1× 33 kΩ resistor
  - 1× 10 kΩ resistor

## 2. Disassemble the Crane Scale
![Disassembly](assets/crane_disassembly.png)

1. Desolder the battery connections.
2. Desolder the four load cell wires (`E-`, `S-`, `S+`, and `E+`) from the PCB.
   ![Crane connections](assets/crane_connections.png)
3. Unscrew and remove the PCB and display.

## 3. Soldering

1. Modify the HX711 module:
   1. Set the sample rate to 80 Hz. Most HX711 modules ship with `RATE` tied to `GND`, which sets 10 Hz. To switch to 80 Hz:
      ![HX711 Pinout](assets/hx711_pinout.png)
      1. Cut the PCB trace to the `RATE` pin.
         - Carefully scratch the trace with a knife.
      2. Verify with a multimeter that `GND` and `RATE` are no longer connected.
         - Take care not to damage adjacent traces.
      3. Solder the `RATE` pin to the `DVDD` pin.
      4. Verify with a multimeter.
   2. [Optional] Improve measurements at 3.3 V. Most HX711 modules are configured for 5 V operation:
      1. Solder a 20 kΩ to 27 kΩ resistor in parallel with `R1` (highlighted in the image):
      ![Resistor to modify](assets/hx711_resistor.jpg)
      - For more information, see [this blog post](https://en.kohacraft.com/archives/modify-the-circuit-of-the-hx711-module-to-operate-at-3-3v-and-measure-the-weight-with-esp32.html).
      - This step is optional but improves measurement quality.
2. Connect the load cell to the HX711:
   - Solder the four wires from the crane scale to the HX711. Typical color mapping:

   | **HX711 Pin** | **Load Cell Pin** | **Description**                    |
   | ------------- | ----------------- | ---------------------------------- |
   | E+            | E+ (Red)          | Excitation positive (to load cell) |
   | E-            | E- (Black)        | Excitation negative (to load cell) |
   | S+            | S+ (Green)        | Signal positive (from load cell)   |
   | S-            | S- (White)        | Signal negative (from load cell)   |

   > ⚠️ **Note**: On some HX711 modules, `S+`/`S-` are labeled `A+`/`A-`.
3. Connect the HX711 to the ESP32-C3-DevKit-RUST-1:

| **HX711 Pin** | **ESP32-C3 Pin** | **Description**                |
| ------------- | ---------------- | ------------------------------ |
| VCC           | 3.3V             | Power supply (3.3V)            |
| GND           | GND              | Ground                         |
| DT (Data)     | GPIO4            | Data output from HX711         |
| SCK (Clock)   | GPIO5            | Clock signal for communication |

![ESP32-C3 Connections](assets/esp32c3_connections.png)

4. [Optional] Solder the voltage divider:
   1. Solder one end of the 33 kOhm resistor to `B+` on the ESP32-C3-DevKit-RUST-1.
   2. Join the other end of the 33 kOhm resistor with one end of the 10 kOhm resistor, then connect that junction to `GPIO1`.
   3. Solder the remaining end of the 10 kOhm resistor to `GND`.
   - The firmware expects the battery sense on `GPIO1` by default. Adjust the firmware configuration if you wire a different pin.
5. Verify all connections with a multimeter.

## 4. Adapt the Scale Case

1. Create space for the USB connector.
   - For example: mark the opening with a pen, then carefully heat a knife and melt the plastic.
2. Install the battery holder:
   1. Glue the battery holder with silicone. Leave the original battery lid opening free so you can route the two battery wires through it.
   2. Solder the positive wire (red) from the battery holder to a switch/button for power. Then solder the other switch/button pin to `B+` on the ESP32-C3-DevKit-RUST-1.
   3. Solder the negative wire (black) from the battery holder to `B-` on the ESP32-C3-DevKit-RUST-1.
3. Close the case:
   1. Ensure all components are securely installed before closing the case.

![Assembly](assets/crane_assembly.png)

## 5. Upload the Firmware

1. Connect the device with a USB-C cable.
2. Clone the `crimpdeq-firmware` repository:
      ```bash
      git clone https://github.com/crimpdeq/crimpdeq-firmware
      ```
      If you do not have Git installed, use the repository's "Code" button and download a ZIP.
3. Upload the firmware:
   1. Download a `.bin` file from the desired [GitHub release](https://github.com/crimpdeq/crimpdeq-firmware/releases).
   2. Flash the device using one of these tools:
     - Using [esp.huhn.me](https://esp.huhn.me/).
       1. Click "Connect" and select the serial port for your ESP board.
       2. Upload your `.bin` file.
       3. Click "Program".
         - See [this blog post](https://blog.spacehuhn.com/espwebtool) for more details.
     - Using [Adafruit ESPTool](https://adafruit.github.io/Adafruit_WebSerial_ESPTool/)
       1. Click Connect and select the serial port for your ESP board (often named `USB/JTAG serial debug unit...`).
       2. Upload your `.bin` file at offset `0x10000`.
       3. Click Program.

   ![Flashing with ESPTool](assets/esptool.png)

   > ⚠️ **Note**: If this method does not work, see the [Firmware chapter](firmware.md). You may need to install prerequisites and flash from the command line.
4. Check whether the default calibration values work for your scale:
   1. Connect the device with the Frez or Tindeq app.
   2. Use the "Live View" option.
   3. Measure a known weight and verify the value is correct.
      - If calibration is off, see the [Calibration chapter](calibration.md).
