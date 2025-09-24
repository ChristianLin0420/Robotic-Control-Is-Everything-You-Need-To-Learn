# Day 7: Safety - Control Barrier Functions

## 🎯 Learning Objectives
- Implement Control Barrier Functions (CBF)
- Understand safety-critical control
- Apply CBF to joint limits and workspace constraints
- Integrate safety with existing controllers

## 📚 Background
Safety is paramount in robotics. Control Barrier Functions provide a mathematical framework to guarantee safety by ensuring the system never enters unsafe states. Today we'll implement CBF-based safety constraints.

## 🛠️ Coding Task

### Setup
```
Day07-Safety-CBF/
├── safety/
│   ├── __init__.py
│   ├── cbf.py              # Control Barrier Functions
│   ├── qp_solver.py        # Quadratic Programming solver
│   └── safety_constraints.py
├── constraints/
│   ├── __init__.py
│   ├── joint_limits.py     # Joint angle/velocity limits
│   ├── workspace.py        # Workspace boundaries
│   └── collision.py        # Collision avoidance
├── demos/
│   ├── safe_control.py     # Safe vs unsafe rollouts
│   ├── constraint_testing.py
│   └── emergency_stop.py
├── utils/
│   ├── plotting.py
│   └── safety_metrics.py
└── requirements.txt
```

### Implementation Requirements

1. **CBF Framework** (`safety/cbf.py`):
   - Barrier function definition
   - Safety constraint formulation
   - CBF-QP optimization
   - Multiple constraint handling

2. **QP Solver** (`safety/qp_solver.py`):
   - Quadratic programming with constraints
   - Real-time optimization
   - Infeasibility handling
   - Warm-start capabilities

3. **Safety Constraints** (`constraints/`):
   - Joint angle limits
   - Joint velocity limits
   - Workspace boundaries
   - Collision avoidance (simplified)

4. **Safety Demo** (`demos/safe_control.py`):
   - Compare safe vs unsafe controllers
   - Show constraint violations
   - Demonstrate emergency stopping
   - Visualize safety margins

### Key Features to Implement

- **CBF-QP Formulation**: Minimize control deviation while ensuring safety
- **Multiple Constraints**: Handle joint limits + workspace + collision
- **Real-time Safety**: Fast QP solving for control loop
- **Constraint Visualization**: Show safety boundaries
- **Emergency Handling**: Graceful degradation when unsafe

## 🎮 Demo Task
Create a comprehensive safety demo that:
1. Sets up a 6-DoF arm with safety constraints:
   - Joint angle limits: ±π/2 for each joint
   - Joint velocity limits: ±2 rad/s
   - Workspace boundaries: 0.3m < r < 0.8m
2. Runs two scenarios:
   - **Unsafe**: Controller without CBF (may violate constraints)
   - **Safe**: Controller with CBF (always respects constraints)
3. Visualizes:
   - Arm trajectories in 3D
   - Constraint violations over time
   - Safety margins
   - Control effort comparison

## 📊 Success Criteria
- [ ] CBF-QP solver works in real-time
- [ ] Safe controller never violates constraints
- [ ] Unsafe controller shows violations
- [ ] Safety margins are clearly visualized
- [ ] Performance impact is reasonable

## 🔧 Dependencies
```bash
pip install numpy scipy matplotlib
pip install cvxpy  # For QP solving
pip install robosuite
pip install spatialmath-python
```

## 📝 Mathematical Background

### Control Barrier Function
A function h(x) is a CBF if:
- h(x) ≥ 0 for all safe states
- h(x) < 0 for all unsafe states
- There exists a control u such that: ḣ(x) + α(h(x)) ≥ 0

### CBF-QP Formulation
```
min_u ||u - u_nom||²
s.t.  ḣ(x) + α(h(x)) ≥ 0
      u_min ≤ u ≤ u_max
```

Where:
- u_nom is the nominal control (from MPPI/iLQR)
- α is a class-K function (e.g., α(h) = γh)
- ḣ(x) = ∇h(x) · f(x,u) is the Lie derivative

## 📝 Deliverables
- Complete CBF safety framework
- Safe vs unsafe control demo
- Constraint violation analysis
- Safety margin visualizations
- Performance impact report

## 🚀 Next Steps
Tomorrow we'll start Week 2 with RL fundamentals and build a reusable RL harness!
