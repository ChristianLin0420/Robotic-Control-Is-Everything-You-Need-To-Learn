# Day 14: System ID + Sim2Sim

## 🎯 Learning Objectives
- Implement system identification from rollouts
- Learn to fit mass and friction parameters
- Understand sim-to-sim transfer
- Retrain policies with updated parameters

## 📚 Background
System identification helps bridge the gap between different simulations or between simulation and reality. By learning the true parameters of a system, we can improve policy performance and transfer.

## 🛠️ Coding Task

### Setup
```
Day14-System-ID-Sim2Sim/
├── system_id/
│   ├── __init__.py
│   ├── parameter_estimator.py  # Least squares fitting
│   ├── dynamics_model.py       # Parameterized dynamics
│   └── data_collector.py       # Rollout collection
├── algorithms/
│   ├── __init__.py
│   ├── sac_retrain.py          # Retrain with new params
│   └── transfer_evaluator.py   # Transfer performance
├── environments/
│   ├── __init__.py
│   ├── parameterized_env.py    # Environment with learnable params
│   └── env_factory.py
├── training/
│   ├── collect_data.py
│   ├── fit_parameters.py
│   ├── retrain_policy.py
│   └── transfer_analysis.py
├── demos/
│   ├── system_id_demo.py
│   ├── sim2sim_transfer.py
│   └── parameter_visualization.py
├── configs/
│   └── system_id_config.yaml
└── requirements.txt
```

### Implementation Requirements

1. **Parameter Estimator** (`system_id/parameter_estimator.py`):
   - Least squares fitting
   - Mass and friction estimation
   - Parameter uncertainty quantification
   - Cross-validation for parameter selection

2. **Dynamics Model** (`system_id/dynamics_model.py`):
   - Parameterized robot dynamics
   - Jacobian computation w.r.t. parameters
   - Forward dynamics prediction
   - Parameter sensitivity analysis

3. **Data Collection** (`system_id/data_collector.py`):
   - Diverse trajectory generation
   - State-action-next_state recording
   - Parameter variation during collection
   - Data quality assessment

4. **Transfer Evaluation** (`algorithms/transfer_evaluator.py`):
   - Performance comparison across parameters
   - Transfer success rate
   - Parameter sensitivity analysis
   - Retraining efficiency

### Key Features to Implement

- **Least Squares Fitting**: Estimate parameters from data
- **Parameter Uncertainty**: Quantify estimation confidence
- **Cross-Validation**: Prevent overfitting
- **Retraining Pipeline**: Update policies with new parameters
- **Transfer Analysis**: Measure improvement from system ID

## 🎮 Demo Task
Implement a complete sim-to-sim transfer pipeline:

### Step 1: Data Collection
1. Generate 1000 diverse trajectories
2. Record (state, action, next_state) tuples
3. Vary mass and friction during collection
4. Save data for parameter fitting

### Step 2: System Identification
1. Fit mass and friction parameters using least squares
2. Validate on held-out test data
3. Quantify parameter uncertainty
4. Compare with ground truth parameters

### Step 3: Policy Retraining
1. Train SAC on original environment
2. Update environment with fitted parameters
3. Retrain SAC on updated environment
4. Compare performance on target environment

### Step 4: Transfer Analysis
1. Evaluate both policies on target environment
2. Measure performance improvement
3. Analyze which parameters matter most
4. Generate transfer success report

## 📊 Success Criteria
- [ ] System ID recovers parameters within 10% of ground truth
- [ ] Retrained policy outperforms original
- [ ] Transfer success rate >80%
- [ ] Parameter uncertainty is quantified
- [ ] Clear improvement from sim-to-sim transfer

## 🔧 Dependencies
```bash
pip install torch torchvision
pip install numpy scipy
pip install robosuite
pip install wandb tensorboard
pip install matplotlib seaborn
pip install scikit-learn  # For cross-validation
```

## 📝 Mathematical Background

### System Identification
Given data {(s_t, a_t, s_{t+1})}, find parameters θ that minimize:
```
L(θ) = ∑||s_{t+1} - f_θ(s_t, a_t)||²
```

Where f_θ is the parameterized dynamics model.

### Least Squares Solution
```
θ* = (X^T X)^(-1) X^T y
```

Where:
- X is the feature matrix (state-action pairs)
- y is the target (next states)
- θ* are the estimated parameters

### Parameter Uncertainty
```
Cov(θ) = σ² (X^T X)^(-1)
```

Where σ² is the residual variance.

## 📝 Deliverables
- Complete system identification pipeline
- Parameter estimation tools
- Sim-to-sim transfer framework
- Transfer performance analysis
- Parameter uncertainty quantification

## 🚀 Next Steps
Tomorrow we start Week 3 with imitation learning and behavior cloning!
