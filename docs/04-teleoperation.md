# 4. Teleoperation

Run teleoperation between the Leader and Follower arms — the Follower will mirror the Leader in real time, and the specified cameras will stream a preview window.

```bash
lerobot-teleoperate \
    --robot.type=so101_follower \
    --robot.port=/dev/ttyACM1 \ # <- paste here the port found at previous step
    --robot.id=my_awesome_follower_arm \
    --robot.cameras="{front: {type: opencv, index_or_path: 0, width: 640, height: 480, fps: 30}, {up: {type: opencv, index_or_path: 2, width: 640, height: 480, fps: 30}}" \
    --teleop.type=so101_leader \
    --teleop.port=/dev/ttyACM0 \
    --teleop.id=my_awesome_leader_arm \
    --display_data=true
```

Notes:

- `--display_data=true` enables live visualization of the camera feeds during teleoperation.
- Make sure the ports and IDs match what you set during [calibration](03-so101-setup.md).
- Update `index_or_path` for each camera to whatever `lerobot-find-cameras opencv` reported.

---

Previous: [← 3. SO‑101 Setup](03-so101-setup.md) · Next: [5. Hugging Face →](05-hugging-face.md)
