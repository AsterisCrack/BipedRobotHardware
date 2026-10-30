# Wiring

<!-- TODO: add wiring_diagram.png (and .pdf) here and embed it: battery → PCB → servos / Jetson, UART, I2C. -->

## Overview

```
Battery ──► Power PCB ──► 12 V servo bus (12× STS3215, daisy-chained)
                     └──► Jetson Orin Nano supply
Jetson UART (pins 8/10) ──► Waveshare Bus Servo Adapter (A) ──► servo bus data line
Jetson I2C bus 7 (pins 3/5) ──► BNO055 IMU (address 0x28)
```

## Servo ID map

All 12 servos share one half-duplex bus at 1 Mbaud. IDs are set once per servo (see
[build guide step 2](../../docs/build/02_servo_setup.md)). The values below are the ones in
BipedRobotJetson's `config/robot.yaml`.

| ID | Joint | Leg | direction_sign |
|---|---|---|---|
| 13 | `l_hip_yaw` | Left | +1 |
| 2 | `l_hip_roll_joint` | Left | −1 |
| 3 | `l_hip_pitch_joint` | Left | −1 |
| 4 | `l_knee_joint` | Left | −1 |
| 5 | `l_ankle_roll_joint` | Left | −1 |
| 6 | `l_ankle_pitch_joint` | Left | −1 |
| 7 | `r_hip_yaw` | Right | −1 |
| 8 | `r_hip_roll_joint` | Right | +1 |
| 9 | `r_hip_pitch_joint` | Right | +1 |
| 10 | `r_knee_joint` | Right | +1 |
| 11 | `r_ankle_roll_joint` | Right | +1 |
| 12 | `r_ankle_pitch_joint` | Right | +1 |

No joint uses ID 1, the factory default, so a servo that still answers on ID 1 is one you have not set yet.

## Jetson 40-pin header

| Pin | Signal | Goes to |
|---|---|---|
| 8 | UART TX (`/dev/ttyTHS1`) | Waveshare adapter **TX** |
| 10 | UART RX | Waveshare adapter **RX** |
| 6 | GND | Waveshare adapter GND |
| 3 | I2C bus 7 SDA | BNO055 SDA |
| 5 | I2C bus 7 SCL | BNO055 SCL |
| TODO | 3.3 V | BNO055 VIN |
| TODO | GND | BNO055 GND |

The Waveshare adapter is wired **straight through** (TX to TX, RX to RX), not crossed like most UARTs.
Crossing them gives complete silence on the bus. The header UART is disabled on a fresh Jetson image; enable
pins 8 and 10 as `uarta` with `jetson-io` (see BipedRobotJetson's README).

## IMU mounting

The BNO055 is mounted rotated **180° about the body X axis** (forward) relative to the robot frame
(X forward, Y left, Z up). The runtime corrects for it by negating Y and Z of the accelerometer and
gyro. If you mount it the other way up, change `_MOUNT_FLIP_YZ` in BipedRobotJetson's
`hardware/imu/bno055.py` to `+1.0` and re-check with the self-test.

TODO: photo of the IMU mount with the chip axes marked; BNO055 breakout used (Adafruit or other).

## Connectors

TODO: connector types and pinouts on the PCB, servo cable lengths per joint, battery connector.
