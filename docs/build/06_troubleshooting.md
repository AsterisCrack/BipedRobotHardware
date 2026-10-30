# 06 Troubleshooting

| Symptom | Cause | Fix |
|---|---|---|
| No servo answers at any baud rate | UART TX/RX crossed | The Waveshare adapter is straight-through: TX to TX, RX to RX |
| Port opens but nothing is sent | Header UART not enabled | `jetson-io.py`: set pins 8 + 10 to `uarta`, reboot; `/sys/class/tty/ttyTHS1/uartclk` must be non-zero |
| Two servos fight / bus errors | Two servos share an ID (often a new one still at ID 1) | Reassign IDs one servo at a time |
| A joint moves the wrong way | `direction_sign` wrong | Toggle it in the Robot tab Config panel |
| Robot leans or the policy behaves oddly | `default_position_deg` wrong for some joint, or a horn reseated without recalibrating | Recalibrate (step 02) |
| IMU tilt has the wrong sign | IMU mounted differently from the reference build | See [IMU mounting](../../electronics/wiring/README.md#imu-mounting) |
| BNO055 not at 0x28 | ADDR pin high, or wiring | Check `i2cdetect -y 7`; ADDR low gives 0x28 |

TODO: add what you hit during your own build.
