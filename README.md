# RiverNode build files

RiverNode is a solar-powered station that records river and air temperature, and
optionally the water level, and uploads it to an open dashboard at
[rivernode.uk](https://rivernode.uk). This repository holds the files you need to make
the hardware yourself:

| Folder | What it is | Status |
|---|---|---|
| [`board/`](board/) | Main circuit board **v3a.2**: gerbers, board render, schematic, parts list | The tracks of the board already built and running, refined from building it |
| [`enclosure/`](enclosure/) | Printed base, cover and test-fit coupon for the board | Fits v3a and v3a.2 |
| [`radar-housing/`](radar-housing/) | Under-bridge housing for the SparkFun XM125 water-level radar, version 2 | Printable now |

The full parts list with prices is at [rivernode.uk/bom/](https://rivernode.uk/bom/), and
help choosing a power set-up for your site is at
[rivernode.uk/choosing-your-node/](https://rivernode.uk/choosing-your-node/).

![RiverNode v3a.2 board](board/RiverNode_v3a2_render.png)

## Recommended power for year-round monitoring

| Part | Choice |
|---|---|
| Battery | **Beyond Batteries NA10**, 10 Ah sodium-ion. Charges to 15.8 V; works from 8 to 15.8 V |
| Solar panel | **30 W "24 V" panel** (72 cells, Vmp about 36 V, Voc 42–43.5 V). One panel only: never two in series |
| Charge controller | **Victron SmartSolar MPPT 75/10**. It also reports the battery and solar figures to the station over Bluetooth |

Set the Victron to a **user-defined** charge profile, not the lithium preset:
absorption 15.8 V, maximum charge voltage 15.8 V, float 13.2–13.4 V, equalisation off,
temperature compensation off. The standard load-output cut-off (11.1 V or 11.8 V) turns
the station off while a sodium-ion pack still has charge in it, so ask the battery maker
for a cut-off voltage and set it as a custom value.

**Why this size.** A station measured on the bench used about 3.7 Wh a day, and the
Victron's own standby adds about 5.8 Wh, so plan on roughly 9.5 Wh a day. Running the
NA10 from 90 % down to 20 % gives about 84 Wh, which is around nine days with no useful
sun. A 30 W panel covers the daily use with under half an hour of full sun, and refills
the battery in about three bright days. A "24 V" panel is chosen for its voltage: the
controller only starts charging once the panel is 5 V above the battery, and a 15.8 V
sodium-ion pack needs a panel with a Vmp of at least 20 V. A "12 V" panel (Vmp about
18 V) leaves the battery slightly undercharged.

## Licence

Everything here is licensed under
[Creative Commons Attribution-NonCommercial-ShareAlike 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)
(CC BY-NC-SA 4.0). See [LICENSE](LICENSE).

You may make, change and share these designs for non-commercial use, such as building
stations for your own club or river group, as long as you credit RiverNode and share any
changes under the same licence. Selling boards, kits or stations made from them needs
permission: ask through [rivernode.uk](https://rivernode.uk).

© 2026 RiverNode.

## No warranty

These files are provided as they are, without any warranty. Check everything against
the real parts before you pay for boards, and take care with batteries, mains chargers
and anything you fix near a river. In England, fixing anything in, over or near a main
river can need a permit from the Environment Agency, and you always need the
landowner's permission.
