# 2. Install LeRobot

## LeRobot Framework

### What is LeRobot?

- **LeRobot** is an open‑source robot learning framework developed by Hugging Face.
- It provides an end‑to‑end platform for applying AI to robots, supporting **Imitation Learning (IL)** and **Reinforcement Learning (RL)**.
- It supports robot arms such as SO‑100, SO‑101 and Koch v1.1 and has an active community with **22.1k+** GitHub stars.

## Pip update the newest version

```bash
pip3 install --upgrade pip
```

### Importance of Updating pip

- The `pip` included in a new virtual environment may be outdated.
- Updating `pip` improves dependency resolution and helps reduce installation errors.
- LeRobot's `pyproject.toml` build system recommends using the latest pip.

## Git clone the LeRobot repository and navigate into the directory

LeRobot GitHub link: <https://github.com/huggingface/lerobot>

```bash
git clone https://github.com/huggingface/lerobot.git
cd lerobot
```

### Git Clone and Directory Navigation

- `git clone https://github.com/huggingface/lerobot.git` clones the latest LeRobot source code from the remote GitHub repository.
- `cd lerobot` moves into the newly created `lerobot` directory.
- The `lerobot` directory contains the LeRobot source code and configuration files.

## Troubleshooting

```bash
conda install -c conda-forge cmake=3.28
```

## Install the dependencies in editable mode

```bash
pip install -e ".[core_scripts]"
pip install -e ".[training]"
pip install -e ".[feetech]"
pip install -e ".[all]"
```

### Installing LeRobot Dependencies

- `pip install -e ".[core_scripts]"` installs LeRobot with the dependencies required for its core scripts.
- `pip install -e ".[training]"` installs additional dependencies required for model training.
- `pip install -e ".[all]"` installs all optional dependencies for full LeRobot functionality.
- These packages are required to ensure that recording, training, evaluation, and other LeRobot features work correctly.

### Editable Mode

- `pip install -e` installs the package in **editable mode**, linking the installed package to the local source code.
- This allows changes to the LeRobot source code to be used immediately without reinstalling the package.
- Editable mode is useful for development, debugging, and modifying LeRobot code.

---

Previous: [← 1. Virtual environment](01-virtual-environment.md) · Next: [3. SO‑101 Robot Setup →](03-so101-setup.md)
