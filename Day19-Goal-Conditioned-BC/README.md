# Day 19: Goal-Conditioned BC

## 🎯 Learning Objectives
- Implement goal-image conditioned policy
- Build contrastive goal encoder
- Understand goal-conditioned learning
- Evaluate under visual distractors

## 📚 Background
Goal-conditioned learning allows policies to achieve different goals without retraining. By conditioning on goal images and using contrastive learning, we can learn robust goal-reaching behaviors.

## 🛠️ Coding Task

### Setup
```
Day19-Goal-Conditioned-BC/
├── goal_conditioned/
│   ├── __init__.py
│   ├── goal_bc.py          # Goal-conditioned BC
│   ├── contrastive_encoder.py  # Contrastive goal encoder
│   └── goal_sampler.py     # Goal sampling strategies
├── data/
│   ├── __init__.py
│   ├── goal_dataset.py     # Goal-conditioned dataset
│   ├── data_augmentation.py
│   └── distractor_generator.py
├── training/
│   ├── train_goal_bc.py
│   ├── contrastive_training.py
│   └── distractor_evaluation.py
├── demos/
│   ├── goal_bc_demo.py
│   ├── distractor_test.py
│   └── goal_reaching.py
├── configs/
│   └── goal_bc_config.yaml
└── requirements.txt
```

### Implementation Requirements

1. **Goal-Conditioned BC** (`goal_conditioned/goal_bc.py`):
   - Goal-image conditioned policy
   - Multi-goal learning
   - Goal sampling strategies
   - Success rate evaluation

2. **Contrastive Encoder** (`goal_conditioned/contrastive_encoder.py`):
   - Contrastive learning for goal encoding
   - Positive/negative pair sampling
   - InfoNCE loss
   - Goal representation learning

3. **Goal Dataset** (`data/goal_dataset.py`):
   - Goal-conditioned demonstration data
   - Goal sampling and pairing
   - Data augmentation for goals
   - Distractor generation

4. **Distractor Evaluation** (`training/distractor_evaluation.py`):
   - Visual distractor testing
   - Robustness evaluation
   - Goal confusion analysis
   - Performance degradation

### Key Features to Implement

- **Goal Conditioning**: Policy takes goal image as input
- **Contrastive Learning**: Learn goal representations
- **Multi-Goal Training**: Handle multiple goal types
- **Distractor Robustness**: Test with visual distractors
- **Goal Sampling**: Diverse goal selection strategies

## 🎮 Demo Task
Train goal-conditioned BC on manipulation tasks:

### Task: Multi-Goal Manipulation
- Environment: Robosuite Can-v0 with multiple goals
- Goals: Different object positions and orientations
- Observation: RGB images + proprioception + goal image
- Action: 7-DoF arm + gripper

### Training Protocol
1. Collect demonstrations for multiple goals
2. Train contrastive goal encoder
3. Train goal-conditioned policy
4. Evaluate on held-out goals
5. Test with visual distractors

### Distractor Testing
- Add random objects to scene
- Change lighting conditions
- Add background clutter
- Test goal confusion rates

## 📊 Success Criteria
- [ ] Goal-conditioned policy works
- [ ] Contrastive encoder learns good representations
- [ ] Success rate >80% on training goals
- [ ] Success rate >60% on test goals
- [ ] Robust to visual distractors

## 🔧 Dependencies
```bash
pip install torch torchvision
pip install robosuite
pip install wandb tensorboard
pip install opencv-python
pip install matplotlib seaborn
pip install numpy scipy
```

## 📝 Mathematical Background

### Goal-Conditioned Policy
```
π(a|s, g) = MLP(CNN(s), CNN(g), s_proprio)
```

Where:
- s is the current observation
- g is the goal image
- CNN extracts visual features

### Contrastive Learning
```
L_contrastive = -log exp(sim(f_s, f_g+)/τ) / ∑_i exp(sim(f_s, f_g_i)/τ)
```

Where:
- f_s is current state features
- f_g+ is positive goal features
- f_g_i are negative goal features
- sim is cosine similarity

### InfoNCE Loss
```
L_InfoNCE = -E[log exp(f_s · f_g+ / τ) / ∑_i exp(f_s · f_g_i / τ)]
```

## 📝 Deliverables
- Complete goal-conditioned BC implementation
- Contrastive goal encoder
- Distractor evaluation framework
- Goal reaching demo
- Robustness analysis report

## 🚀 Next Steps
Tomorrow we'll implement language-conditioned imitation learning!
