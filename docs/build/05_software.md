# 05 Software and first power-on

The runtime is [BipedRobotJetson](https://github.com/AsterisCrack/BipedRobotJetson); its README has the full
details. This page is the order to do things in on a new robot.

These steps are for the Jetson the reference robot uses. For a Raspberry Pi 5, see
[Raspberry Pi instead of the Jetson](../../bom/README.md#raspberry-pi-instead-of-the-jetson).

## 1. Set up the Jetson

Flash JetPack onto the microSD card following NVIDIA's
[Jetson Orin Nano Developer Kit getting-started guide](https://developer.nvidia.com/embedded/learn/get-started-jetson-orin-nano-devkit).

## 2. Install the runtime

```bash
git clone --recurse-submodules https://github.com/AsterisCrack/BipedRobotJetson
cd BipedRobotJetson
python3 -m venv venv && source venv/bin/activate
pip install -r requirements.txt
pip install -r requirements-hardware.txt
```

Enable the header UART (`sudo /opt/nvidia/jetson-io/jetson-io.py`, pins 8 + 10 → `uarta`), reboot, add your
user to `dialout`, and check the IMU with `sudo i2cdetect -y 7` (expect `28`).

## 3. First power-on, robot hanging

Hang the robot (or hold it) with the feet off the ground for every first test.

1. Start the server and open the web UI. All 12 servos should report position, voltage and temperature.
2. Calibrate (see [02 Servo setup, step 3](02_servo_setup.md#3-calibrate-after-assembly)).
3. Run the self-test (torque off).

## 4. Safe standing test

1. Robot hanging, torque on, Home → `stand`. Check every joint goes where the 3D view says.
2. Lower it to the ground with a hand on it, and let it stand.
3. Only then deploy a policy (BipedRobotJetson README, "Deploying a policy").
