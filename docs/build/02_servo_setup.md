# 02 Servo setup

Do this **before** mounting any servo in the structure. A servo with the wrong ID or a horn on the wrong
spline is the most common cause of a robot that moves wrongly, and it is hard to fix once the leg is closed.

Everything here uses BipedRobotJetson's web UI. Install it on the Jetson first (step 05, "Install"), or run it
on a PC with a USB-to-SCS adapter (`UART_PORT=/dev/ttyUSB0`).

## 1. Set the IDs

New STS3215s all ship as ID 1, so they cannot share the bus until each has its own ID.

1. Connect **one servo at a time** to the bus.
2. Debug tab → *Reassign Servo IDs* (torque off) → give it its ID from the map below.
3. Label the servo with its ID and joint (tape on the case).

| ID | Joint | ID | Joint |
|---|---|---|---|
| 13 | `l_hip_yaw` | 7 | `r_hip_yaw` |
| 2 | `l_hip_roll_joint` | 8 | `r_hip_roll_joint` |
| 3 | `l_hip_pitch_joint` | 9 | `r_hip_pitch_joint` |
| 4 | `l_knee_joint` | 10 | `r_knee_joint` |
| 5 | `l_ankle_roll_joint` | 11 | `r_ankle_roll_joint` |
| 6 | `l_ankle_pitch_joint` | 12 | `r_ankle_pitch_joint` |

![TODO: labelled servos](img/02_labelled_servos.jpg)

## 2. Centre before mounting the horn

TODO: centre each servo (encoder 2048) with torque on, then fit the horn in the orientation shown, so every
joint has its full range on both sides.

![TODO: horn orientation per joint](img/02_horn_orientation.jpg)

## 3. Calibrate (after assembly)

The software works in two angle spaces:

- **URDF space**: 0° at the servo's calibrated centre (`zero_offset_steps`).
- **Logical space**: 0° at the robot's standing pose. `logical = urdf − default_position_deg`.

The policy, the poses and the UI sliders use logical space, so `default_position_deg` must be right for
every joint or every observation and command is shifted.

Once the robot is assembled (after step 04):

1. Disable all torques and hold the robot by hand in its standing pose.
2. **Direction.** Robot tab → Config panel: toggle each joint's sign until the slider moves the real joint
   the same way as the 3D model.
3. **Zero.** Debug tab → *Set Current As Zero (config)* writes `zero_offset_steps` to `config/robot.yaml`.
4. **Standing offset.** With the robot in the pose you want as logical zero, click **Set Here** per joint,
   then **Print Config**, and copy the servo entries into `config/robot.yaml`.
5. Restart and run the self-test (step 05).

Repeat the calibration whenever you reseat a horn.

## 4. PID

The PID is P-only (`p: 32, d: 0, i: 0`) on purpose: the simulated servo model the policy was trained with
is a P-only firmware loop. The runtime refuses to arm a policy whose required PID does not match the config.
