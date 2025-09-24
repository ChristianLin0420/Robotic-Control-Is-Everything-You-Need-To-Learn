# Day 17: Offline RL - IQL

## 🎯 Learning Objectives
- Implement Implicit Q-Learning (IQL) algorithm
- Understand offline RL challenges
- Train on D4RL/robomimic datasets
- Compare IQL with BC performance

## 📚 Background
Offline RL learns from fixed datasets without environment interaction. IQL is a simple but effective method that avoids the distribution shift problems of other offline RL algorithms.

## 🛠️ Coding Task

### Setup
```
Day17-Offline-RL-IQL/
├── offline_rl/
│   ├── __init__.py
│   ├── iql.py              # IQL implementation
│   ├── value_network.py    # Value function learning
│   └── policy_network.py   # Policy extraction
├── datasets/
│   ├── __init__.py
│   ├── d4rl_loader.py      # D4RL dataset loading
│   ├── robomimic_loader.py # Robomimic dataset loading
│   └── data_preprocessing.py
├── training/
│   ├── train_iql.py
│   ├── compare_methods.py
│   └── offline_evaluation.py
├── demos/
│   ├── iql_demo.py
│   ├── dataset_analysis.py
│   └── performance_comparison.py
├── configs/
│   └── iql_config.yaml
└── requirements.txt
```

### Implementation Requirements

1. **IQL Algorithm** (`offline_rl/iql.py`):
   - Value function learning
   - Advantage-weighted policy extraction
   - Conservative Q-learning
   - Offline evaluation

2. **Value Network** (`offline_rl/value_network.py`):
   - State value function V(s)
   - Advantage estimation A(s,a)
   - Target network updates
   - Loss function implementation

3. **Policy Network** (`offline_rl/policy_network.py`):
   - Advantage-weighted policy
   - Action sampling
   - Log probability computation
   - Policy evaluation

4. **Dataset Loading** (`datasets/`):
   - D4RL dataset integration
   - Robomimic dataset support
   - Data preprocessing and filtering
   - Train/validation splits

### Key Features to Implement

- **Value Learning**: Learn V(s) from offline data
- **Advantage Estimation**: A(s,a) = Q(s,a) - V(s)
- **Policy Extraction**: Advantage-weighted policy
- **Conservative Learning**: Avoid overestimation
- **Offline Evaluation**: No environment interaction

## 🎮 Demo Task
Train IQL on offline datasets and compare with BC:

### Dataset 1: D4RL Hopper
- Environment: Hopper-v2
- Dataset: hopper-medium-v2
- Evaluation: 100 episodes

### Dataset 2: Robomimic Can
- Environment: Robosuite Can-v0
- Dataset: robomimic-can-v0
- Evaluation: 100 episodes

### Training Protocol
1. Load offline dataset
2. Train value function V(s)
3. Extract advantage-weighted policy
4. Evaluate on test episodes
5. Compare with BC baseline

### Analysis
- Learning curves (value loss, policy loss)
- Success rate comparison
- Trajectory quality analysis
- Dataset utilization efficiency

## 📊 Success Criteria
- [ ] IQL implementation is correct
- [ ] Value function converges
- [ ] Policy extraction works
- [ ] IQL outperforms BC on both datasets
- [ ] Offline evaluation is stable

## 🔧 Dependencies
```bash
pip install torch torchvision
pip install d4rl
pip install robomimic
pip install wandb tensorboard
pip install matplotlib seaborn
pip install numpy scipy
```

## 📝 Mathematical Background

### IQL Value Learning
Learn V(s) by minimizing:
```
L_V = E[(V(s) - max_a Q(s,a))²]
```

Where Q(s,a) is estimated from the dataset.

### Advantage Estimation
```
A(s,a) = Q(s,a) - V(s)
```

### Policy Extraction
```
π(a|s) ∝ exp(A(s,a)/τ)
```

Where τ is a temperature parameter.

### Conservative Q-Learning
```
L_Q = E[(Q(s,a) - (r + γV(s'))²] + λ E[Q(s,a)²]
```

Where λ is the conservative coefficient.

## 📝 Deliverables
- Complete IQL implementation
- Dataset loading pipeline
- Offline evaluation framework
- Performance comparison with BC
- Learning curve analysis

## 🚀 Next Steps
Tomorrow we'll implement CQL for more conservative offline RL!
