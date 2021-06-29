# Project Report 

## Environment
In this environment, a double-jointed arm can move to target locations. A reward of +0.1 is provided for each step that the agent's hand is in the goal location. Thus, the goal of your agent is to maintain its position at the target location for as many time steps as possible.

The observation space consists of 33 variables corresponding to position, rotation, velocity, and angular velocities of the arm. Each action is a vector with four numbers, corresponding to torque applicable to two joints. Every entry in the action vector should be a number between -1 and 1.

## Agent
I've used a ddpg agent along with actor-critic networks and replay buffer.

Agent `ddpg_Agent.py`

The agent has the methods that interacts with the environment: `step()`, `act()`, `learn()` and some others.

Models used are defined in `model.py`

The architecture of the model has two networks, one for the actor and the other for the critic.


## Network Architectures.
Two hidden units for each of the actor and critic networks.
Added batchnorm after the first hidden layer of both the networks.
For actor: 
* Fully connected layer - input size is 33(state size) and output is 256 activation used is RELU
* Fully connected layer - input size is 256 and output is also 128 activation used is RELU
* Fully connected layer - input size is 128 and output is 4(action size) activation used is tanh

For critic: 
* Fully connected layer - input size is 33(state size) and output is 256 activation used is RELU
* Fully connected layer - input size is 260 and output is also 128 activation used is RELU
* Fully connected layer - input size is 128 and output is 1
## Hyperparameters

Training (after much experimentation) used the following hyperparameters:

```
BUFFER_SIZE = int(1e6)  # replay buffer size
BATCH_SIZE = 128        # minibatch size
GAMMA = 0.99            # discount factor
TAU = 1e-3              # for soft update of target parameters
LR_ACTOR = 1e-4        # learning rate of the actor 
LR_CRITIC = 2e-3        # learning rate of the critic
WEIGHT_DECAY = 0        # L2 weight decay
UPDATE_EVERY = 20       # how often to update the network
UPDATE_TIMES = 10      # how many times to update the network each time
EPSILON = 1.0           # epsilon for the noise process added to the actions
EPSILON_DECAY = 1e-6

```


## Training Plot
The agent was able to solve the environment by achieving score of 30.0 over 100 consecutive episodes after 231 episodes.
![ ](https://github.com/gouthamcm/Reacher/blob/main/plot.png)

## Training Output

```
Episode 100	Average Score: 2.74
Episode 200	Average Score: 23.88
Episode 231	Average Score: 30.19
Environment solved in 231 episodes!	Average Score: 30.19
```

## Future Work

 - Use a priority algorithm for sampling from the replay buffer instead of uniformly sampling
