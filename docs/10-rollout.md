# 10. Rollout

## Rollout your trained policy

```bash
lerobot-rollout \
  --strategy.type=base \
  --policy.path=${HF_USER}/act_IL_Test_20260915_104447 \ # <- paste here your hugging face repo id for policy
  --robot.type=so100_follower \
  --robot.port=/dev/ttyACM1 \ # <- paste here the port found at previous step
  --robot.cameras="{ front: {type: opencv, index_or_path: 0, width: 640, height: 480, fps: 30}, { up: {type: opencv, index_or_path: 0, width: 640, height: 480, fps: 30}}" \ # <- paste here the camera information found at previous step
  --task="Pick and Place" \
  --duration=60
```

## Explanation

- **`lerobot-rollout`** — executes the trained policy in the environment to observe how the robot performs the learned task.
- **`--policy.path=${HF_USER}/my_policy`** — specifies the path to the trained policy that will be loaded for the rollout.
- **`--task`** — the natural‑language description of the task, matching what you recorded the dataset under.
- **`--duration=60`** — how long, in seconds, the rollout should run.

During rollout the Follower arm is driven by the policy's predicted actions; the Leader arm is not needed.

---

Previous: [← 9. Training](09-training.md) · Next: [11. Troubleshooting →](11-troubleshooting.md)
