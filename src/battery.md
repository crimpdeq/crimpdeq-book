# Battery and Status LED

## Charging

To charge the device:

1. Plug the device into a power source using a USB-C cable.
2. Set the power switch for your PCB revision:
   - **PCB V1:** turn the device on.
   - **PCB V2 and V3:** leave the device either on or off; they support charging while switched off.
3. Check that the red charging LED turns on.
   - On V3, the red LED is visible through the smaller of the two holes in the lid.
4. When the red LED turns off, charging is complete. Unplug the USB-C cable.

![Device Charging](assets/battery_charge.png)

On V3, the USB-C port and power switch are on the front wall of the case:

<p style="text-align:center;"><img src="assets/crimpdeq_v3_side.jpg" alt="USB-C port and power switch on the V3 case" width="40%"></p>

## Status LED (PCB V2 and V3)

The RGB LED shows the device status:

| LED              | Status                                 |
| ---------------- | -------------------------------------- |
| Blue             | On and waiting for a Bluetooth connection |
| Green            | Connected to an app                    |
| Blinking red     | Battery low (3.5 V or less); charge it soon |
| Off              | Asleep or switched off                 |

With firmware `v2.1.0` or newer, when the battery drops to 3.3 V while not charging, the device turns itself off to protect the battery. The device also sleeps when idle: with firmware `v3.x`, after 4 minutes without a connection or 30 minutes connected without measuring or other commands; with older firmware, after 4 minutes of inactivity. Battery and sample-rate requests from a connected app do not keep it awake. To wake it, disconnect USB and turn the switch off and on again.

> ⚠️ **Note**: On V3, USB power keeps the device running while the cable is connected, even with the switch off.
