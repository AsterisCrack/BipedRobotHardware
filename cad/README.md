# CAD

| File | |
|---|---|
| [`step/robot_assembly.zip`](step/robot_assembly.zip) | The full robot assembly as STEP (zipped: the raw file is 160 MB) |
| [`step/bodies/`](step/bodies/) | One STEP per printed part |
| [`fusion/`](fusion/) | The Fusion 360 archive (`Robot.f3z`), attached to the [latest release](https://github.com/AsterisCrack/BipedRobotHardware/releases/latest) because it is over GitHub's 100 MB file limit |

STEP opens in any CAD tool (FreeCAD, Onshape, SolidWorks, Fusion 360...). Units are millimetres, and the
robot frame follows the URDF: X forward, Y left, Z up.

## Parts

| STEP | Printed as | Qty |
|---|---|---|
| `body.step` | `body.stl` | 1 |
| `IMU_tray.step` | `IMU_tray.stl` | 1 |
| `hip_and_ankle.step` | `ankle_and_hip.stl` | 4 |
| `thigh.step` | `thigh.stl` | 2 |
| `calf.step` | `calf.stl` | 2 |
| `left_upper_hip.step`, `right_upper_hip.step` | `left_upper_hip.stl`, `right_upper_hip.stl` | 1 each |
| `left_foot.step`, `right_foot.step` | `left_foot.stl`, `right_foot.stl` | 1 each |

The legs are mirror images, and most parts are the same on both sides: print them twice. Only the upper hips
and the feet have separate left and right versions.
