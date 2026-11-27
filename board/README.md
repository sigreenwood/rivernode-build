# Main board, v3a.2

**The RiverNode board, refined.** v3a.2 keeps every track of v3a, the board already built
and running, and adds what building it taught us: a screw terminal for
the service-mode reed switch, a clear 12 V path with nothing to bridge by hand, a marked
spot for the optional power meter, and corrected labels on every socket.

![RiverNode v3a.2 board](RiverNode_v3a2_render.png)

## What's on the board

- **ESP32-S3 controller** with Wi-Fi, and Bluetooth for reading the Victron charge controller
- **4G modem socket** (Waveshare SIM7600G-H) for sites with no Wi-Fi
- **Real-time clock** (Adafruit DS3231, STEMMA QT version) that wakes the station on the
  hour, every hour, in step with the Environment Agency's gauges. Its Qwiic sockets start
  the sensor chain
- **Qwiic sensor chain**: the box sensor, the station's card and the power meter each plug
  in with a Qwiic cable, so there's nothing to solder and any of them swaps in seconds
- **Its own microSD card** (SparkFun Qwiic OpenLog): every reading is saved locally first,
  so nothing is lost when the signal drops
- **Two temperature probe inputs** with surge protection (gas discharge tube, resettable
  fuse and clamp diodes) on every cable that leaves the box
- **Box climate sensor** (Adafruit SHT45 with a PTFE filter) for temperature and humidity
  inside the enclosure
- **Switched power rails**: the modem and probes are switched off between readings,
  so a small solar panel keeps it going all year
- **Spare GPIO header** for adding sensors later

Every part is through-hole except one small chip (U3), the controller, modem and 5 V
converter plug into 2.54 mm sockets, and the sensors join by Qwiic cable, so it is a
comfortable build with a normal soldering iron.

| File | What it is |
|---|---|
| `gerbers/` | Fabrication files for the board maker, plus `FAB_NOTES.txt` |
| `RiverNode_v3a2_render.png` | Picture of the finished board |
| `RiverNode_v3a2_board.pdf` | Board layout, layer by layer |
| `RiverNode_v3a2_schematic.pdf` | Circuit diagram |
| `RiverNode_v3a2_BOM.csv` | Parts list by reference (prices and suppliers are at [rivernode.uk/bom/](https://rivernode.uk/bom/)) |

## Ordering the board

Zip the `gerbers/` folder and upload it to any board maker (JLCPCB, PCBWay and others).

| Setting | Value |
|---|---|
| Size | 182 × 136 mm |
| Layers | 2 |
| Thickness | 1.6 mm |
| Copper | **1 oz (35 µm)** |
| Finish | HASL is fine |
| Mask and legend colour | Any. Legend on **both** sides |

The 12 V feed to the 4G modem is sized for 1 oz copper, because the modem draws up to
2.2 A in bursts, so choose 1 oz if it isn't the maker's default. The maker's own design
check (DFM) report is free and worth a look before you pay.

## Building it

- Fit the modules after the rest of the board is soldered: the controller, modem and 5 V
  converter go into sockets.
- **Clock:** solder the Adafruit DS3231 STEMMA QT (5188) straight into MOD2 with its pin
  header, coin cell (CR1220) facing up. Its pins line up with MOD2's labels. Its two Qwiic
  sockets are on the underside at each end, edge-mounted, so the cables still plug in
  from the side.
- **Qwiic chain:** from the clock, chain the SHT45 box sensor, the Qwiic OpenLog (with a
  microSD card in it) and, if fitted, the power meter, in any order. **MOD1 and J4 stay
  empty**: they are for the older plug-in climate sensor and SPI card module, which the
  firmware still supports.
- **Service-mode reed switch:** two wires to J20 (REED and GND). Hold a magnet against
  the box and the station opens its own Wi-Fi set-up page on your phone.
- **Power meter (optional):** an Adafruit INA228 measures what the whole station draws.
  It sits on foam tape in the marked area, wired into the 12 V feed as printed there
  (VIN+ from the fuse, VIN− to J1 +, VBUS to VIN−), and joins the Qwiic chain.
- **Long probe cables:** if they give 1-Wire errors, fit the jumper J11 for a stronger pull-up.

**Sodium-ion batteries.** The input surge protector D1 is rated to 15.3 V continuous.
A sodium-ion pack charging at 15.8 V sits a little above that, well below the 17.1 V
where it starts to conduct. If you prefer to keep it fully within rating, set the
charger's absorption voltage to 15.3 V.

## Firmware

The station firmware is not in this repository yet. Get in touch through
[rivernode.uk](https://rivernode.uk) and we'll help you get a board running.

Once it's running, firmware updates reach the station **over the air**, and a new version
rolls itself back automatically if it doesn't start cleanly. v3a.2 will stay supported
alongside RiverNode v5.
