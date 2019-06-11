# DRLND_P2_Continous-Control

## Project Summary

In this project, a Unity environment, consisting of a double-jointed arm can move to target locations is investigated. A reward of +0.1 is assigned for each step that the agent's hand is in the goal location. The goal of the agent design is to maintain its position at the target location for as many time steps as possible.

The observation space is made up of 33 variables of the robotic arm:
* Position
* Rotation
* Linear Velocity
* Angular Velocity

Each action taken in the environment is a vector defined by four numbers, corresponding to the torque applicable to the two joints of the arm. Every entry in the action vector should be a number between -1 and 1. The task is episodic, and in order to solve the environment, the agent must achieve an average score of +30 over 100 consecutive episodes.

## Setup

The project solves the Unity ML-Agents Reacher environment (customized for Udacity) with either one or twenty robotic arms. To run the program clone this repository, and add the Unity Reacher app in the cloned folder, and specify the correct path to the application in the Continuous_Control_DDPG.ipynb notebook. The necessary Reacher version for a desired operating system can be accessed from the following links:

### One (1) Agent
Linux: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/one_agent/Reacher_Linux.zip)
Mac OSX: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/one_agent/Reacher.app.zip)
Windows (64-bit): [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/one_agent/Reacher_Windows_x86_64.zip)

### Twenty (20) Agents
Linux: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher_Linux.zip)
Mac OSX: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher.app.zip)
Windows (64-bit): [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher_Windows_x86_64.zip)

## Installation Dependencies

The following packages are required to run the program and can be installed via the pip command:
* unityagents
* numpy
* torch

## Code Execution
* In order to run the program, access the Jupyter Notebook: Continuous_Control_DDPG.ipynb
* Run the notebook cells using the play command.
* In order to train the agent and observe the training output, run the code: scores = ddpg()
