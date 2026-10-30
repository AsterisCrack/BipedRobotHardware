# 04 Electronics

Wiring reference: [`electronics/wiring/`](../../electronics/wiring/). Board: [`electronics/power_pcb/`](../../electronics/power_pcb/).

## 1. Power PCB

TODO: mounting, battery connector, servo bus outputs, Jetson supply. Check polarity with a multimeter
**before** connecting anything.

## 2. Servo bus

TODO: daisy-chain order per leg, cable routing.

## 3. Jetson and servo adapter

Waveshare Bus Servo Adapter (A), wired **straight through**: Jetson pin 8 (TX) to adapter TX, pin 10 (RX)
to adapter RX, pin 6 to GND.

## 4. IMU

BNO055 on I2C bus 7 (pin 3 SDA, pin 5 SCL), address 0x28. Mount it rotated 180° about the robot's X
(forward) axis, as on the reference build. The runtime corrects for exactly that mounting; see
[wiring](../../electronics/wiring/README.md#imu-mounting) if yours differs.

![TODO: IMU mount](img/04_imu_mount.jpg)

## Check

Power on with the Jetson disconnected first, and check the voltages at the servo and Jetson outputs.
TODO: expected values.
