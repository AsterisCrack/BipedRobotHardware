# Bill of materials

| File | |
|---|---|
| [`bom.csv`](bom.csv) | Everything you buy, with prices and links |
| [`printed_parts.csv`](printed_parts.csv) | Everything you print: 9 files, 14 parts |

## Summary

| Qty | Part | USD |
|---|---|---|
| 12 | Waveshare ST3215 servo, 12 V | 263.88 |
| 1 | BNO055 IMU breakout | 17.00 |
| 1 | Power distribution PCB ([`electronics/power_pcb`](../electronics/power_pcb/)) | 25.00 |
| 1 | Waveshare Bus Servo Adapter (A) | 4.99 |
| 1 | 3S LiPo, 2200 mAh, XT60 | 20.00 |
| | **Robot without a computer** | **330.87** |

Add the computer:

| Computer | Extra parts | Computer cost | **Robot total** |
|---|---|---|---|
| Raspberry Pi 5, 1 GB | 12 V → 5 V 5 A USB-C step-down (~$10) | 55.00 | **≈ $386** |
| Raspberry Pi 5, 2 GB | 12 V → 5 V 5 A USB-C step-down (~$10) | 87.50 | **≈ $418** |
| Raspberry Pi 5, 4 GB | 12 V → 5 V 5 A USB-C step-down (~$10) | 120.00 | **≈ $451** |
| NVIDIA Jetson Orin Nano Super (reference robot) | none | 399.00 | **≈ $730** |

Any Raspberry Pi 5 keeps the robot under $500. With a Jetson it stays above that, even at its $249 launch
price (≈ $580).

Prices were checked in October 2026 (Raspberry Pi list prices as of 12 Oct 2026) and drift; check before
you order. Rows marked "estimate" in the CSV are typical prices for generic parts rather than a specific
listing.

**Not in the prices:** the microSD card, about 0.5 kg of PLA, and the small parts (wires, power switch,
XT60 and barrel leads, 2 blade fuses). The build uses only the screws that come with the servos. You also
need a 3D printer, a soldering iron and a LiPo balance charger.

## Raspberry Pi instead of the Jetson

The Jetson is more than half the cost of the robot, and the policy doesn't need it: it is a small MLP that
the runtime runs on the CPU with onnxruntime, well within a Raspberry Pi 5's budget at 50 Hz. The rest of
the hardware is the same.

- **Power:** the Pi 5 needs 5 V over USB-C, not battery voltage. Connect a 12 V → 5 V, 5 A step-down module
  with a USB-C output to the PCB's JETSON terminal.
- **Wiring:** the Pi's 40-pin header uses the same pins as the Jetson: UART on pins 8/10 to the servo
  adapter, I2C on pins 3/5 to the BNO055.
- **Software:** [BipedRobotJetson](https://github.com/AsterisCrack/BipedRobotJetson) runs as-is with two
  settings changed. Set `UART_PORT=/dev/ttyAMA0` (after enabling the UART with `dtparam=uart0=on`) and set
  `i2c_bus: 1` in `config/hardware.yaml`. Skip `Jetson.GPIO` when installing the hardware requirements.

The reference robot runs on the Jetson; the Raspberry Pi setup has not been tested on it yet.
