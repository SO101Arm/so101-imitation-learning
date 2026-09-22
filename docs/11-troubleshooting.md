# 11. Troubleshooting

## `ConnectionError` — cause & troubleshooting

Common causes when the recording or teleoperation script fails to open the arms:

- Wrong port assigned to Leader / Follower. Re‑run `lerobot-find-port` and update `--robot.port` / `--teleop.port`.
- Missing serial permissions. Re‑apply:

  ```bash
  sudo chmod 666 /dev/ttyACM0
  sudo chmod 666 /dev/ttyACM1
  ```
- Bus Servo Adapter power cable unplugged — USB alone does **not** power the servos.
- Cameras occupied by another process (browser tab, other terminal). Close them or pick a different `index_or_path`.

## Resume collecting a dataset

- If an issue occurs or you want to record additional episodes in the same dataset, you can resume by re‑running the same command with `--resume=true`.
- When resuming a recording, `--dataset.num_episodes` must be set to the **number of additional episodes** to be recorded.
- Make sure that you also set `--dataset.root="local_path"` — it's a local path to save the new part of the dataset and is required to resume.

See the full resume command in [7. Dataset Record](07-dataset-record.md#resume-collecting-a-dataset).

## ffmpeg / `libsvtav1` errors

- Default conda install pulls ffmpeg 8.x with the `libsvtav1` encoder.
- If `libsvtav1` is missing (check via `ffmpeg -encoders`) or you hit a `torchcodec` version mismatch, pin ffmpeg to 7.1.1:

  ```bash
  conda install ffmpeg=7.1.1 -c conda-forge
  ```

## `cmake` / build failures during `pip install`

Install the pinned cmake into your conda env before retrying the LeRobot install:

```bash
conda install -c conda-forge cmake=3.28
```

---

Previous: [← 10. Rollout](10-rollout.md) · Back to [README](../README.md)
