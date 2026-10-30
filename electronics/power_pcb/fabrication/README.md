# Fabrication files

What PCBWay needs to make and assemble the board as-is:

| File | |
|---|---|
| `gerbers.zip` | Gerbers + drill files |
| `bom.csv` | Components: designator, value, footprint, manufacturer part number, quantity |
| `cpl.csv` | Pick-and-place (component placement list): designator, X, Y, rotation, layer |

Generate them from the same revision as [`../source/`](../source/) and [`../schematic.pdf`](../).
