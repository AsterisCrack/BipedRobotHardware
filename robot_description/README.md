# Robot description

The robot's kinematic and inertial model, exported from the Fusion 360 design with
[fusion2urdf](https://github.com/syuntoku14/fusion2urdf). This folder is the single source of truth: the
training repo ([BipedRobot](https://github.com/AsterisCrack/BipedRobot)) and the on-robot runtime
([BipedRobotJetson](https://github.com/AsterisCrack/BipedRobotJetson)) both include this repo as a
submodule at `robot_hardware/` and read the URDF and meshes from here.

| File | |
|---|---|
| `urdf/Robot.urdf` | The URDF as exported, with xacro includes for materials, transmissions and Gazebo |
| `urdf/robot_flat.urdf` | The same URDF without the xacro includes. Loads in any URDF tool (urdf-loader, PyBullet, MuJoCo, ikpy) |
| `urdf/materials.xacro`, `Robot.trans`, `Robot.gazebo` | ROS/Gazebo extras from the exporter |
| `meshes/*.stl` | One mesh per link, in millimetres (the URDF scales them by 0.001) |
| `package.xml`, `CMakeLists.txt`, `launch/` | ROS package files. The package name is `Robot_description`, so mesh paths are `package://Robot_description/meshes/...` |

## Links and joints

Frame: X forward, Y left, Z up. 12 revolute joints plus a fixed `imu_joint` at the BNO055.

| Joint | Parent → child | Axis | Range (rad) |
|---|---|---|---|
| `l_hip_yaw` / `r_hip_yaw` | base_link → hip_upper | ±Z | ±0.785 |
| `l_hip_roll_joint` / `r_hip_roll_joint` | hip_upper → hip_lower | ±X | −0.436 … 1.571 |
| `l_hip_pitch_joint` / `r_hip_pitch_joint` | hip_lower → thigh | Y | ±1.571 |
| `l_knee_joint` / `r_knee_joint` | thigh → calf | −Y | ±2.094 |
| `l_ankle_roll_joint` / `r_ankle_roll_joint` | calf → ankle | ±X | ±1.396 |
| `l_ankle_pitch_joint` / `r_ankle_pitch_joint` | ankle → foot | Y | −0.611 … 1.484 |

| Link | Mass (kg) |
|---|---|
| base_link (torso, electronics) | 0.633 |
| hip_upper ×2 | 0.101 |
| hip_lower ×2 | 0.021 |
| thigh ×2 | 0.169 |
| calf ×2 | 0.105 |
| ankle ×2 | 0.021 |
| foot ×2 | 0.097 |
| **Total** | **1.661** |

TODO: weigh the real parts and update these masses if they differ. The simulator's dynamics depend on them.

## Changing the description

1. Re-export from Fusion 360 with fusion2urdf. Keep the link and joint names: the software repos use them.
2. Regenerate `urdf/robot_flat.urdf` (strip the `xmlns:xacro` attribute and the three `<xacro:include>` lines).
3. In BipedRobot:
   - update the inertials copied into the MuJoCo model
     (`envs/assets/robotV2/robot_v2.xml`);
   - re-import the URDF into Isaac Sim to regenerate the USD in `envs/assets/robotV2/usd/`.
4. Commit here, then bump the `robot_hardware` submodule in both software repos.

The MuJoCo model (`robot_v2.xml`) lives in BipedRobot rather than here, because it is a simulation model
(floor, contact settings, sensor sites) that changes with simulation work. It reads its meshes from this
folder.

## Licence

The robot design, meshes and URDF content are licensed under CERN-OHL-P-2.0 (see [`../LICENSE`](../LICENSE)).
The exporter's template files (CMakeLists.txt, package.xml, launch files) come from fusion2urdf, MIT ©
Toshinori Kitamura: see [`LICENSE-fusion2urdf`](LICENSE-fusion2urdf).
