---
layout: default
use_math: true
permalink: /rockets/introduction.html
---

# `rockets`

<small>[<< Back: Overview](/rockets) | [Next: Physics >>](physics) </small>

## Introduction

While a graduate student taking controls courses, I was captivated watching SpaceX landing their Falcon 9 first-stage boosters.  I wondered what sorts of control algorithms were required to continually perform such an amazing feat. This project is designed to test the performance of different control strategies for solving this problem in 2 dimensions.

### Problem Statement 

The hypothetical scenario is this: as an up-and-coming space launch vehicle company, you'd like to test scale models of your rocket and controller before committing to building a full-scale vehicle prototype.  

A successful test flight involves a takeoff, flying to a specified altitude and ground position, and then landing on the launchpad.  The rocket is well-balanced and has a gimballed thruster that can be commanded to increase and decrease its throttle, as well as rotate to provide directional thrust.  This problem is functionally similar to the [OpenAI Gym LunarLanderContinuous-v2 Environment](https://gym.openai.com/envs/LunarLanderContinuous-v2/); however, note that similar solutions to this problem include side thrusters, which I do not - I wanted to see if it was possible to control the rocket via thrust-vectoring alone.  

How do you control the rocket?  How well do your algorithms perform?

### Controller Methods 

When I first started this project, I had a basic understanding of [full-state feedback/pole placement](https://en.wikipedia.org/wiki/Full_state_feedback), [PID](https://en.wikipedia.org/wiki/PID_controller), [LQR](https://en.wikipedia.org/wiki/Linear%E2%80%93quadratic_regulator), and discrete-time [reinforcement learning](https://en.wikipedia.org/wiki/Reinforcement_learning) (RL) techniques.  My assumptions were that: 
* PID controllers would be difficult to implement and tune, as they are intended for single-input, single-output (SISO) systems, and this is a multiple-input, multiple output (MIMO) system 
* LQR controllers operate on linear systems, and as this system is nonlinear, they would provide subpar results - if they worked at all 
* Discrete-time RL techniques would be unwieldly and the curse-of-dimensionality involved in discretizing the continuous state/action space would require tremendous solve times

To date, I have only implemented the LQR controllers and have been impressed with their performance.  Linearizing the system of equations governing the problem proved to be far more robust than I imagined.  
