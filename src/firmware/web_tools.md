# Flash with Web Tools

## Upload the Firmware
<!-- Remove this part from here, move the firmware chapter just after assembly as it common to both builds -->
1. Connect the device with a USB-C cable.
2. Download the `crimpdeq.bin`  from the [latest GitHub release](https://github.com/crimpdeq/crimpdeq-firmware/releases/latest)
3. Upload the firmware: You can flash your device using one of these two tools:
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
