# Calibrate with Crimpdeq App

## Prerequisites
- Crimpdeq app on your platform:
  - Web version (no installation): [Crimpdeq web app](https://crimpdeq.github.io/crimpdeq-app/)
    - Not all browsers support WebBluetooth. Check [browser compatibility](https://developer.mozilla.org/en-US/docs/Web/API/Web_Bluetooth_API#browser_compatibility).
  - Native builds from the latest release: [crimpdeq-app/releases/latest](https://github.com/crimpdeq/crimpdeq-app/releases/latest)
    - Android: `crimpdeq-app-v<x.y.z>.apk`
    - macOS: `crimpdeq-app-v<x.y.z>-macos.zip`
    - Windows: `crimpdeq-app-v<x.y.z>-windows.zip`
    - Linux: `crimpdeq-app-v<x.y.z>-linux.zip`
- A stable mounting point so the device hangs freely and remains still
- At least one known weight (ideally near your typical maximum load)

## Calibration Steps

1. Connect to your Crimpdeq
   1. Launch the Crimpdeq app and grant permission to access device location (required for Bluetooth).
   2. Tap **Scan** to pair with your device.
   3. Once connected, the app shows device info (firmware version, battery, and current calibration).
2. Add calibration points
   1. Open the **Calibration** tab.
   2. For each point:
     - Hang the corresponding load on the device (or leave it empty for zero).
     - Enter the weight value in the app and tap **Add Calibration Point**.
   - **Recommended:** Add at least 2 points—**zero** (nothing hanging) and **full scale** (the maximum weight you expect to measure). The device supports up to 20 calibration points for finer accuracy.
3. Check the result
   1. After adding at least 2 points, the app displays the current calibration curve. Confirm it matches your expectations.

   ![Calibration Result](../assets/Screenshot_0.jpg)

Adding more calibration points (up to 20) improves measurement accuracy across the full load range.
