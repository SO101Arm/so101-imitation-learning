# SO-101 Robot — Imitation Learning Training

> **Physical AI Lab — PAI Lab**
>
> End‑to‑end manual for teleoperating the **SO‑101** robot with **Hugging Face LeRobot**, recording datasets, training an Imitation Learning policy, and rolling it out on the real robot.

This repository is a GitHub‑friendly transcription of the internal PAI Lab slide manual `Template-02-190926`.

---

## Table of Contents

1. [Create and setup virtual environment](docs/01-virtual-environment.md)
2. [Install LeRobot](docs/02-install-lerobot.md)
3. [SO-101 Robot Setup](docs/03-so101-setup.md)
4. [Teleoperation](docs/04-teleoperation.md)
5. [Hugging Face](docs/05-hugging-face.md)
6. [Problem Definition](docs/06-problem-definition.md)
7. [Dataset Record](docs/07-dataset-record.md)
8. [Dataset Analysis](docs/08-dataset-analysis.md)
9. [Training](docs/09-training.md)
10. [Rollout](docs/10-rollout.md)
11. [Troubleshooting](docs/11-troubleshooting.md)

---

## What you will build

An Imitation Learning pipeline where the SO‑101 **Leader** arm teleoperates the **Follower** arm while the system records synchronized joint positions and camera images. That dataset is uploaded to the Hugging Face Hub, used to train an ACT policy, and finally rolled out on the Follower arm.

```
[Data Collection]
Teleoperation
      ↓
Observation + Action
      ↓
[Model Training]
Observation → Action
      ↓
[Policy Execution]
Observation
      ↓
Policy
      ↓
Action Prediction
      ↓
Robot Control
```

## Requirements

- Ubuntu with `conda` (Miniconda / Anaconda)
- Two SO‑101 arms (Leader + Follower), each with a Bus Servo Adapter and independent power supply
- One or more USB cameras (webcam, built‑in laptop cam, RealSense, etc.)
- A Hugging Face account with a **Write** access token
- NVIDIA GPU with CUDA (recommended for training)

## Quick start

```bash
# 1. Environment
conda create -y -n lerobot python=3.12
conda activate lerobot
conda install ffmpeg -c conda-forge

# 2. LeRobot
pip3 install --upgrade pip
git clone https://github.com/huggingface/lerobot.git
cd lerobot
pip install -e ".[core_scripts]"
pip install -e ".[training]"
pip install -e ".[feetech]"
pip install -e ".[all]"

# 3. Find ports, calibrate, teleoperate, record, train, rollout
#    → follow docs/03 through docs/10
```

See each linked section for the full commands and explanations.

---

## License

This manual is provided for internal use in the Physical AI Lab (PAI Lab).
LeRobot is © Hugging Face, released under the terms in [huggingface/lerobot](https://github.com/huggingface/lerobot).
