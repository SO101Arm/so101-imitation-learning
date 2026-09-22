# 8. Dataset Analysis

Once recording finishes, the dataset lives in two places:

- **On your local PC**, the dataset is stored at:

  ```
  ~/.cache/huggingface/lerobot/{repo-id}
  ```

- **On the Hugging Face Hub**, the dataset is uploaded to:

  ```
  ${HF_USER}/{repo-id}
  ```

## Analyze your dataset on Hugging Face

Open the dataset page on your Hugging Face profile:

```
https://huggingface.co/datasets/${HF_USER}/{repo-id}
```

There you can inspect:

- **Episodes** — the list of recorded episodes with previews of the camera streams.
- **Observation / Action tensors** — joint states and target joint positions per frame.
- **Metadata** — task description, number of episodes, FPS, camera resolution, etc.

Use this analysis view to spot bad episodes (jittery motion, mis‑framed objects, aborted trials) before you spend GPU hours training on them.

---

Previous: [← 7. Dataset Record](07-dataset-record.md) · Next: [9. Training →](09-training.md)
