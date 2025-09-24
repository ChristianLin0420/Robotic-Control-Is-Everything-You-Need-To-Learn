# Day 16: DAgger

## 🎯 Learning Objectives
- Implement Dataset Aggregation (DAgger) algorithm
- Understand the distribution shift problem in BC
- Build an oracle scripted policy for data collection
- Compare DAgger with BC sample efficiency

## 📚 Background
DAgger addresses the distribution shift problem in behavior cloning by iteratively collecting data from the learned policy and correcting it with expert actions. This leads to much better sample efficiency than pure BC.

## 🛠️ Coding Task

### Setup
```
Day16-DAgger/
├── imitation/
│   ├── __init__.py
│   ├── dagger.py           # DAgger implementation
│   ├── oracle_policy.py    # Scripted expert policy
│   └── data_aggregator.py  # Data collection and aggregation
├── training/
│   ├── train_dagger.py
│   ├── compare_bc_dagger.py
│   └── error_analysis.py
├── demos/
│   ├── dagger_demo.py
│   ├── error_evolution.py
│   └── sample_efficiency.py
├── utils/
│   ├── plotting.py
│   └── metrics.py
├── configs/
│   └── dagger_config.yaml
└── requirements.txt
```

### Implementation Requirements

1. **DAgger Algorithm** (`imitation/dagger.py`):
   - Iterative data collection
   - Expert action correction
   - Policy retraining
   - Convergence criteria

2. **Oracle Policy** (`imitation/oracle_policy.py`):
   - Scripted expert behavior
   - Goal-reaching strategies
   - Error recovery mechanisms
   - Performance monitoring

3. **Data Aggregator** (`imitation/data_aggregator.py`):
   - Rollout collection from learned policy
   - Expert action annotation
   - Dataset management
   - Data quality assessment

4. **Error Analysis** (`training/error_analysis.py`):
   - Track error evolution over iterations
   - Compare BC vs DAgger learning curves
   - Analyze distribution shift
   - Measure sample efficiency

### Key Features to Implement

- **Iterative Learning**: Multiple rounds of data collection
- **Expert Correction**: Oracle provides correct actions
- **Error Tracking**: Monitor policy performance over time
- **Sample Efficiency**: Compare with BC baseline
- **Convergence**: Stop when performance plateaus

## 🎮 Demo Task
Implement DAgger and compare with BC on a manipulation task:

### Task: Pick and Place
- Environment: Robosuite Can-v0
- Oracle Policy: Scripted pick-and-place behavior
- Evaluation: 100 test episodes per iteration

### DAgger Protocol
1. **Initial BC**: Train on 50 expert demonstrations
2. **Iterative Collection**:
   - Collect 20 rollouts with current policy
   - Get expert actions for all states
   - Add to training dataset
   - Retrain policy
3. **Repeat** for 10 iterations or until convergence

### Analysis
- Plot error vs iteration number
- Compare BC vs DAgger success rates
- Measure sample efficiency (success per demo)
- Analyze distribution shift over iterations

## 📊 Success Criteria
- [ ] DAgger implementation is correct
- [ ] Error decreases over iterations
- [ ] DAgger outperforms BC with same data
- [ ] Sample efficiency is clearly better
- [ ] Convergence is achieved within 10 iterations

## 🔧 Dependencies
```bash
pip install torch torchvision
pip install robosuite
pip install wandb tensorboard
pip install matplotlib seaborn
pip install numpy scipy
```

## 📝 Mathematical Background

### DAgger Algorithm
1. **Initialize**: D ← D_expert, π ← BC(D)
2. **For i = 1 to N**:
   - Collect rollouts: τ_i ~ π
   - Get expert actions: a_expert = π*(s) for s ∈ τ_i
   - Aggregate: D ← D ∪ {(s, a_expert)}
   - Retrain: π ← BC(D)

### Distribution Shift
The key insight is that BC minimizes:
```
E_{s~d_expert}[||π(s) - π*(s)||²]
```

But we need to minimize:
```
E_{s~d_π}[||π(s) - π*(s)||²]
```

DAgger addresses this by collecting data from d_π.

### Error Evolution
Track the error over iterations:
```
Error_i = E_{s~d_π_i}[||π_i(s) - π*(s)||²]
```

## 📝 Deliverables
- Complete DAgger implementation
- Oracle policy for data collection
- Error evolution analysis
- Sample efficiency comparison
- Convergence study

## 🚀 Next Steps
Tomorrow we'll implement offline RL with IQL!
