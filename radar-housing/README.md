# Under-bridge radar housing, version 2

A housing for the **SparkFun XM125** 60 GHz radar and a **SparkFun QwiicBus EndPoint**,
fixed to the underside of a bridge to measure the distance down to the water. The lid
is a lens that focuses the radar into a beam about 6° wide, for water **1–3 m below**.
The network cable from the station comes in through an M20 gland.

| File | Material | Print |
|---|---|---|
| `radar-housing-v2-body.stl` | PETG or ASA | Flange and box in one part. Flange down on the bed, no supports |
| `radar-housing-v2-lens-lid.stl` | **Light-coloured** ASA or PETG | **100 % infill.** Print it as it comes, then turn it over like a page: the dome goes inside, over the radar. The screw lugs are spaced unevenly, so it only fits one way round |
| `radar-housing-v2-lid-gasket-tpu.stl` | TPU 95A | Lid seal. Or use 2.0 mm round EPDM or silicone cord in the lid groove instead |
| `radar-housing-v2-flange-seal-tpu.stl` | TPU 95A | Seal between the flange and the bridge. Or fill the flange groove with neutral-cure silicone and screw up while it is wet. It does **not** fit the lid |
| `radar-focus-spacer.stl` | PETG | Print 8: 4 fitted and 4 for focus tuning |
| `radar-level-shim.stl` | PETG | Print 8: 1 mm packers for levelling |

**Print with a 0.6 mm nozzle:** the wall, tongue and floor thicknesses are multiples of
its line width. **Don't use black filament for the lid.** The carbon black in it absorbs
60 GHz radar.

## Other parts you need

- Knurled M3 × 5.7 heat-set inserts (every M3 hole takes one)
- Stainless screws: 6 × M3 × 10 countersunk (lid), 4 × M3 × 10 (radar, with one spacer
  each), 4 × M3 × 8 (EndPoint)
- M20 × 1.5 cable gland and locknut
- M12 × 1.5 IP68 breather membrane vent, in the hole in the side wall
- 4 countersunk wood screws for the flange (the holes are 4.5 mm)
- Short Qwiic cable between the two boards
- A silica gel sachet

## Fitting

1. Fit the inserts. Mount the radar board on its four posts with one focus spacer under
   each, and the EndPoint with its network socket facing the gland.
2. **Focus.** One spacer per post gives the designed 25 mm focus. Remove them to move the
   sensor 2.5 mm further from the lens, or use two per post to move it 2.5 mm closer. On
   the bench, point it at a floor 1–3 m away and keep whichever setting gives the
   strongest echo on the station's service page.
3. Put a silica gel sachet in the empty strip beside the radar. Without it, condensation
   forms drops on the lens, and drops block a lot of a 60 GHz signal.
4. Fit the lid gasket and the six lid screws.
5. Screw the flange to the underside of the bridge, with its seal.
6. **Level it to within ±2.5° both ways.** Calm water reflects like a mirror, so a tilted
   beam misses the sensor. Hold a phone level against the lid's flat outer face, along
   it and then across it. Take each reading twice with the phone turned end for end, and
   average the two. Correct any tilt by slipping 1 mm shims under a flange corner; each
   one tilts the housing about 0.5°.
7. Set the station's depth baseline with the lid fitted. The lens adds a small fixed
   offset to the distance, and the baseline takes it out.

After a flood, drops left on the lens weaken the echo until they drain or dry, so expect
poorer readings for a while.
