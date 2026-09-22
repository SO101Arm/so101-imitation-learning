# 7. Dataset Record

## Data Collection Process

- Data collection follows a repeated **Recording → Reset → Recording** cycle.
- After the configured episode recording time (`episode_time_s`), the system automatically moves to the **Reset** stage.
- During the reset time, reposition the object to its initial position and prepare for the next episode.
- This cycle is repeated for the configured number of episodes (`num_episodes`).
- After all episodes are completed, the recording automatically ends and the dataset is uploaded.

## Recording dataset command

Activate the env and set your HF user first:

```bash
conda activate lerobot
HF_USER=${YOUR_HF_NAME}
echo $HF_USER
```

Then start recording:

```bash
lerobot-record \
  --robot.type=so101_follower \
  --robot.port=/dev/ttyACM1 \ # <- paste here the port found at previous step
  --robot.id=my_awesome_follower_arm \
  --robot.cameras="{ front: {type: opencv, index_or_path: 0, width: 640, height: 480, fps: 30}, { up: {type: opencv, index_or_path: 0, width: 640, height: 480, fps: 30}}" \ # <- paste here the camera information found at previous step
  --teleop.type=so101_leader \
  --teleop.port=/dev/ttyACM0 \ # <- paste here the port found at previous step 
  --teleop.id=my_awesome_leader_arm \
  --display_data=true \
  --dataset.repo_id=${HF_USER}/IL_Test \ # <- paste here your hugging face repo id 
  --dataset.num_episodes=20 \
  --dataset.single_task="Pick and Place" \
  --dataset.streaming_encoding=true \
  --dataset.encoder_threads=2
```

## Key parameter explanation

| Parameter                       | Description                                                     |
| ------------------------------- | --------------------------------------------------------------- |
| `--robot.type`                  | Specifies the robot type to be used (`so101_follower`)          |
| `--robot.port`                  | Serial port of the Follower robot                               |
| `--robot.id`                    | Unique ID assigned to the robot                                 |
| `--robot.cameras`               | Camera configuration (name, type, resolution, FPS)              |
| `--teleop.type` / `port` / `id` | Configuration of the Leader arm for teleoperation               |
| `--display_data`                | Enables data visualization during recording                     |
| `--dataset.repo_id`             | Name / path of the Hugging Face dataset repository              |
| `--dataset.single_task`         | Description of the task being performed                         |
| `--dataset.num_episodes`        | Number of episodes to record                                    |
| `--dataset.streaming_encoding`  | Enables video encoding during recording                         |
| `--dataset.encoder_threads`     | Number of threads used for video encoding                       |

## Starting the recording

Control the data recording flow using keyboard shortcuts:

- **Right Arrow (→)** or **`n`** — Early‑stop the current episode or reset time and move to the next.
- **Left Arrow (←)** or **`r`** — Cancel the current episode and re‑record it.
- **Escape (ESC)** or **`q`** — Immediately stop the session, encode videos, and upload the dataset.

### Recording start log

- A red *"Recording episode 0"* message appears at the bottom of the terminal, indicating that recording has started.
- Robot configuration information such as `calibration_dir`, camera settings, and port is displayed in the terminal.
- Check the logs to confirm successful connections to the OpenCV cameras and Leader / Follower arms.
- With `display_data=true`, the camera feeds are displayed in real time on the right side.

## Reset episode

- The terminal displays the *"Reset the environment"* message.
- During this period, reposition the object to its initial position and prepare for the next episode.
- After the configured `reset_time_s` has elapsed, recording automatically starts for the next episode.
- You can also press a key to immediately start the next episode.

## Completing the dataset

- The terminal displays *"Stop recording"*, indicating that data collection has finished.
- The cameras and robot are then disconnected sequentially.
- MP4 video post‑processing (moving the `moov` atom) is performed automatically.
- Progress bars for *"Processing Files"* and *"New Data Upload"* are displayed.
- The recorded dataset is automatically uploaded to Hugging Face.
- After the upload is complete, *"Exiting"* is displayed and the program terminates.

## Resume collecting a dataset

```bash
lerobot-record \
    --robot.type=so101_follower \
    --robot.port=/dev/ttyACM1 \ # <- paste here the port found at previous step
    --robot.id=my_awesome_follower_arm \
    --robot.cameras="{front: {type: opencv, index_or_path: 0, width: 640, height: 480, fps: 30}, {up: {type: opencv, index_or_path: 0, width: 640, height: 480, fps: 30}}" \ # <- paste here the camera information found at previous step
    --teleop.type=so101_leader \
    --teleop.port=/dev/ttyACM0 \ # <- paste here the port found at previous step
    --teleop.id=my_awesome_leader_arm \
    --display_data=true \
    --dataset.repo_id=${HF_USER}/IL_Test-20260915_104447 \  # <- paste here your hugging face repo id
    --dataset.root="/home/pai01/.cache/huggingface/lerobot/Thach12/IL_Test-20260915_104447" \ # <- paste here your hugging face root path
    --dataset.num_episodes=10 \
    --dataset.single_task="Pick and Place" \
    --dataset.streaming_encoding=true \
    --dataset.encoder_threads=2 \
    --resume=true
```

- If an issue occurs or you want to record **additional** episodes in the same dataset, resume by re‑running the same command with `--resume=true`.
- When resuming a recording, `--dataset.num_episodes` must be set to the **number of additional episodes** to be recorded.
- Make sure that you also set `--dataset.root="local_path"` — it's a local path to save the new part of the dataset and is required to resume.

---

Previous: [← 6. Problem Definition](06-problem-definition.md) · Next: [8. Dataset Analysis →](08-dataset-analysis.md)
