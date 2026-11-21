# Main board, v3a

**This is the board that has been made and run.** These are the files it was
manufactured from, unchanged. It works, but it has a few known issues that you fix by
hand while building it. They are listed below in [Known issues](#known-issues). A
revised board that fixes them is being drawn and will be published here once it is
ready.

| File | What it is |
|---|---|
| `gerbers/` | Fabrication files for the board maker, plus `FAB_NOTES.txt` |
| `RiverNode_v3a_render.png` | Picture of the finished board |
| `RiverNode_v3a_board.pdf` | Board layout, layer by layer |
| `RiverNode_v3a_schematic.pdf` | Circuit diagram |
| `RiverNode_v3a_BOM.csv` | Parts list by reference (prices and suppliers are at [rivernode.uk/bom/](https://rivernode.uk/bom/)) |
| `SOCKET_CHECK_SHEET.pdf` | Socket pin-order check. **Print at 100 %** |
| `FIT_CHECK_1to1.pdf` | Full-size layout to lay the real modules on. **Print at 100 %, scaling off** |
| `FIRST_POWER_UP.pdf` | Step-by-step first power-up |

## Ordering the board

Zip the `gerbers/` folder and upload it to any board maker (JLCPCB, PCBWay and others).

| Setting | Value |
|---|---|
| Size | 182 × 136 mm |
| Layers | 2 |
| Thickness | 1.6 mm |
| Copper | **1 oz (35 µm). Not optional** |
| Finish | HASL is fine |
| Mask and legend colour | Any. Legend on **both** sides |

The 12 V feed to the 4G modem is sized for 1 oz copper, because the modem draws up to
2.2 A in bursts. On 0.5 oz copper those tracks run hot, so pay for 1 oz if it isn't the
maker's default. Read the board maker's own design check (DFM) report before you pay.

## Known issues

**1. The power-monitor socket MOD3 is in the 12 V path. Do not plug a module into it.**
MOD3 was drawn for an INA226 module. Stations now use an Adafruit INA228 instead, and
its pins do not match the socket: plugged in, it puts its alert pin on 12 V and locks
up the sensor bus. But the socket cannot simply be left empty either, because the whole
board is fed through its pins 1 and 2.

What to do:
- Solder a **solid copper wire link (0.8–1.0 mm) across MOD3 pins 1 and 2**. It carries
  the whole board current, so not a jumper cap. Without it nothing gets power.
- Wire the **INA228 in the 12 V feed before the board**, after the external 3 A fuse:
  VIN+ towards the battery, VIN− towards the board's 12 V IN terminal, VBUS tied to VIN−.
- Fix the INA228 to the board **with double-sided foam tape** in the space beside MOD3,
  and connect it to the sensor bus with a **Qwiic / STEMMA QT cable**: 3.3 V, GND, SDA
  and SCL, the same signals as the BME280 socket MOD1. Its terminals are
  live 12 V, so keep them clear of the board's solder joints.

**2. There is no terminal for the service-mode reed switch.** Wire the reed switch
to the spare GPIO header **J15: pin 5 (GPIO 2) and pin 7 (GND)**. The firmware needs no
pull-up resistor.

**3. Some socket labels are wrong.** The pin names printed beside **MOD2, MOD3 and J4**
were typed by hand and three are wrong. Go by `SOCKET_CHECK_SHEET.pdf` and the
schematic, not the printing on the board. `FIRST_POWER_UP.pdf` also says the I²C
sensors are on the switched supply; they are on the always-on 3.3 V supply (see below).

**4. The website address on the board is out of date.** It reads rivernode.net; the
site is [rivernode.uk](https://rivernode.uk).

**5. U3 is small.** U3 (SOT-23-6) is the only surface-mount part and its pads are
tight for hand soldering. Check its joints under a magnifier; on one board it needed
reflowing.

## Building it

- Every part is through-hole except U3. All modules sit in 2.54 mm sockets, so any of
  them can be swapped.
- Follow `FIRST_POWER_UP.pdf` before fitting the modules. Fit the MOD3 wire link first.
- The I²C sensors (BME280, DS3231 and anything on the Qwiic cable) are all on the always-on
  3.3 V supply. Only the microSD card and the temperature probes are switched off
  between readings.

**Battery voltage.** The input surge protector D1 is rated to 15.3 V continuous. A
sodium-ion pack charging at 15.8 V is slightly above that but well below the 17.1 V
where it starts conducting, so expect a little more leakage during the final stage of
charging only. Setting the charger's absorption voltage to 15.3 V keeps it fully within
rating, at the cost of a slightly less full battery.

## Firmware

The station firmware is not in this repository yet.
