# Flash with Web Tools

This chapter covers how to flash your device with a pre-built binary.

1. Connect the device with a USB-C cable.
2. Download a `.bin` from the [GitHub release that matches your PCB revision](./index.md#choose-the-firmware-for-your-pcb):
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

## If the Flasher Cannot Connect

If the serial port does not appear, or the flasher cannot connect to it:

1. Make sure the device is awake. A sleeping device (status LED off) does not show its serial port. On PCB V3 and V4, turn the switch off and reconnect the USB-C cable: with the switch off, connecting USB restarts the device.
2. If it still does not connect, put the ESP32-C3 into download mode. PCB V4 has `EN`, `GND`, and `BOOT` pads for this on its bottom side, under the ESP32-C3 module (see the [pad layout](../assembly/crimpdeq/pcb.md#revision-4-current)), so take the board out of the case first. Either:
   - Hold `BOOT` to `GND` and briefly connect `EN` to `GND`. The pads are 1.5 mm apart, so tweezers can bridge neighboring pads.
   - With the switch off and USB disconnected, hold `BOOT` to `GND` while connecting the USB-C cable.
3. Flash the firmware as described above, then disconnect and reconnect USB with the switch off, or briefly connect `EN` to `GND`, to start it.
