[image001]: ./images/RL_illustration.png "RL Illustration"
[image002]: ./images/DDPG_pseudo_code.png "DDPG pseudo code"
[image003]: ./images/DDPG_illustration.png "DDPG_illustration"
[image004]: ./images/Code_Architecture.png "Code_Architecture"

[image005]: ./plots/results_001.png "results_001"
[image006]: ./plots/results_002.png "results_002"
[image007]: ./plots/results_003.png "results_003"
[image008]: ./plots/results_004.png "results_004"
[image009]: ./plots/results_005.png "results_005"
[image0010]: ./plots/results_006.png "results_006"
[image0011]: ./plots/results_007.png "results_007"
[image0012]: ./plots/results_008.png "results_008"


# DRLND_P2_Continous-Control

## Project Summary

In this project, a Unity environment, consisting of a double-jointed arm can move to target locations is investigated. A reward of +0.1 is assigned for each step that the agent's hand is in the goal location. The goal of the agent design is to maintain its position at the target location for as many time steps as possible.

The observation space is made up of 33 variables of the robotic arm:
* Position
* Rotation
* Linear Velocity
* Angular Velocity

Each action taken in the environment is a vector defined by four numbers, corresponding to the torque applicable to the two joints of the arm. Every entry in the action vector should be a number between -1 and 1. The task is episodic, and in order to solve the environment, the agent must achieve an average score of +30 over 100 consecutive episodes.

## Solution Architecture: DDPG

A reinforcement learning (RL) approach is implemented utilizing Deep Deterministic Policy Gradients (DDPG). The algorithm development is detailed in the following paper:

Continuous control with deep reinforcement learning
https://arxiv.org/abs/1509.02971

A practical summary from OpenAI can be found here:
https://spinningup.openai.com/en/latest/algorithms/ddpg.html

...and an overview of DDPG with respect to other algorithms in RL is discussed here:
https://towardsdatascience.com/introduction-to-various-reinforcement-learning-algorithms-i-q-learning-sarsa-dqn-ddpg-72a5e0cb6287

RL starts with the classic concept of an agent acting in an environment and receiving a reward:
![alt text][image001]

In essence, instead of solving for a specific (state, action) based on a defined policy (as is common in conventional RL), DDPG looks to modify and optimize the policy, hence the use of policy gradients. DDPG learns a Q-function and a policy, using off-policy data and the Bellman equation to learn the Q-function, and then the Q-function is used to learn the policy required to solve the environment. This allows for a continuous environment to be solved, where the the number of (action, state) is too large to be effectively solved due to computational size. A key element of DDPG is the use of Actor-Critic neural network models to drive evaluation of the decisions in the environment.

The pseudo code for DDPG is given here:

![alt text][image002]

In the code implementation view, DDPG has four main components:

* Agent
* Actor
* Critic
* DDPG Algorithm

Initially, the Actor and Critic networks are initialized randomly. At each time-step, the current state is fed into the actor network, a value is then returned which if fed into the noise function of the Agent. Taking this action naturally leads to a new state value and associated reward. As with Deep Q-Learning, the temporal relationship between actions and rewards is essential to contextualizing the relationship between action sequences and reward in the environment. The Agent includes a Replay Buffer function, which stores the history of: State, Action, Reward, NextState. Conceptually DDGP is illustrated in the following diagram:

![alt text][image003]

A random sample is taken from the Replay Buffer, and fed to the Critic Network, which then evaluates with the new state with an action from the Actor network, which ultimately provides the new state. The Replay Buffers essentially stores experiences, and is sampled from to direct new actions. In other words, it learns to take new actions based on previous experiences. To implement stable learning behavior, the Replay Buffer must be large to contain enough experiences to be useful. A trade-off needs to exist so that the algorithm doesn't use only the the very-most recent data, since this would logically lead to overfit of recent actions, but not generalize well across all action experiences. Therefore it is essential that a random sample of experiences be taken to direct new actions. The Critic is evaluated with the new state, based on the taken action from the Actor, in order to approximate the next reward. With the policy-based approach, the Actor learns how to act by maximizing reward and thereby estimating the optimal policy. Here gradient ascent is used (traditionally gradient descent is used in deep learning optimization methods). With the value-based approach, the Critic estimate the cumulative reward of the (state, action) sets.

## Code Implementation
A vanilla implementation of DDPG, following from example DDPG code was used (https://github.com/udacity/deep-reinforcement-learning/tree/master/ddpg-bipedal). The code is implemented in three files, and an overview of the main functions included in each file is shown below:

![alt text][image004]

### DDPG
The Unity environment is loaded and main libraries imported. The DDPG function is defined which implements the DDPG algorithm, and the Agent is trained. The training results are also generated here to evaluate the training evolution and check if the environment has been solved or not.

### DDPG Agent
The Agent defines key functions such as OUNoise, Learn, Step and the Replay Buffer. The model functions are imported, where the neural networks for the Actor and Critic are defined.

### Model
The model.py file includes the Actor and Critic networks, including key parameter implementations such as the number of fully connected unit (FCU) in network layers and the activation function (ReLu).

## Solution

To explore and tune neural network fully connected unit sizes and Agent hyper-parameters, initial training runs were done with 50 episodes to look at the relative rise in score. The logic was that parameter combinations which lead to relatively stable scores with low exponential increase would probably not achieve the desired target of 30 in relatively few (or if ever) episode iterations.

Below is a sampling of selected training results showing the relative difference between fully connected unit layer sizes and seed values.

![alt text][image006]
![alt text][image008]
![alt text][image009]
![alt text][image0010]
![alt text][image0011]

The Training History and Evolution are in the table and plot below. The Agent could achieve an average over 100 episodes of over 30 after 300 episodes. Hyper-parameter tuning mainly involved modification of the fully connected units in the neural network and the random seed value. The following parameters appeared to be most likely to produce a successful training run:

| fc1_units | fc2_units | seed |
|-----------|-----------|------|
| 300       | 150       |  40  |

### Training Results

Based on the chosen parameters, the following training results were achieved, with an average score of 30.06 achieved in 126 episodes.

| Episode | Avg Score | Score  |
|---------|-----------|--------|
| 100     | 5.67      | 16.420 |
| 200     | 26.93     | 30.610 |
| 226     | 30.06     | 34.850 |

The full training history out to 400 episodes is shown below:

![alt text][image0012]

## Future Directions

D4PG : 2018 algorithm that applies the distributional approach to a DDPG with an asynchronous architecture
https://arxiv.org/pdf/1804.08617.pdf
