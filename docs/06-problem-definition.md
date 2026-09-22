# 6. Problem Definition

## Problem Definition

We want the robot to **learn how to perform a manipulation task from human demonstrations** instead of manually programming every robot movement.

> Example: *"Pick up the toy and place it into the cup."*

## Solution: Imitation Learning

- **Imitation Learning (IL):** a method where the robot learns to reproduce behaviors from human demonstrations.
- The overall pipeline consists of three main stages:
  1. **Data Collection** — Demonstrate the task through teleoperation and record Observation–Action pairs.
  2. **Model Training** — Train the model to learn the relationship between Observation → Action from the collected data.
  3. **Policy Execution** — The trained policy takes an Observation as input, predicts an Action, and controls the robot.
- LeRobot provides tools for data collection, dataset management, model training, and policy deployment.

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

## Core Concepts

### Task

- The **goal** the robot is expected to accomplish.
- Defines what the robot needs to do, e.g. *"Pick up the toy and place it into the cup."*
- One task can contain **multiple episodes** for collecting different demonstrations.

### Episode

- One complete execution of a task, from the starting point to the completion condition.
- Each episode contains a sequence of Observations and Actions.
- **One episode = one complete demonstration.**

```
Task
"Pick up the toy and place it into the cup"
        ↓
   Multiple Episodes
        ↓
Episode 1:
Observation → Action → Observation → Action → ... → Completion
Episode 2:
Observation → Action → Observation → Action → ... → Completion
```

### Observation

- Information collected by the robot to understand its current state and environment.
- `observation.state` — the Follower robot's current joint‑state vector (6‑DOF).
- `observation.images` — RGB images captured by the camera, providing visual information.

### Action

- Control signals or commands sent to the robot to execute movement.
- `action` — target joint‑position vector for the robot joints (6‑DOF continuous joint angles).
- Defines the specific angular values (degrees or radians) that each of the 6 motors/joints should rotate to in the next step.

### Dataset fields

| Field                        | Type          | Description                                   |
| ---------------------------- | ------------- | --------------------------------------------- |
| `action`                     | `List[float32]` | Leader state vector                          |
| `observation.state`          | `List[float32]` | Follower state vector                        |
| `observation.images.camera`  | `Image`       | RGB image captured by the first camera        |

---

Previous: [← 5. Hugging Face](05-hugging-face.md) · Next: [7. Dataset Record →](07-dataset-record.md)
