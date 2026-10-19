# Crimpdeq Assembly

This chapter shows how to assemble a Crimpdeq using the custom PCB and 3D-printed case.

Most assembly steps are the same for PCB V1, V2, and V3. The main differences are the external wiring pad layout, especially the battery/switch wiring, and how the PCB sits in the case.

<p style="text-align:center;"><img src="../../assets/Crimpdeqs_v3.jpg" alt="Assembled Crimpdeq V3" width="90%"></p>

## 1. Gather Parts and Tools

### Parts

- [Crimpdeq PCB](https://github.com/crimpdeq/crimpdeq-pcb/releases/latest)
  - See the [PCB manufacturing guide](./pcb.md#how-to-manufacture) if you need to order one.
- [Crimpdeq 3D-printed case](./case.md) that matches your PCB revision
- WH-C07 load cell, or a compatible load cell with similar dimensions
  - You can salvage one from a [crane scale](https://www.aliexpress.com/item/1005002719645426.html) ([Amazon alternative](https://www.amazon.es/dp/B08133JCM6)) or buy it separately.
- [3.7 V, 2000 mAh LiPo battery](https://www.aliexpress.us/item/3256809404408618.html?spm=a2g0o.order_list.order_list_main.5.1406194d6kJ2h0&gatewayAdapt=glo2usa4itemAdapt)
- [KCD11 two-terminal switch](https://www.aliexpress.us/item/2255800787248498.html?spm=a2g0o.order_list.order_list_main.11.1406194d6kJ2h0&gatewayAdapt=glo2usa4itemAdapt)
- Insulated hookup wire and heat-shrink tubing
- 4 × M2.5 screws (M2.5×10 for the V3 case)

### Tools

- Soldering iron and solder
- Wire cutters and strippers
- Multimeter

## 2. Identify Your PCB Layout

Before soldering, identify which PCB layout you have and follow the matching wiring table.

| PCB V1 | PCB V2 |
| --- | --- |
| <img src="../../assets/pcb_pinout.png" alt="Crimpdeq PCB V1 pad layout" style="display:block; width:240px; max-width:100%; margin:0 auto;"> | <img src="../../assets/pcb_v2_pinout.png" alt="Crimpdeq PCB V2 pad layout" style="display:block; width:240px; max-width:100%; margin:0 auto;"> |
| The load cell uses numbered pads `12`–`15`; the battery uses `16` and `17`. | The load-cell and power pads are labeled `E+`, `E-`, `A-`, `A+`, `VBAT`, and `SW+`. |

**PCB V3** has eight labeled pads: `E-`, `A-`, `A+`, and `E+` for the load cell along one edge, and `B-`, `B+`, `SW+`, and `SW-` for the battery and switch along the edge next to the USB-C connector. The labels are printed on both sides of the board.

![Crimpdeq PCB V3 pad layout](../../assets/pcb_v3_pinout.png)

The photos in this chapter show a V1 or V3 PCB, as noted in each caption. Use the tables below—not the wire positions in the photos—to connect a V2 PCB.

## 3. Solder the Connections

> ⚠️ **Battery safety**: Keep USB power disconnected while wiring. Prevent the battery leads from touching each other, and insulate every splice and switch terminal with heat-shrink tubing. Complete the unpowered checks below before connecting either battery lead.

### Load cell

| Function            | Typical wire color | PCB V1 pad | PCB V2 pad | PCB V3 pad |
| ------------------- | ------------------ | ---------- | ---------- | ---------- |
| Excitation positive | Red                | `E+ (15)`  | `E+`       | `E+`       |
| Excitation negative | Black              | `E- (14)`  | `E-`       | `E-`       |
| Signal positive     | Green or blue      | `S+ (12)`  | `A+`       | `A+`       |
| Signal negative     | White              | `S- (13)`  | `A-`       | `A-`       |

> ⚠️ **Note**: Wire colors are not guaranteed. Confirm the labels or documentation for your load cell before soldering.

Reference photo of the load cell wires after soldering them to a V1 PCB:

<p style="text-align:center;"><img src="../../assets/loadcell_pcb.jpg" alt="Load cell wires soldered to a V1 PCB" width="65%"></p>

Reference photo of a V3 PCB with the load cell wired to `E-`, `A-`, `A+`, and `E+`, and the battery wired to `B-` and `B+`:

<p style="text-align:center;"><img src="../../assets/crimpdeq_v3_assembly_1.jpg" alt="Load cell and battery wired to a V3 PCB" width="75%"></p>

### Battery and switch

Before soldering the switch terminals, feed both switch wires from inside the case through the switch opening and slide heat-shrink tubing onto them. Solder the switch outside the case; you will press it into the opening later. Do not attach the switch before feeding the wires through the opening.

Leave both battery leads disconnected until instructed to connect them below.

#### PCB V1

1. Solder a wire from `B+ (17)` to either switch terminal.
2. Leave the other switch terminal available for the battery positive wire.

The completed circuit will place the switch in series with the positive lead: `battery + → switch → B+ (17)`.

#### PCB V2

1. Solder a wire from `SW+` to either switch terminal.
2. Connect the other switch terminal to `VBAT` with a short jumper.
3. Plan the shared `E-` connection for the load-cell and battery negative wires.
   - If both wires do not fit cleanly in the pad, make a short insulated pigtail from `E-` with one branch for each wire.

The completed connections will be:

- `battery + → VBAT`
- `VBAT → switch → SW+`
- `battery − → E-`

> ⚠️ **Important V2 difference**: Unlike V1, V2 keeps `VBAT` connected to the battery while the switch is off. This allows the battery to charge while the device is off. Do not place the switch between the battery and `VBAT`.

#### PCB V3

1. Solder one switch wire to `SW+` and the other to `SW-`.
2. Feed both wires through the switch opening and solder each one to a switch terminal. The switch has no polarity.

The completed connections will be:

- `battery + → B+`
- `battery − → B-`
- `SW+ → switch → SW-`

Like V2, V3 keeps `B+` connected to the battery while the switch is off, so the battery charges while the device is off. The switch only turns the device on and off; do not place it between the battery and `B+`.

<p style="text-align:center;"><img src="../../assets/crimpdeq_v3_assembly_2.jpg" alt="Switch wires from SW+ and SW- fed through the switch opening of the V3 case" width="75%"></p>

### Check before connecting the battery

With both battery leads still disconnected, use a multimeter in continuity or resistance mode to check that:

- Battery positive is not shorted to ground (`B+` to `B-` on V1 and V3, or `VBAT` to `E-` on V2).
- Each load-cell wire reaches the correct pad for your PCB revision.
- The switch opens and closes its path.
  - On V1, check between the free switch terminal and `B+`.
  - On V2, check between `VBAT` and `SW+`.
  - On V3, check between `SW+` and `SW-`.

Resolve any unexpected short or open connection before proceeding.

### Connect the battery

- **PCB V1:** connect battery positive (red) to the free switch terminal, then connect battery negative (black) to `B- (16)`.
- **PCB V2:** connect battery negative (black) to the shared `E-` connection, then connect battery positive (red) to `VBAT`.
- **PCB V3:** connect battery negative (black) to `B-`, then connect battery positive (red) to `B+`.

## 4. Install Everything in the Case

### PCB V1 and V2

1. Place the load cell in its position in the 3D-printed case.
2. Route the load cell wires so they are not pinched by the PCB or the lid.
3. Place the battery in the battery compartment.

<p style="text-align:center;"><img src="../../assets/crimpdeq_assembly_1.png" alt="Load cell and battery placed on the case" width="75%"></p>

4. Position the PCB in the case.
5. Tuck the wires neatly around it so nothing sits under the board.
6. Insert the KCD11 switch into the switch opening.

<p style="text-align:center;"><img src="../../assets/crimpdeq_assembly_2.jpg" alt="PCB V1 positioned in the case" width="65%"></p>

<p style="text-align:center;"><img src="../../assets/crimpdeq_assembly_3.jpg" alt="Wires arranged around a PCB V1" width="65%"></p>

### PCB V3

In the V3 case, the front wall is the one with the USB-C and switch openings.

1. Place the load cell in the main body with the white strain-gauge cover facing up and its wires toward the front wall.
2. Route the load-cell wires under the battery position to the front of the case, where the load-cell pads will sit.
3. Place the battery on top of the load cell, with its leads at the rear. Run the leads up behind the battery and forward along its side to the `B-` and `B+` pads.
4. Press the KCD11 switch into the switch opening.
5. Hold the PCB with the ESP32-C3 module and LEDs facing up. Tilt it to insert the USB-C connector into the front-wall opening, then lower the board onto its two support columns in front of the battery.
6. Check that no wire sits on top of the support columns or the battery, where the lid clamps press.

<p style="text-align:center;"><img src="../../assets/crimpdeq_v3_assembly_3.jpg" alt="PCB V3 seated in the case above the battery" width="75%"></p>

<p style="text-align:center;"><img src="../../assets/crimpdeq_v3_assembly_4.jpg" alt="PCB V3 seated with its USB-C connector in the front wall" width="75%"></p>

## 5. Verify the Powered Wiring

With USB still disconnected, use the multimeter in DC voltage mode to confirm the polarity and switch behavior:

- **PCB V1:** place the black probe on `B-` and the red probe on `B+`. The meter should show battery voltage only while the switch is on.
- **PCB V2:** place the black probe on `E-`. With the red probe, confirm that `VBAT` always shows battery voltage and `SW+` shows battery voltage only while the switch is on.
- **PCB V3:** place the black probe on `B-`. With the red probe, confirm that `B+` always shows battery voltage and `SW-` shows battery voltage only while the switch is on.

Turn the switch off before closing the case.

## 6. Close the Case

1. Place the lid on the main enclosure.
   - On V3, align the lid's two LED holes over the RGB status LED and the red charging LED.
2. Fasten it with the 4 × M2.5 screws.

<p style="text-align:center;"><img src="../../assets/crimpdeq_v3_side.jpg" alt="V3 case front wall with the USB-C port and power switch" width="45%"></p>

## 7. Next Steps

1. Flash the firmware (see [Firmware](../../firmware/index.md)).
2. Calibrate the device (see [Calibration](../../calibration/index.md)).
