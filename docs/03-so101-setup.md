# 3. SO‑101 Setup

## Secure the SO‑101 Leader and Follower Robot Arms

### Clamp fixing precautions

- Secure **both** the Leader and Follower arms firmly to the workbench using clamps.
- Ensure the robots are fixed in a stable position to prevent tipping or vibration during operation.
- Clamp both ends of the robot base plate securely.
- Make sure there is sufficient workspace around the robots before operation.

## Connect the SO‑101 Leader and Follower Robot Arms with the PC

### USB and power connection

- **Controller board:** Each SO‑101 arm uses a **Bus Servo Adapter (MotorBus controller)** to communicate with its six **Feetech STS3215** servos.
- **USB connection:** Connect the controller board to the PC using a USB‑A ↔ USB‑C cable for communication.
- **Power connection:** Connect a **separate power supply** to the controller board — USB does **not** power the servo motors.
- **Leader and Follower:** Each arm has its own controller board, USB connection, and power supply.

```
                ┌─────────────────────────┐
Power Supply ──▶│                         │
                │  Bus Servo Adapter      │──▶ Motor Wiring (6 × STS3215)
USB‑C ↔ USB‑A ▶│  (MotorBus controller)  │
   to PC       └─────────────────────────┘
```

## Find the USB ports associated with each arm

```bash
lerobot-find-port
```

### Identifying the MotorBus adapter ports

- Make sure **both** the Follower and Leader arms are connected to the PC via USB.
- When prompted with *"Remove the USB cable from your MotorBus and press Enter when done"*, disconnect the USB cable from one arm and press Enter.
- The output will show the port of the disconnected MotorBus adapter.
- Repeat the process for the other arm and record the corresponding ports, e.g.:
  - **Leader** → `/dev/ttyACM0`  <- paste here the port found at previous step
  - **Follower** → `/dev/ttyACM1`   <- paste here the port found at previous step

## Give access to the ports

```bash
sudo chmod 666 /dev/ttyACM0 # <- paste here the port found at previous step
sudo chmod 666 /dev/ttyACM1 # <- paste here the port found at previous step
```

### Giving access to USB serial ports

- `chmod 666` changes the permissions of the device file so that the owner, group, and other users can read and write to the serial port.
- This is needed because `/dev/ttyACM0` and `/dev/ttyACM1` are USB serial devices, and LeRobot needs read/write access to communicate with the SO‑101 MotorBus adapters.
- `sudo` is required because `/dev/ttyACM*` is a system device, and changing its permissions requires administrator privileges.

## Calibrate the robot

- First, move the robot to its **home position** before performing the calibration.
- Then, rotate each robot joint (motor) from the home position to its **minimum** and **maximum** positions to ensure that the robot has the full range of motion.

### Calibrate the Follower arm first

```bash
lerobot-calibrate \
    --robot.type=so101_follower \
    --robot.port=/dev/ttyACM1 \
    --robot.id=my_awesome_follower_arm
```

### Calibrate the Leader arm

```bash
lerobot-calibrate \
    --teleop.type=so101_leader \
    --teleop.port=/dev/ttyACM0 \
    --teleop.id=my_awesome_leader_arm
```

### Why calibrate the Leader and Follower arms?

- Calibration establishes the correct relationship between the servo positions and the physical joint positions of each arm.
- It ensures that the Leader and Follower arms have consistent joint configurations, allowing the Follower to accurately reproduce the Leader's movements.
- Calibration is especially important **before teleoperation and data collection** to improve motion accuracy and dataset quality.

## Camera finding and checking

```bash
lerobot-find-cameras opencv
```

### Why find and check available cameras?

- Finding and checking the camera configuration is required for configuring the dataset collection and rollout process.
- LeRobot offers multiple options for video capture and dataset gathering.
- You can choose to use 1, 2 or more cameras based on how many you connect.

| Class              | Supported Cameras                        |
| ------------------ | ---------------------------------------- |
| `OpenCVCamera`     | Phone, built‑in laptop, webcams          |
| `ZMQCamera`        | Network‑connected cameras                |
| `RealSenseCamera`  | Intel RealSense (with depth)             |
| `Reachy2Camera`    | Reachy 2 robot cameras                   |

---

Previous: [← 2. Install LeRobot](02-install-lerobot.md) · Next: [4. Teleoperation →](04-teleoperation.md)
