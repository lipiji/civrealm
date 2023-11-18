# Tensor Agent
Welcome to Civrealm Tensor Agent! This documentation will guide you through the process of training tensor-based agents, specifically using the Proximal Policy Optimization (PPO), in the Civrealm Environment. We will first provide an overview of the Civrealm Tensor Env, followed by instructions on how to use the Civtensor repository to train a PPO agent on this environment.

## 🌏 Civrealm Tensor Environment
The Civrealm Tensor Environment is a reinforcement learning environment wrapped upon Civrealm Base Env specifically designed for training agents using tensor-based algorithms. This environment 

- provides flattened, tensorized observation and action spaces,
- restrict available actions in order to reduce meaningless actions,
- offers delta game score as a basic reward for RL agents,
- provide parallel environments with batched inputs and outputs for efficient training, 

and various modular wrappers which are open to customize your own environment.

## 🏃Using civrealm-tensor-baseline Repository



The civrealmtensor-baseline repository is a collection of code and utilities that provide a baseline implementation for training reinforcement learning agents using tensor-based algorithms.

It includes an implementation of the PPO algorithm, which we will use to train our agents in the Civrealm Tensor Environment.

## 🏌️ Getting Started
To get started, follow these steps:

First install
```
cd civrealmtensor-baseline
pip install -e .
```

then run the training script
```sh
cd examples
./train.sh # or python train.py
```

> If you encounter the error "./train.sh: line 1: python: command not found", you may change "python" in train.sh to "python3".

### Fullgame
Edit `civrealmtensor-baseline/civtensor/configs/envs_cfgs/freeciv_tensor_env.yaml`

Change `task_name` to `fullgame`

```yaml
task_name: fullgame
```

### Minigame

### Run all minitasks

Before running, please download the mini task maps according to [Prepare Dataset](https://civrealm.github.io/civrealm/advanced_materials/minigame/#prepare-dataset).

`civrealmtensor-baseline/examples/run.py` will run all minitasks specified in `examples/run_configs` including 12 types x 3 levels = 36 runs.
```sh
cd exmaples
python run.py --webdir $civrealm-dir
```
where `$civrealm-dir` should specify the path of your local **civrealm** repo.

### Expreiment results are in
```sh
civrealm-tensor-baseline/examples/results 
```

To view your results on tensorboard, alter the following script to match your path structure and run
```sh
cd examples/results/freeciv_tensor_env/$game_type/ppo/installtest/seed-XXXXXXXXX
# where $game_type = fullgame or minitask
tensorboard logs/
```
then the results should be visible in the browser.


## Customize
Training parameters could be adjusted in `civrealmtensor-baseline/civtensor/configs/algos_cfgs/ppo.yaml`

For training minitask tensor baseline, we used the following default setting:

```yaml
seed:
  # whether to use the specified seed
  seed_specify: False
  # seed
  seed: None
train:
  # number of parallel environments for training data collection
  n_rollout_threads: 8
  # number of total training steps
  num_env_steps: 20000
  # number of steps per environment per training data collection
  episode_length: 125
  # logging interval
  log_interval: 1
```

Congratulations! You have successfully set up the Civrealm Tensor Agent and trained a PPO agent on the Civrealm Tensor Environment using the tensor-baseline repository.

## Conclusion
In this guide, we introduced the Civrealm Tensor Environment and explained how to use the tensor-baseline repository to train a PPO agent on this environment. We encourage you to explore the various features and customization options available in the Civrealm Tensor Agent and experiment with different reinforcement learning algorithms to further enhance your agent's performance. Happy training!


