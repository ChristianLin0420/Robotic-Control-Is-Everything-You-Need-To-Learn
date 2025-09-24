# Day 3: Dynamics & Simulation Fidelity

## 🎯 Learning Objectives
- Implement basic robot dynamics models
- Understand the sim-to-real gap problem
- Learn residual dynamics modeling with MLPs
- Compare simulation vs. learned dynamics

## 📚 Background
Real robots don't behave exactly like simulations. Today we'll implement a simple dynamics model and then use machine learning to learn the "residual" - the difference between simulation and reality.

## 🛠️ Coding Task

### Setup
```
Day03-Dynamics-Simulation/
├── dynamics/
│   ├── __init__.py
│   ├── euler_dynamics.py    # Simple Euler integration
│   ├── lagrangian_dynamics.py
│   └── residual_mlp.py      # Learn sim-real gap
├── data/
│   ├── collect_rollouts.py  # Gather sim data
│   └── process_data.py
├── training/
│   ├── train_residual.py
│   └── evaluate_dynamics.py
├── demos/
│   └── dynamics_comparison.py
└── requirements.txt
```

### Implementation Requirements

1. **Simple Dynamics Model** (`dynamics/euler_dynamics.py`):
   - Euler integration for joint states
   - Basic gravity compensation
   - Coriolis and centrifugal terms (simplified)
   - Mass matrix approximation

2. **Residual MLP** (`dynamics/residual_mlp.py`):
   - Small neural network to learn Δ-state
   - Input: (state, action)
   - Output: residual correction
   - Train on sim data first

3. **Data Collection** (`data/collect_rollouts.py`):
   - Generate diverse trajectories
   - Record (state, action, next_state) tuples
   - Both from simulation and learned model

4. **Comparison Tools** (`demos/dynamics_comparison.py`):
   - Visualize trajectory differences
   - Compute prediction errors
   - Show sim vs. learned dynamics

### Key Features to Implement

- **Euler Integration**: Simple but effective dynamics
- **Residual Learning**: MLP to correct simulation errors
- **Data Pipeline**: Efficient rollout collection
- **Evaluation Metrics**: MSE, trajectory deviation
- **Visualization**: Side-by-side comparisons

## 🎮 Demo Task
Create a demo that:
1. Implements simple dynamics for a 2-link arm
2. Collects 1000 rollouts from simulation
3. Trains a small MLP to learn residual dynamics
4. Compares trajectories: sim vs. learned vs. ground truth
5. Shows the learned residual corrections

## 📊 Success Criteria
- [ ] Simple dynamics model runs stably
- [ ] Residual MLP converges during training
- [ ] Learned dynamics are more accurate than simple model
- [ ] Visualization clearly shows improvements
- [ ] Code is modular and well-documented

## 🔧 Dependencies
```bash
pip install torch torchvision
pip install numpy scipy matplotlib
pip install robosuite  # For ground truth data
```

## 📝 Mathematical Background

### Simple Dynamics (Euler Integration)
```
q_{t+1} = q_t + q̇_t * dt
q̇_{t+1} = q̇_t + M⁻¹(τ - C(q,q̇)q̇ - G(q)) * dt
```

### Residual Learning
```
Δs = f_MLP(s_t, a_t)
s_{t+1} = s_{t+1}^{sim} + Δs
```

Where:
- s_t is the state vector
- a_t is the action
- f_MLP is a small neural network
- Δs is the learned residual correction

## 📝 Deliverables
- Complete dynamics modeling library
- Trained residual MLP
- Comparison visualizations
- Performance metrics
- Brief report on sim-real gap reduction

## 🚀 Next Steps
Tomorrow we'll implement PID control that actually works with auto-tuning!
