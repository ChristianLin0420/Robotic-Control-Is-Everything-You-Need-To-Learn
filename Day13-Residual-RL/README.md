# Day 13: Residual RL

## 🎯 Learning Objectives
- Combine classical control with RL
- Implement residual policy learning
- Understand the benefits of structured control
- Ablate residual magnitude constraints

## 📚 Background
Residual RL combines the stability of classical control with the flexibility of RL. The RL policy learns a residual correction on top of a classical controller (e.g., PID), providing both safety and performance.

## 🛠️ Coding Task

### Setup
```
Day13-Residual-RL/
├── residual/
│   ├── __init__.py
│   ├── residual_policy.py   # Residual policy wrapper
│   ├── classical_controller.py  # PID/LQR baseline
│   └── constraint_manager.py    # Residual constraints
├── algorithms/
│   ├── __init__.py
│   ├── residual_sac.py      # SAC with residual learning
│   └── residual_ppo.py      # PPO with residual learning
├── environments/
│   ├── __init__.py
│   ├── residual_env.py      # Environment with residual control
│   └── env_factory.py
├── training/
│   ├── train_residual.py
│   ├── ablation_study.py
│   └── constraint_analysis.py
├── demos/
│   ├── residual_demo.py
│   ├── constraint_comparison.py
│   └── stability_analysis.py
├── configs/
│   └── residual_config.yaml
└── requirements.txt
```

### Implementation Requirements

1. **Residual Policy** (`residual/residual_policy.py`):
   - Combine classical + RL control
   - Residual magnitude constraints
   - Smooth residual transitions
   - Safety fallback mechanisms

2. **Classical Controllers** (`residual/classical_controller.py`):
   - PID controller implementation
   - LQR controller for reference tracking
   - Adaptive gain scheduling
   - Performance monitoring

3. **Residual SAC/PPO** (`algorithms/`):
   - Modified algorithms for residual learning
   - Residual-specific loss functions
   - Constraint-aware exploration
   - Classical controller integration

4. **Constraint Management** (`residual/constraint_manager.py`):
   - Residual magnitude limits
   - Smooth constraint transitions
   - Emergency override mechanisms
   - Constraint violation detection

### Key Features to Implement

- **Structured Control**: Classical + RL combination
- **Residual Constraints**: Limit residual magnitude
- **Smooth Transitions**: Avoid control discontinuities
- **Safety Fallback**: Revert to classical control when needed
- **Ablation Studies**: Compare different constraint levels

## 🎮 Demo Task
Train residual RL on a manipulation task and compare with pure RL:

### Task: Precise Manipulation
- Environment: Robosuite manipulation task
- Classical Controller: PID for joint position control
- RL Policy: Residual torque corrections
- Constraints: |residual| < 0.1 * |classical|

### Ablation Study
Train policies with different residual constraints:
1. **No Constraints**: Pure RL (baseline)
2. **Small Residual**: |residual| < 0.05 * |classical|
3. **Medium Residual**: |residual| < 0.1 * |classical|
4. **Large Residual**: |residual| < 0.2 * |classical|

### Evaluation
- Success rate on manipulation task
- Control smoothness (torque variance)
- Stability under disturbances
- Learning speed comparison

## 📊 Success Criteria
- [ ] Residual RL outperforms pure RL
- [ ] Constrained residuals maintain performance
- [ ] Control is smoother than pure RL
- [ ] System is more stable under disturbances
- [ ] Clear ablation study results

## 🔧 Dependencies
```bash
pip install torch torchvision
pip install robosuite
pip install control  # For classical controllers
pip install wandb tensorboard
pip install matplotlib seaborn
```

## 📝 Mathematical Background

### Residual Control
```
u_total = u_classical + u_residual
```

Where:
- u_classical is from PID/LQR
- u_residual is from RL policy
- |u_residual| ≤ α|u_classical| (constraint)

### Residual Policy Learning
The RL policy learns to output residual corrections:
```
u_residual = π_θ(s, u_classical)
```

### Constraint Handling
```
u_residual = clip(u_residual, -α|u_classical|, α|u_classical|)
```

## 📝 Deliverables
- Complete residual RL implementation
- Classical controller integration
- Constraint management system
- Ablation study results
- Stability analysis report

## 🚀 Next Steps
Tomorrow we'll learn system identification and sim-to-sim transfer!
