# Printing

All parts are in [`stl/`](stl/), one file per part, in millimetres. The legs are mirror images, so most
files are printed twice; only the upper hips and the feet have separate left and right files.

| File | Qty | Notes |
|---|---|---|
| `body.stl` | 1 | |
| `IMU_tray.stl` | 1 | |
| `ankle_and_hip.stl` | **4** | Lower hip and ankle are the same part. **Critical**, see below |
| `thigh.stl` | 2 | |
| `calf.stl` | 2 | |
| `left_upper_hip.stl` | 1 | |
| `right_upper_hip.stl` | 1 | |
| `left_foot.stl` | 1 | |
| `right_foot.stl` | 1 | |
| **Total** | **14 parts** | About 0.5 kg of PLA |

## Settings

The reference robot was printed in PLA on a stock Creality Ender-3 V2 with the slicer's default PLA profile.
Nothing about this design needs special tuning: use your printer's default PLA settings, and add supports
where your slicer asks for them.

## The one part that matters: `ankle_and_hip.stl`

The lower-hip/ankle bracket is the part most likely to break when the robot falls. For all 4 copies:

- **Print it tilted 45°** on the bed, so the layer lines don't line up with the load from a fall.
- **Use at least 6 walls** (perimeters).

Print a spare or two: it's the part you'll replace first.
