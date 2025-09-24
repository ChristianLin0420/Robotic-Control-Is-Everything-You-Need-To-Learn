# 30-Day Robotics Control Coding Challenge

A comprehensive, code-first robotics control challenge that progresses from classical control fundamentals to cutting-edge visuomotor and vision-language-action (VLA) methods. Every day includes hands-on coding tasks using common, free toolchains.

## 🎯 Overview

This challenge is designed to take you from basic robotics control concepts to state-of-the-art methods in 30 days. Each day builds upon previous knowledge and includes practical coding tasks that you can run and experiment with.

### Learning Progression
- **Week 1**: Mechanics & Classical Control (Days 1-7)
- **Week 2**: Continuous-control RL (Days 8-14) 
- **Week 3**: Imitation & Offline Learning (Days 15-21)
- **Week 4**: Advanced Methods (Days 22-30)

## 🛠️ Tech Stack

- **Core**: Python 3.8+, PyTorch
- **Simulators**: robosuite, Meta-World, ManiSkill2, dm_control
- **Datasets**: BridgeData V2, CALVIN, D4RL
- **Logging**: Weights & Biases, TensorBoard
- **Environment Management**: Poetry/conda

## 📁 Project Structure

```
30-Day-Robotics-Control-Challenge/
├── README.md                           # This file
├── Day01-Sim-Lab-Boot/                 # Week 1: Mechanics & Classical Control
├── Day02-Kinematics-Pack/
├── Day03-Dynamics-Simulation/
├── Day04-PID-Control/
├── Day05-LQR-iLQR/
├── Day06-Sampling-MPC/
├── Day07-Safety-CBF/
├── Day08-RL-Harness/                   # Week 2: Continuous-control RL
├── Day09-SAC-Baseline/
├── Day10-TD3-Exploration/
├── Day11-PPO-Done-Right/
├── Day12-Domain-Randomization/
├── Day13-Residual-RL/
├── Day14-System-ID-Sim2Sim/
├── Day15-Behavior-Cloning/             # Week 3: Imitation & Offline
├── Day16-DAgger/
├── Day17-Offline-RL-IQL/
├── Day18-Offline-RL-CQL/
├── Day19-Goal-Conditioned-BC/
├── Day20-Language-Conditioned-IL/
├── Day21-Hierarchical-Skills/
├── Day22-Diffusion-Policy/             # Week 4: Advanced Methods
├── Day23-Decision-Transformers/
├── Day24-VLA-Fine-tuning/
├── Day25-OpenPI-Training/
├── Day26-Diffusion-Navigation/
├── Day27-Model-Based-RL/
├── Day28-Multi-Env-Generalization/
├── Day29-Safety-Reliability/
└── Day30-Capstone-Pick-Place/
```

## 🚀 Getting Started

### Prerequisites
- Python 3.8+
- CUDA-capable GPU (recommended)
- 16GB+ RAM
- 50GB+ free disk space

### Setup
1. Clone this repository
2. Set up your environment:
   ```bash
   # Using conda
   conda create -n robotics-control python=3.8
   conda activate robotics-control
   
   # Or using poetry
   poetry install
   ```

3. Install core dependencies:
   ```bash
   pip install torch torchvision torchaudio
   pip install gymnasium robosuite metaworld mani-skill2 dm_control
   pip install wandb tensorboard
   ```

### Daily Workflow
Each day follows this structure:
1. Read the day's README for context and learning objectives
2. Implement the coding task
3. Run experiments and collect metrics
4. Generate plots and videos
5. Write a brief report

## 📊 Daily Deliverables

Every day should produce:
- **Code**: `envs/`, `algos/`, `train.py`, `eval.py`, `configs/*.yaml`, `scripts/run_*.sh`
- **Metrics**: Success rate, return, episode length, constraint violations, FPS
- **Artifacts**: Top-k checkpoints, 3 rollout videos
- **Report**: Brief markdown with plots and 3 key insights

## 🎓 Learning Objectives

By the end of this challenge, you will have:

1. **Classical Control Mastery**: PID, LQR, MPC, CBF
2. **RL Fundamentals**: SAC, TD3, PPO, domain randomization
3. **Imitation Learning**: BC, DAgger, offline RL (IQL, CQL)
4. **Advanced Methods**: Diffusion policies, transformers, VLA models
5. **Real-world Skills**: Sim-to-real transfer, safety, robustness

## 📚 Key Resources

- [BridgeData V2](https://rail-berkeley.github.io/bridgedata/) - Goal/language-conditioned manipulation
- [CALVIN](https://github.com/mees/calvin) - Long-horizon, language-conditioned benchmark
- [OpenVLA](https://openvla.github.io/) - 7B VLA model
- [Diffusion Policy](https://github.com/real-stanford/diffusion_policy) - Action-diffusion visuomotor control
- [OpenPI](https://github.com/OpenPI-Team/OpenPI) - Foundation model training

## 🤝 Contributing

This is a learning challenge! Feel free to:
- Share your implementations
- Report issues or improvements
- Add additional resources or examples
- Create visualizations and demos

## 📝 License

This project is for educational purposes. Please respect the licenses of individual datasets and models used.

## 🏆 Capstone Project

The final day (Day 30) culminates in a complete pick-and-place system with language goals:
- **Input**: "place the red cube into the bowl"
- **Pipeline**: Camera → Encoder(s) → Policy → Controller → Environment
- **Deliverables**: Reproducible scripts, metrics dashboard, videos, ablations

---

**Ready to start?** Begin with [Day 1: Sim Lab Boot](./Day01-Sim-Lab-Boot/) and work your way through the challenge!

*Happy coding! 🤖*