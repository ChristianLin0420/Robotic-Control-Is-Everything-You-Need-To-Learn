# Day 12: Domain Randomization

## 🎯 Learning Objectives
- Implement comprehensive domain randomization
- Understand sim-to-real transfer challenges
- Apply randomization to visual and physical properties
- Measure robustness under domain shifts

## 📚 Background
Domain randomization is crucial for sim-to-real transfer. By randomizing various aspects of the simulation during training, we can learn policies that are robust to the reality gap.

## 🛠️ Coding Task

### Setup
```
Day12-Domain-Randomization/
├── randomization/
│   ├── __init__.py
│   ├── visual_randomizer.py  # Texture, lighting, colors
│   ├── physics_randomizer.py # Mass, friction, dynamics
│   ├── temporal_randomizer.py # Delays, frame rates
│   └── domain_sampler.py     # Randomization strategies
├── environments/
│   ├── __init__.py
│   ├── randomized_env.py     # Wrapper with randomization
│   └── env_factory.py
├── training/
│   ├── train_with_randomization.py
│   ├── robustness_evaluation.py
│   └── ablation_study.py
├── demos/
│   ├── randomization_demo.py
│   ├── robustness_test.py
│   └── transfer_analysis.py
├── configs/
│   └── randomization_config.yaml
└── requirements.txt
```

### Implementation Requirements

1. **Visual Randomization** (`randomization/visual_randomizer.py`):
   - Texture randomization
   - Lighting variation (intensity, direction, color)
   - Background changes
   - Camera noise and distortion

2. **Physics Randomization** (`randomization/physics_randomizer.py`):
   - Mass and inertia variation
   - Friction coefficient changes
   - Joint damping and stiffness
   - Gravity and air resistance

3. **Temporal Randomization** (`randomization/temporal_randomizer.py`):
   - Action delays
   - Frame rate variation
   - Observation noise
   - Control frequency changes

4. **Robustness Evaluation** (`training/robustness_evaluation.py`):
   - Test on fixed domains
   - Measure performance degradation
   - Compare with/without randomization
   - Statistical analysis

### Key Features to Implement

- **Systematic Randomization**: Cover all relevant parameters
- **Realistic Ranges**: Use physically plausible values
- **Curriculum Learning**: Gradually increase randomization
- **Evaluation Protocol**: Fair comparison across conditions
- **Visualization**: Show randomization effects

## 🎮 Demo Task
Train PPO with domain randomization and evaluate robustness:

### Task: Manipulation with Randomization
- Environment: Robosuite manipulation task
- Randomization:
  - **Visual**: Textures, lighting, colors, backgrounds
  - **Physics**: Mass ±20%, friction ±50%, damping ±30%
  - **Temporal**: Action delays 0-50ms, frame rate 20-60Hz

### Evaluation Protocol
1. Train two policies:
   - **Baseline**: No randomization
   - **Randomized**: Full domain randomization
2. Evaluate on:
   - **Nominal**: Default simulation parameters
   - **Perturbed**: Various fixed parameter sets
   - **Extreme**: Edge cases of parameter ranges
3. Measure:
   - Success rate on each condition
   - Performance variance
   - Robustness score

## 📊 Success Criteria
- [ ] Comprehensive randomization implemented
- [ ] Randomized policy is more robust
- [ ] Performance variance is reduced
- [ ] Clear improvement in sim-to-real potential
- [ ] Ablation study shows which randomizations matter

## 🔧 Dependencies
```bash
pip install torch torchvision
pip install robosuite
pip install opencv-python
pip install wandb tensorboard
pip install matplotlib seaborn
```

## 📝 Randomization Strategies

### Visual Randomization
```python
# Texture randomization
texture_id = random.randint(0, num_textures)

# Lighting randomization
light_intensity = random.uniform(0.5, 2.0)
light_direction = random.uniform(-1, 1, 3)

# Color randomization
object_color = random.uniform(0, 1, 3)
```

### Physics Randomization
```python
# Mass randomization
mass_multiplier = random.uniform(0.8, 1.2)

# Friction randomization
friction_coeff = random.uniform(0.1, 0.9)

# Joint properties
joint_damping = random.uniform(0.1, 1.0)
```

## 📝 Deliverables
- Complete domain randomization system
- Robustness evaluation framework
- Ablation study results
- Transfer analysis report
- Randomization visualization tools

## 🚀 Next Steps
Tomorrow we'll combine classical control with RL using residual policies!
