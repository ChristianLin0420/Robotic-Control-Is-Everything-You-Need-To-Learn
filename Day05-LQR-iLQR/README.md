# Day 5: LQR/iLQR

## 🎯 Learning Objectives
- Implement Linear Quadratic Regulator (LQR)
- Build iterative LQR (iLQR) for nonlinear systems
- Understand optimal control theory
- Apply to via-point trajectory planning

## 📚 Background
LQR provides optimal control for linear systems, while iLQR extends this to nonlinear systems through iterative linearization. These are fundamental tools for trajectory optimization and control.

## 🛠️ Coding Task

### Setup
```
Day05-LQR-iLQR/
├── optimal_control/
│   ├── __init__.py
│   ├── lqr.py              # Linear Quadratic Regulator
│   ├── ilqr.py             # Iterative LQR
│   └── trajectory_utils.py
├── systems/
│   ├── __init__.py
│   ├── pendulum.py         # Linear pendulum system
│   └── planar_arm.py       # 2-link planar arm
├── demos/
│   ├── pendulum_swingup.py
│   ├── arm_viapoints.py
│   └── cost_visualization.py
├── utils/
│   ├── plotting.py
│   └── animation.py
└── requirements.txt
```

### Implementation Requirements

1. **LQR Controller** (`optimal_control/lqr.py`):
   - Riccati equation solver
   - Infinite horizon LQR
   - Finite horizon LQR
   - Cost function evaluation

2. **iLQR Algorithm** (`optimal_control/ilqr.py`):
   - Forward pass (rollout)
   - Backward pass (value function)
   - Line search for step size
   - Convergence checking

3. **System Models** (`systems/`):
   - Linear pendulum dynamics
   - 2-link planar arm dynamics
   - Jacobian computation for iLQR

4. **Via-point Planning** (`demos/arm_viapoints.py`):
   - Define via-points in workspace
   - Convert to joint space via IK
   - Plan smooth trajectory with iLQR
   - Visualize optimal control sequence

### Key Features to Implement

- **Riccati Solver**: Solve discrete-time Riccati equation
- **iLQR Backward Pass**: Compute optimal control gains
- **Line Search**: Ensure cost decrease at each iteration
- **Trajectory Smoothing**: Penalize high accelerations
- **Visualization**: Show control evolution and cost reduction

## 🎮 Demo Task
Create two demos:

### Demo 1: Pendulum Swing-up
1. Linearize pendulum around upright position
2. Use LQR to stabilize at top
3. Show phase portrait and control effort
4. Compare with PID performance

### Demo 2: 2-Link Arm Via-points
1. Define 3-4 via-points in workspace
2. Use iLQR to plan smooth trajectory
3. Visualize:
   - Arm configuration sequence
   - Control torques over time
   - Cost reduction per iteration
4. Compare with straight-line interpolation

## 📊 Success Criteria
- [ ] LQR stabilizes linear pendulum
- [ ] iLQR converges for arm planning
- [ ] Via-point trajectories are smooth
- [ ] Cost decreases monotonically
- [ ] Visualizations are clear and informative

## 🔧 Dependencies
```bash
pip install numpy scipy matplotlib
pip install control  # For Riccati equation solving
pip install spatialmath-python
```

## 📝 Mathematical Background

### LQR Problem
Minimize: J = ∑(xᵀQx + uᵀRu) + xₜᵀQₜxₜ
Subject to: x_{t+1} = Ax_t + Bu_t

Solution: u_t = -K_t x_t
Where: K_t = (R + BᵀP_{t+1}B)⁻¹BᵀP_{t+1}A

### iLQR Algorithm
1. **Forward Pass**: Rollout with current policy
2. **Backward Pass**: 
   - Q_xx, Q_uu, Q_ux = second derivatives
   - k = -Q_uu⁻¹Q_u (feedforward)
   - K = -Q_uu⁻¹Q_ux (feedback)
3. **Line Search**: Find α that decreases cost
4. **Update**: u_new = u + αk + K(x - x_nom)

## 📝 Deliverables
- Complete LQR/iLQR implementation
- Pendulum swing-up demo
- Arm via-point planning demo
- Cost reduction visualizations
- Performance comparison report

## 🚀 Next Steps
Tomorrow we'll implement sampling-based MPC with CEM and MPPI!
