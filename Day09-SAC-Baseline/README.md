# Day 9: SAC Baseline

## 🎯 Learning Objectives
- Implement Soft Actor-Critic (SAC) algorithm
- Understand entropy regularization in RL
- Master action squashing for continuous control
- Train on dm_control environments

## 📚 Background
SAC is one of the most successful off-policy RL algorithms for continuous control. It uses entropy regularization to encourage exploration and learns both a policy and Q-functions simultaneously.

## 🛠️ Coding Task

### Setup
```
Day09-SAC-Baseline/
├── algorithms/
│   ├── __init__.py
│   ├── sac.py              # SAC implementation
│   ├── networks.py         # Policy and Q-network architectures
│   └── losses.py           # SAC loss functions
├── environments/
│   ├── __init__.py
│   ├── dm_control_wrapper.py
│   └── env_factory.py
├── training/
│   ├── train_sac.py
│   ├── evaluate.py
│   └── hyperparameter_tuning.py
├── demos/
│   ├── cheetah_run.py
│   ├── finger_spin.py
│   └── learning_curves.py
├── configs/
│   └── sac_config.yaml
└── requirements.txt
```

### Implementation Requirements

1. **SAC Algorithm** (`algorithms/sac.py`):
   - Soft policy gradient
   - Soft Q-learning updates
   - Automatic entropy tuning
   - Target network updates

2. **Network Architectures** (`algorithms/networks.py`):
   - Gaussian policy network
   - Twin Q-networks
   - Action squashing (tanh)
   - Log probability computation

3. **Loss Functions** (`algorithms/losses.py`):
   - Policy loss with entropy bonus
   - Q-function loss (MSE)
   - Entropy loss for auto-tuning
   - Gradient clipping

4. **dm_control Integration** (`environments/dm_control_wrapper.py`):
   - Wrap dm_control environments
   - Handle observation preprocessing
   - Action space normalization
   - Episode termination logic

### Key Features to Implement

- **Entropy Regularization**: Automatic temperature tuning
- **Twin Q-Networks**: Reduce overestimation bias
- **Action Squashing**: Handle bounded action spaces
- **Target Networks**: Stable learning
- **Gradient Clipping**: Prevent exploding gradients

## 🎮 Demo Task
Train SAC on two dm_control tasks:

### Task 1: Cheetah Run
- Environment: `dm_control.cheetah.run`
- Goal: Maximize forward velocity
- Success: Average velocity > 8 m/s

### Task 2: Finger Spin
- Environment: `dm_control.finger.spin`
- Goal: Keep finger spinning
- Success: Average angular velocity > 5 rad/s

For each task:
1. Train for 1M steps
2. Log learning curves (return, Q-loss, policy loss)
3. Generate evaluation videos
4. Compare with random policy baseline

## 📊 Success Criteria
- [ ] SAC implementation matches paper
- [ ] Cheetah reaches >8 m/s average velocity
- [ ] Finger spin maintains >5 rad/s
- [ ] Learning curves show clear improvement
- [ ] Videos show smooth, stable behavior

## 🔧 Dependencies
```bash
pip install torch torchvision
pip install dm_control
pip install gymnasium
pip install wandb tensorboard
```

## 📝 Mathematical Background

### SAC Objective
```
J(π) = E[∑_{t=0}^T γ^t (r_t + α H(π(·|s_t)))]
```

Where:
- H(π(·|s_t)) is the entropy of the policy
- α is the temperature parameter
- γ is the discount factor

### Policy Loss
```
L_π = E[α log π(a_t|s_t) - Q_θ(s_t, a_t)]
```

### Q-Function Loss
```
L_Q = E[(Q_θ(s_t, a_t) - (r_t + γ Q_θ'(s_{t+1}, a_{t+1}) - α log π(a_{t+1}|s_{t+1})))^2]
```

### Automatic Entropy Tuning
```
L_α = E[-α log π(a_t|s_t) - α H_target]
```

## 📝 Deliverables
- Complete SAC implementation
- Training scripts for both tasks
- Learning curve plots
- Evaluation videos
- Performance comparison report

## 🚀 Next Steps
Tomorrow we'll implement TD3 with exploration techniques!
