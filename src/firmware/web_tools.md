# Flash with Web Tools

This chapter covers how to flash your device with a pre-built binary.

1. Connect the device with a USB-C cable.
2. Download a `.bin` from the [latest GitHub release](https://github.com/crimpdeq/crimpdeq-firmware/releases/latest):
   - If this is the first time you are flashing Crimpdeq firmware to your device, download `crimpdeq-merged.bin`.
   - If you are updating firmware on a device that is already flashed, download `crimpdeq.bin`.
3. Choose a web flasher. Use either:
   - [esp.huhn.me](https://esp.huhn.me/)
     - See [this blog post](https://blog.spacehuhn.com/espwebtool) for extra details.
   - [Adafruit ESPTool](https://adafruit.github.io/Adafruit_WebSerial_ESPTool/)
4. Click `Connect` and select the serial port for your ESP board.
   - In Adafruit ESPTool, the port often appears as `USB/JTAG serial debug unit...`.
5. Click `Erase` only if this is the first time you are flashing this device.

   > ⚠️ **Note**: Erasing the device also erases stored calibration values. Skip this if the device was already programmed and calibrated.

6. Upload your `.bin`:
   - If you are using `crimpdeq-merged.bin` -> address `0x0`
   - If you are using `crimpdeq.bin` -> address `0x10000`
7. Click `Program`.

![Flashing with ESPTool](../assets/esptool.png)
