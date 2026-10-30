# Changelog

## v2.0 (2026-10-30)

First public release of Sir Servington, the robot the current policies in
[BipedRobot](https://github.com/AsterisCrack/BipedRobot) are trained for and run on.

- 12 Waveshare ST3215 servos, Jetson Orin Nano Super, BNO055 IMU, 3S LiPo.
- Custom power distribution PCB, fabricated and assembled by PCBWay.
- URDF with an `imu_link` at the BNO055 mounting point.

The model of the earlier V1 robot is still in BipedRobot (`--task BipedRobot`).
