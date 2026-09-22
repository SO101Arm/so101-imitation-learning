# 9. Training

## Training command

```bash
lerobot-train \
  --dataset.repo_id=${HF_USER}/IL_Test-20260915_104447 \ # <- paste here your hugging face repo id for dataset
  --policy.type=act \
  --output_dir=outputs/train/act_IL_Test_20260915_104447 \ # <- paste here the destination you want to save your data set in
  --job_name=act_so101_test \
  --policy.device=cuda \
  --wandb.enable=false \
  --policy.repo_id=${HF_USER}/act_IL_Test_20260915_104447 \ # <- paste here your hugging face repo id for policy
  --save_checkpoint_to_hub=true \
  --steps=300
```

## Explanation

- **`record-test`** — the name of the Hugging Face dataset used for training. `record` indicates the recorded dataset, while `test` indicates the dataset name.
- **`act_so101_test`** — the name of the training job and output folder. It can be used to identify the training experiment.
- **`my_policy`** — the name of the Hugging Face repository where the trained policy is saved / uploaded.
- **`--steps=300`** — specifies the number of training steps. For example, `300` means the model is trained for 300 steps.
- These names are user‑defined and can be changed to match your project or experiment.
- **`--save_checkpoint_to_hub=true`** — enables saving / pushing training checkpoints to the Hugging Face Hub, allowing training to be resumed from the Hub later.

## Training process

- Once launched, LeRobot loads the dataset, initializes the ACT policy, and begins iterating.
- Progress (step, loss, throughput) is printed to the terminal each iteration.
- Checkpoints are written under `output_dir/checkpoints/` and, with `--save_checkpoint_to_hub=true`, mirrored to the Hub repo defined by `--policy.repo_id`.

## Training finish

When the configured number of steps completes, LeRobot writes the final checkpoint under `outputs/train/<job>/checkpoints/last/pretrained_model/` and pushes it to the Hub (if enabled). This is the checkpoint you point [rollout](10-rollout.md) at.

## Resume training from a local dataset

```bash
lerobot-train \
  --config_path=outputs/train/act_IL_Test_20260915_104447/checkpoints/last/pretrained_model/train_config.json \ # <- paste here your hugging face repo id for policy
  --resume=true
```

- `--resume=true` resumes training from the latest checkpoint. The optimizer, scheduler, step counter, and data order are restored automatically.
- `--config_path` specifies the path to the training configuration. It can be a local path to a configuration file or training output directory, or a Hugging Face Hub repository ID when resuming from a model saved on the Hub.

## Resume training from a Hugging Face dataset

```bash
lerobot-train \
  --config_path=${HF_USER}/act_IL_Test_20260915_104447 \ paste here your hugging face repo id for dataset
  --resume=true
```

---

Previous: [← 8. Dataset Analysis](08-dataset-analysis.md) · Next: [10. Rollout →](10-rollout.md)
