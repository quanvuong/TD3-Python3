# Python3 port of Addressing Function Approximation Error in Actor-Critic Methods

A port of the official PyTorch implementation of Twin Delayed Deep Deterministic Policy Gradients (TD3) to Python 3 with a few additional changes:

1. trange from the tqdm package is used to display progress bar
2. torch.set_num_threads(1)
3. Use tensorboardX to visualize evaluation performance during training
4. One centralized function to set seed. Also set the seed for the GPU.
5. Evaluation is run for 100 instead of 10 episodes.
6. Performance is tested on the v2 version of OpenAI Mujoco environments instead of v1

With the same sets of hyper-parameters as in the original Python2 implementation, performance is high for every environment tested except for Ant-v2.

### Performance

![](results/graphs/Ant-v2.png) ![](results/graphs/HalfCheetah-v2.png) ![](results/graphs/InvertedPendulum-v2.png) ![](results/graphs/Reacher-v2.png)

![](results/graphs/Hopper-v2.png) ![](results/graphs/Walker2d-v2.png) ![](results/graphs/InvertedDoublePendulum-v2.png)

### Usage
The results can be reproduced exactly by running:
```
./experiments.sh
```
Experiments on single environments can be run by calling:
```
python main.py --env HalfCheetah-v2
```

The authors include an implementation of DDPG (DDPG.py) for easy comparison of hyper-parameters with TD3, this is not the implementation of "Our DDPG" as used in their paper (see OurDDPG.py).

To open tensorboard visualization, run:
```
tensorboard --logdir runs
```
### Results
Each learning curve are formatted as NumPy arrays of 201 evaluations (201,), where each evaluation corresponds to the average episode return from running the policy for 100 episodes with no exploration. The first evaluation is the randomly initialized policy network (unused in the paper). Evaluations are performed every 5000 time steps, over a total of 1 million time steps. There is a notebook in the results folder to visualize the performance.
