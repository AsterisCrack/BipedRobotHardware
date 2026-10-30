# BipedRobotHardware

**Open hardware for a small 12-servo biped that learns to walk in simulation.**
CAD, print files, bill of materials, power PCB, robot description (URDF) and build guide.

<p align="center">
  <img src="media/robot.jpeg" alt="Sir Servington" width="35%"/>
</p>

<!-- TODO: hero GIF of Sir Servington walking (media/walking.gif) -->

| Software | |
|---|---|
| [BipedRobot](https://github.com/AsterisCrack/BipedRobot) | Training (Isaac Lab + MuJoCo), servo model, policy export |
| [BipedRobotJetson](https://github.com/AsterisCrack/BipedRobotJetson) | On-robot runtime: servo bus, IMU, web UI, policy loop |

---

## Specs

| | |
|---|---|
| Height | About 38 cm with the legs straight |
| Mass | 1.66 kg in the CAD model |
| Degrees of freedom | 12 (per leg: hip yaw, hip roll, hip pitch, knee, ankle roll, ankle pitch) |
| Actuators | 12× Waveshare ST3215 serial bus servos (12 V, 30 kg·cm), one shared bus at 1 Mbaud |
| Compute | NVIDIA Jetson Orin Nano Super, 50 Hz control loop (a Raspberry Pi 5 also works, see [Cost](#cost)) |
| IMU | BNO055 on I2C |
| Power | 3S LiPo (11.1 V, 2200 mAh) through a custom power PCB |
| Structure | 14 printed parts, PLA, printed on a stock Ender-3 V2 |
| Fasteners | Only the screws that come with the servos |
| Cost | Under $500 with a Raspberry Pi 5 (≈ $418 with the 2 GB model); ≈ $730 with the Jetson. Prices checked October 2026 |

---

## Where to start

| I want to... | Go to |
|---|---|
| See what to buy and what it costs | [`bom/`](bom/) |
| Print the parts | [`print/`](print/) |
| Modify the design | [`cad/`](cad/) (STEP for any CAD tool, Fusion 360 archive in the release) |
| Order or build the power board | [`electronics/power_pcb/`](electronics/power_pcb/) |
| Wire it | [`electronics/wiring/`](electronics/wiring/) |
| Build it | [`docs/build/`](docs/build/) |
| Simulate it | [`robot_description/`](robot_description/) (URDF + meshes) |

The [latest release](https://github.com/AsterisCrack/BipedRobotHardware/releases/latest) has the STLs,
the gerbers and the Fusion 360 archive as downloads, so you don't need to clone the repo.

---

## Cost

| Part | Cost (USD) |
|---|---|
| 12× Waveshare ST3215 servos | 263.88 |
| BNO055 IMU | 17.00 |
| Power PCB | 25.00 |
| Waveshare Bus Servo Adapter (A) | 4.99 |
| 3S 2200 mAh LiPo | 20.00 |
| **Robot without a computer** | **330.87** |

| With... | Total (USD) |
|---|---|
| Raspberry Pi 5, 2 GB + 12 V → 5 V USB-C step-down | **≈ 418** |
| Raspberry Pi 5, 4 GB + 12 V → 5 V USB-C step-down | **≈ 451** |
| NVIDIA Jetson Orin Nano Super (reference robot) | **≈ 730** |

The policy is a small network that runs on the CPU, so a **Raspberry Pi 5 can replace the Jetson** and keeps the
robot under $500. The Jetson costs $399 at NVIDIA's list price since July 2026 (it launched at $249). The
reference robot runs on the Jetson; the Pi setup (power, wiring, two config changes) is in
[`bom/README.md`](bom/README.md#raspberry-pi-instead-of-the-jetson) and hasn't been tested on the robot yet.

Prices were checked in October 2026; details and links are in [`bom/`](bom/). Not in the prices: the microSD
card, about 0.5 kg of PLA and small parts (wires, switch, leads, fuses). Tools: a 3D printer, a soldering
iron and a LiPo balance charger.

---

## Repository layout

```
cad/
├── step/              Assembly (zipped) + one STEP per printed part
└── fusion/            Fusion 360 archive (download from the release)
print/stl/             One STL per printed part, with print notes in print/README.md
robot_description/     URDF + meshes (ROS package "Robot_description")
electronics/
├── Schematic_RobotPCB.pdf
├── power_pcb/         Power PCB: EasyEDA source, gerbers, BOM, pick-and-place, render
└── wiring/            Servo ID map, Jetson pinout, IMU mounting
bom/                   Purchased parts and printed parts (CSV)
docs/build/            Build guide
media/                 Photos
```

The software repos include this one as a git submodule (`robot_hardware/`), so the robot description
used for training and on the robot is always the one in this repo.

---

## Credits

<p>
  <img src="media/pcbway.png" alt="PCBWay logo" height="40"/>
</p>

- The power PCB was fabricated and assembled by [PCBWay](https://www.pcbway.com/), who sponsored this board.
- The servo model used in simulation builds on Rhoban's [BAM](https://github.com/Rhoban/bam).
- The URDF was exported from Fusion 360 with [fusion2urdf](https://github.com/syuntoku14/fusion2urdf)
  (MIT, see [`robot_description/LICENSE-fusion2urdf`](robot_description/LICENSE-fusion2urdf)).

---

## License

The hardware design (CAD, print files, PCB, robot description, documentation) is licensed under the
[CERN Open Hardware Licence Version 2 - Permissive](LICENSE) (CERN-OHL-P-2.0).
The exporter template files in `robot_description/` keep their own MIT licence; the robot design itself is
covered by CERN-OHL-P. The software repos are MIT.
