# 1. Create and setup virtual environment

## Open the terminal to create a virtual environment

Press `Ctrl + Alt + t` to open the terminal.

### How to open the Terminal in Ubuntu?

- The fastest way to open the Terminal in Ubuntu is by pressing the `Ctrl + Alt + t` keyboard shortcut.
- Alternatively, open it by clicking the **Terminal** icon from the Applications menu.
- Once the Terminal is opened, a prompt such as `pai@pai:~$` will be displayed.
- **Note:** In Ubuntu Terminal, press `Ctrl + Shift + C` to copy and `Ctrl + Shift + V` to paste.

## Create a virtual environment with Python 3.12

```bash
conda create -y -n lerobot python=3.12
```

## Activate your virtual environment

```bash
conda activate lerobot
```

### What is a virtual environment?

- A virtual environment is an isolated environment that allows each project to have its own Python interpreter and packages.
- It is separated from the system Python environment, which helps prevent package conflicts between different projects.
- `conda create -y -n lerobot python=3.12` creates a Conda virtual environment named `lerobot` with Python 3.12.
- To check the existing Conda environments, use `conda env list`.
- To delete a Conda environment, use `conda env remove -n lerobot`.

### Why Python 3.12?

- Python 3.12 is selected because it provides good compatibility with LeRobot and its dependencies.
- It is also a stable and widely supported Python version.

## Install ffmpeg in your conda environment for video processing

```bash
conda install ffmpeg -c conda-forge
```

### What is FFmpeg?

- **FFmpeg** is a multimedia framework for processing video and audio. It is used in LeRobot to record robot camera footage, convert it into datasets, and decode videos included in training data.
- This usually installs ffmpeg 8.X with the `libsvtav1` encoder. If you run into issues (e.g. `libsvtav1` missing — check with `ffmpeg -encoders` — or a version mismatch with `torchcodec`), you can explicitly install ffmpeg 7.1.1 using:

  ```bash
  conda install ffmpeg=7.1.1 -c conda-forge
  ```

---

Next: [2. Install LeRobot →](02-install-lerobot.md)
