# Day 1: Sim Lab Boot

## 🎯 Learning Objectives
- Set up a unified robotics simulation environment
- Create a standardized environment wrapper for multiple simulators
- Implement logging and video recording capabilities
- Establish the foundation for all future experiments

## 📚 Background
Today we'll set up the core infrastructure that will support all 30 days of the challenge. We need a unified interface that works across different simulators (robosuite, Meta-World, ManiSkill2, dm_control) with consistent logging and video recording.

## 🛠️ Coding Task

### Setup
Create a repository with the following structure:
```
Day01-Sim-Lab-Boot/
├── envs/
│   ├── __init__.py
│   ├── base_env.py          # Base environment wrapper
│   ├── robosuite_wrapper.py
│   ├── metaworld_wrapper.py
│   └── maniskill_wrapper.py
├── utils/
│   ├── __init__.py
│   ├── logging.py           # W&B and TensorBoard logging
│   └── video_recorder.py    # Video export utilities
├── configs/
│   └── env_config.yaml
├── train.py
├── eval.py
└── requirements.txt
```

### Implementation Requirements

1. **Unified Environment Wrapper** (`envs/base_env.py`):
   - Standard interface: `reset()`, `step()`, `render()`, `set_seed()`
   - Consistent observation/action space handling
   - Episode recording capabilities

2. **Simulator Wrappers**:
   - `robosuite_wrapper.py`: Wrap robosuite environments
   - `metaworld_wrapper.py`: Wrap Meta-World environments  
   - `maniskill_wrapper.py`: Wrap ManiSkill2 environments

3. **Logging System** (`utils/logging.py`):
   - Weights & Biases integration
   - TensorBoard support
   - Episode metrics tracking

4. **Video Recording** (`utils/video_recorder.py`):
   - Record rollouts as MP4 videos
   - Support multiple camera views
   - Automatic video compression

### Key Features to Implement

- **Environment Factory**: Easy switching between simulators
- **Rollout Recording**: Save episodes as videos and data
- **Metrics Logging**: Track success rate, episode length, rewards
- **Seed Management**: Reproducible experiments
- **Configuration System**: YAML-based config management

## 🎮 Demo Task
Create a simple demo that:
1. Loads a robosuite Panda arm environment
2. Runs 5 random episodes
3. Records videos of each episode
4. Logs metrics to both W&B and TensorBoard
5. Exports a summary report

## 📊 Success Criteria
- [ ] All three simulator wrappers work
- [ ] Videos are recorded and saved correctly
- [ ] Metrics are logged to both W&B and TensorBoard
- [ ] Code is well-documented and modular
- [ ] Demo script runs without errors

## 🔧 Dependencies
```bash
pip install torch torchvision torchaudio
pip install gymnasium robosuite metaworld mani-skill2
pip install wandb tensorboard opencv-python
pip install pyyaml matplotlib seaborn
```

## 📝 Deliverables
- Complete environment wrapper system
- Working demo script
- 3 recorded videos from different simulators
- Logged metrics and plots
- Brief report on what worked/failed

## 🚀 Next Steps
Tomorrow we'll use this foundation to implement forward and inverse kinematics for robotic arms!
