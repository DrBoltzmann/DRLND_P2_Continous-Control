# DRLND_P2_Continous-Control

## Project Summary

In this project, a Unity environment, consisting of a double-jointed arm can move to target locations is investigated. A reward of +0.1 is assigned for each step that the agent's hand is in the goal location. The goal of the agent design is to maintain its position at the target location for as many time steps as possible.

The observation space is made up of 33 variables of the robotic arm:
* Position
* Rotation
* Linear Velocity
* Angular Velocity

Each action taken in the environment is a vector defined by four numbers, corresponding to the torque applicable to the two joints of the arm. Every entry in the action vector should be a number between -1 and 1. The task is episodic, and in order to solve the environment, the agent must achieve an average score of +30 over 100 consecutive episodes.

## Installation Dependencies

To run the program clone this repository, and add the Unity Reacher app in the cloned folder, and specify the correct path to the application.

The following packages are required to run the program and can be installed via the pip command:

unityagents import UnityEnvironment
numpy
from collections import deque
from itertools import count
time
torch
matplotlib.pyplot as plt
from numpy import random as nprandom
import random
import copy
from collections import namedtuple, deque
import torch
import torch.nn.functional as F
import torch.optim as optim

## Code Execution
In order to run the program, access the Jupyter Notebook, Continuous_Control_DDPG.ipynb, and run the notebook cells using the play command. The code:

scores = ddpg()

will execute the program and train the agent, with training output listed and graphed.
