# Main board, v3a.1

**Not yet manufactured.** v3a.1 is the v3a board with the faults found while building
and testing v3a fixed. It keeps v3a's 182 × 136 mm outline, its four M3 mounting holes
and its layout. KiCad's design-rule check passes with no errors, no unconnected pads and
no differences from the schematic. Nobody has built one yet, so read
[Before you pay](#before-you-pay) first.

| File | What it is |
|---|---|
| `gerbers/` | Fabrication files for the board maker, plus `FAB_NOTES.txt` |
| `RiverNode_v3a1_render.png` | Picture of the finished board |
| `RiverNode_v3a1_board.pdf` | Board layout, layer by layer |
| `RiverNode_v3a1_schematic.pdf` | Circuit diagram |
| `RiverNode_v3a1_BOM.csv` | Parts list by reference (prices and suppliers are at [rivernode.uk/bom/](https://rivernode.uk/bom/)) |
| `SOCKET_CHECK_SHEET.pdf` | Socket pin-order check. **Print at 100 %** |
| `FIT_CHECK_1to1.pdf` | Full-size layout to lay the real modules on. **Print at 100 %, scaling off** |
| `FIRST_POWER_UP.pdf` | Step-by-step first power-up using the test points |

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
| Minimum track / gap / drill | 0.30 mm / 0.25 mm / 0.40 mm |

The 12 V feed to the 4G modem is sized for 1 oz copper, because the modem draws up to
2.2 A in bursts. On 0.5 oz copper those tracks run hot, so pay for 1 oz if it isn't the
maker's default.

## Before you pay

1. **Lay an Adafruit INA228 board on `SOCKET_CHECK_SHEET.pdf`.** The pin order of its
   socket (MOD3) was worked out from how the module behaved in v3a's socket, not read from
   a datasheet.
2. **Lay the real modules on `FIT_CHECK_1to1.pdf`.** Check the 4G modem socket (J3) row
   spacing of 35.56 mm in particular; it is still an assumption.
3. **Read the board maker's own design check (DFM) report.** It checks things against
   their real process that no desktop tool does.

## Building it

- Every part is through-hole except three: U3 (SOT-23-6, on oversized pads for hand
  soldering) and the two Qwiic sockets J18 and J19 (1 mm JST-SH).
- All modules sit in 2.54 mm sockets, so any of them can be swapped.
- **JP1** is a solid copper wire link (0.8–1.0 mm) that closes the 12 V path when there
  is no INA228 in MOD3. Fit JP1 *or* the INA228, **never both**: together they short out
  the current-sense resistor.
- The probe terminals J5 and J6 have plug-in JST XH sockets beside them (J21 and J22).
  They are the same connection, so use either.
- For long or exposed probe cables, bond stud **E1** to an earth rod. The surge
  protection on the probe lines needs that path to work.
- Follow `FIRST_POWER_UP.pdf` before fitting the modules.

**Battery voltage.** The input surge protector D1 is rated to 15.3 V continuous. A
sodium-ion pack charging at 15.8 V is slightly above that but well below the 17.1 V
where it starts conducting, so expect a little more leakage during the final stage of
charging only. Setting the charger's absorption voltage to 15.3 V keeps it fully within
rating, at the cost of a slightly less full battery.

## What changed from v3a

- The INA228 power-monitor socket (MOD3) is re-pinned to suit the Adafruit INA228.
- JP1 link added for running without MOD3.
- Two Qwiic sockets (J18, J19) for the XM125 radar or an external INA228.
- A screw terminal for the service-mode reed switch (J20), which v3a needed hand-wired.
- Spare GPIO header (J15) extended to 11 pins.
- Earth bond stud E1 beside the probe terminals.
- 17 labelled test points, TP1–TP17.
- Larger pads for U3, which needed reworking on v3a.
- Socket pin names generated from the circuit, fixing three wrong labels on v3a.
- Clearer markings on both sides, including pin-1 and count marks on every socket.
- Power terminals J1 and J12 moved 2 mm in from the edge.
- Backup JST XH probe sockets J21 and J22.

## Firmware

The station firmware is not in this repository yet.
