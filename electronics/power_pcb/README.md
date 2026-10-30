# Power distribution PCB

<p align="center">
  <img src="pcb.jpg" alt="Power distribution PCB" height="300"/>
</p>

Distributes battery power to the 12 servos and the Jetson, so the wiring is stable and modular.

**Fabricated and assembled by [PCBWay](https://www.pcbway.com/), who sponsored this board.**
<!-- TODO: confirm with PCBWay whether they want a specific link or wording. -->

## Specs

| | |
|---|---|
| Input | TODO V, TODO A max (battery: TODO) |
| Servo outputs | TODO × TODO V (servo bus connectors: TODO) |
| Compute output | TODO V, TODO A to the Jetson Orin Nano |
| Other outputs | TODO |
| Protection | TODO (fuse, reverse polarity, ...) |
| Size | TODO × TODO mm, TODO layers |
| Connectors | TODO (part numbers in `fabrication/bom.csv`) |

## Files

| Path | Contents |
|---|---|
| [`source/`](source/) | KiCad / EasyEDA project: modify the board from here |
| [`fabrication/`](fabrication/) | Exactly what PCBWay needs to make it as-is: `gerbers.zip`, `bom.csv`, `cpl.csv` |
| `schematic.pdf` | Schematic, readable without the EDA tool |
| [`renders/`](renders/) | 3D renders and board photos |

## Ordering

1. Upload `fabrication/gerbers.zip` to [PCBWay](https://www.pcbway.com/) (TODO: board thickness, copper weight, finish).
2. For assembly, add `fabrication/bom.csv` and `fabrication/cpl.csv`.
3. TODO: anything to check on the order (parts to hand-solder, polarity of the input connector).
