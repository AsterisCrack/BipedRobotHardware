# 03 Legs, hips and torso

Set every servo's ID first ([02 Servo setup](02_servo_setup.md)): once a servo is inside a leg, it is hard
to reach. All screws are the ones that come with the servos.

Assemble one leg completely, check that it moves freely, then build the other one.

## Left leg, from the foot up

| Step | Printed part | Joint that moves it (servo ID) |
|---|---|---|
| 1 | `left_foot` | Ankle pitch (6) |
| 2 | `ankle_and_hip` (ankle) | Ankle roll (5) |
| 3 | `calf` | Knee (4) |
| 4 | `thigh` | Hip pitch (3) |
| 5 | `ankle_and_hip` (lower hip) | Hip roll (2) |
| 6 | `left_upper_hip` | Hip yaw (13) |

## Right leg

The same steps with `right_foot`, `right_upper_hip` and IDs 12, 11, 10, 9, 8, 7 (ankle pitch to hip yaw).

## Torso

Mount both legs on `body`, fit the BNO055 in `IMU_tray` (orientation:
[04 Electronics](04_electronics.md#4-imu)), and route the servo cables up each leg to the body.

## Check

With the torques off, move every joint through its range by hand. Nothing should bind, and no cable should
pull. The assembly in [`cad/step/robot_assembly.zip`](../../cad/step/robot_assembly.zip) shows where every
part and servo goes.
