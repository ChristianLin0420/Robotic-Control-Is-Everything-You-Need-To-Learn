# Day 6: Sampling MPC (CEM/MPPI)

## 🎯 Learning Objectives
- Implement Model Predictive Path Integral (MPPI) control
- Understand sampling-based MPC methods
- Compare MPPI with iLQR performance
- Apply to challenging control tasks like cart-pole swing-up

## 📚 Background
Sampling-based MPC methods like MPPI are powerful for handling nonlinear dynamics and constraints. They work by sampling many trajectories and selecting the best one, making them robust to model uncertainty.

## 🛠️ Coding Task

### Setup
```
Day06-Sampling-MPC/
├── mpc/
│   ├── __init__.py
│   ├── mppi.py             # Model Predictive Path Integral
│   ├── cem.py              # Cross-Entropy Method
│   └── trajectory_sampler.py
├── systems/
│   ├── __init__.py
│   ├── cartpole.py         # Cart-pole dynamics
│   └── double_pendulum.py  # Double pendulum
├── demos/
│   ├── cartpole_swingup.py
│   ├── mppi_vs_ilqr.py
│   └── robustness_test.py
├── utils/
│   ├── plotting.py
│   └── performance_metrics.py
└── requirements.txt
```

### Implementation Requirements

1. **MPPI Controller** (`mpc/mppi.py`):
   - Trajectory sampling with noise
   - Cost evaluation for each sample
   - Weighted control update
   - Temperature parameter tuning

2. **CEM Algorithm** (`mpc/cem.py`):
   - Iterative distribution updates
   - Elite sample selection
   - Gaussian distribution fitting
   - Convergence criteria

3. **Cart-pole System** (`systems/cartpole.py`):
   - Nonlinear dynamics
   - Swing-up task definition
   - State constraints (cart limits)
   - Cost function design

4. **Performance Comparison** (`demos/mppi_vs_ilqr.py`):
   - Side-by-side comparison
   - Success rate analysis
   - Computational cost measurement
   - Robustness to disturbances

### Key Features to Implement

- **Trajectory Sampling**: Generate diverse control sequences
- **Cost Weighting**: Softmax-based sample selection
- **Control Smoothing**: Penalize high-frequency control
- **Constraint Handling**: Soft constraints via cost penalties
- **Real-time Performance**: Optimize for control frequency

## 🎮 Demo Task
Create a comprehensive demo that:
1. Implements cart-pole swing-up task
2. Compares MPPI vs iLQR on:
   - Success rate (100 episodes)
   - Average time to swing-up
   - Computational cost per iteration
   - Robustness to parameter variations
3. Visualizes:
   - Sample trajectories (MPPI)
   - Optimal trajectory (iLQR)
   - Control effort comparison
   - Success rate over episodes

## 📊 Success Criteria
- [ ] MPPI successfully swings up cart-pole
- [ ] iLQR also works for comparison
- [ ] MPPI is more robust to disturbances
- [ ] Computational costs are measured
- [ ] Clear performance comparison plots

## 🔧 Dependencies
```bash
pip install numpy scipy matplotlib
pip install gymnasium  # For cart-pole environment
pip install control
```

## 📝 Mathematical Background

### MPPI Algorithm
1. **Sample**: u_t^(i) ~ N(u_t, Σ) for i=1...K
2. **Rollout**: x_t^(i) = f(x_{t-1}^(i), u_t^(i))
3. **Cost**: S^(i) = ∑_{t=0}^T c(x_t^(i), u_t^(i))
4. **Weight**: w^(i) = exp(-S^(i)/λ) / ∑_j exp(-S^(j)/λ)
5. **Update**: u_t = ∑_i w^(i) u_t^(i)

### Key Parameters
- **K**: Number of samples per timestep
- **T**: Horizon length
- **λ**: Temperature (exploration vs exploitation)
- **Σ**: Control noise covariance

## 📝 Deliverables
- Complete MPPI implementation
- Cart-pole swing-up demo
- MPPI vs iLQR comparison
- Performance analysis report
- Robustness testing results

## 🚀 Next Steps
Tomorrow we'll add safety constraints with Control Barrier Functions!
