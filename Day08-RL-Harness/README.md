# Day 8: RL Harness

## 🎯 Learning Objectives
- Build a reusable RL infrastructure
- Implement vectorized replay buffer
- Create parallel environment runner
- Design common policy/value API

## 📚 Background
Today we'll build the foundation for all RL algorithms in the coming days. A good RL harness should be modular, efficient, and easy to extend with new algorithms.

## 🛠️ Coding Task

### Setup
```
Day08-RL-Harness/
├── rl/
│   ├── __init__.py
│   ├── replay_buffer.py    # Vectorized replay buffer
│   ├── env_runner.py       # Parallel environment runner
│   ├── policy.py           # Common policy interface
│   ├── value_function.py   # Common value function interface
│   └── base_agent.py       # Base agent class
├── utils/
│   ├── __init__.py
│   ├── logging.py
│   ├── checkpointing.py
│   └── metrics.py
├── demos/
│   ├── test_harness.py
│   └── performance_benchmark.py
├── configs/
│   └── rl_config.yaml
└── requirements.txt
```

### Implementation Requirements

1. **Vectorized Replay Buffer** (`rl/replay_buffer.py`):
   - Efficient storage for (s, a, r, s', done) tuples
   - Batch sampling with replacement
   - Prioritized experience replay support
   - Memory-efficient circular buffer

2. **Parallel Environment Runner** (`rl/env_runner.py`):
   - Vectorized environment execution
   - Asynchronous data collection
   - Episode management and statistics
   - Seed handling and reproducibility

3. **Policy Interface** (`rl/policy.py`):
   - Abstract base class for policies
   - Support for both deterministic and stochastic policies
   - Action sampling and log probability computation
   - GPU/CPU device handling

4. **Value Function Interface** (`rl/value_function.py`):
   - Abstract base class for value functions
   - State value and action-value support
   - Target network management
   - Gradient computation helpers

5. **Base Agent** (`rl/base_agent.py`):
   - Common training loop structure
   - Checkpointing and resuming
   - Logging and metrics collection
   - Evaluation protocol

### Key Features to Implement

- **Vectorization**: Efficient batch processing
- **Modularity**: Easy to swap components
- **Performance**: Optimized for speed
- **Logging**: Comprehensive metrics tracking
- **Reproducibility**: Consistent random seeds

## 🎮 Demo Task
Create a comprehensive test that:
1. Sets up 4 parallel cart-pole environments
2. Implements a simple random policy
3. Collects 1000 steps of experience
4. Tests replay buffer sampling
5. Measures:
   - Data collection speed (steps/second)
   - Memory usage
   - Sampling efficiency
   - Environment synchronization

## 📊 Success Criteria
- [ ] Replay buffer handles 1M+ transitions efficiently
- [ ] Parallel runner achieves >1000 steps/second
- [ ] Policy/value interfaces are clean and extensible
- [ ] All components work together seamlessly
- [ ] Performance benchmarks are documented

## 🔧 Dependencies
```bash
pip install torch torchvision
pip install numpy gymnasium
pip install wandb tensorboard
pip install pyyaml
```

## 📝 Design Principles

### Replay Buffer
```python
class ReplayBuffer:
    def __init__(self, capacity, obs_shape, action_shape, device):
        # Efficient storage with pre-allocated tensors
    
    def add(self, obs, action, reward, next_obs, done):
        # Add single transition
    
    def sample(self, batch_size):
        # Sample batch with replacement
    
    def __len__(self):
        # Current buffer size
```

### Environment Runner
```python
class EnvRunner:
    def __init__(self, env_fns, policy, max_steps):
        # Initialize parallel environments
    
    def collect_rollouts(self, n_steps):
        # Collect data in parallel
    
    def reset(self):
        # Reset all environments
```

## 📝 Deliverables
- Complete RL harness library
- Performance benchmarks
- Test suite for all components
- Usage documentation
- Integration examples

## 🚀 Next Steps
Tomorrow we'll implement SAC (Soft Actor-Critic) using this harness!
