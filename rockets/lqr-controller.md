---
layout: default
use_math: true
parent: Rockets
title: LQR Controller
nav_order: 3
---


# `rockets`

<small>[<< Back: Physics](physics) | [Next: Simulation >>](simulation) </small>

## LQR Controller

The Linear Quadratic Regulator (LQR) controller is explained in detail by [Steve Brunton](https://www.youtube.com/watch?v=1_UobILf3cc) and [Ogata](https://www.amazon.com/Modern-Control-Engineering-Katsuhiko-Ogata/dp/0136156738), so I won't cover all of the details here.  I consulted the [Wikipedia article](https://en.wikipedia.org/wiki/Linear%E2%80%93quadratic_regulator) significantly for the following section.

### LQR Basics 

Consider the state-space system previously derived in the form of: 

i$ \dot{x} = A x + B u i$  
i$ y = C x + D u i$

where i$ A i$ is a matrix of size `n x n` and i$ B i$ is size `n x r`.

The LQR controller is simply a form of full-state feedback that computes state-feedback gains which provide an optimal response.  In this case, optimality is considered via a cost function that is quadratic in i$ x i$ and i$ u i$.  

In general, there are two types of LQR controllers: one that explicitly states the final time to reach the desired end state ("finite-horizon"), and one that does not prescribe a final time ("infinite-horizon").  For this problem, the infinite-horizon case is assumed, and therefore the cost function is defined as:

$$ 
J=\int _{{0}}^{\infty }\left(x^{T}Qx+u^{T}Ru+2x^{T}Nu\right)dt
$$ 

i$ Q i$, i$ R i$, and i$ N i$ are matrices chosen as cost function weights.  In particular, i$ Q i$ and i$ R i$ are diagonal, and i$ N i$ is often neglected.  Note that the controller is considered optimal *only with respect to the choice of cost function weights* - in other words, these must be chosen carefully to produce the desired result, and the system is not "optimal" simply by virtue of implementing the LQR controller itself.  

The state-feedback gain matrix i$ K i$ is computed via: 

$$ 
K=R^{{-1}}(B^{T}P+N^{T})
$$

and i$ P i$ is solved by computing the steady-state [algebraic Riccati equation](https://en.wikipedia.org/wiki/Algebraic_Riccati_equation):

$$
A^{T}P+PA-(PB+N)R^{{-1}}(B^{T}P+N^{T})+Q=0
$$

I found solving this equation to be difficult and implemented [`MatrixEquations.jl`](https://github.com/andreasvarga/MatrixEquations.jl) instead of writing my own solver.

Since the state-feedback controller is of the form

$$ u = - K x $$

the state-space system becomes 

$$ \dot{x} = (A - K) x $$

This illustrates the result of the pole-placement/state-feedback techniques: the controller is simply moving the location of the system poles (eigenvalues) to the desired location.  

### Cost Function Selection

A significant challenge in the use of LQR controller is selecting cost function weights.  Often, the simple choice is trial and error.  However, there are slightly more directed approaches, as detailed on pg 3 of these [lecture notes](http://www.cds.caltech.edu/~murray/courses/cds110/wi07/lqr.pdf), or even more advanced techniques such as the [Bees](http://www.joace.org/uploadfile/2016/1025/20161025051823903.pdf) algorithm.  

A typical allowable error-based approach based on the lecture notes referenced above would set the diagonal elements of i$ Q i$ and i$ R i$ to be: 

$$ 
q_i = e_{i}^{-2}, \quad r_i = \rho \cdot f_{i}^{-2}
$$ 

where i$ e_i i$ is the allowable error of the `i`-th state, i$ f_i i$ is the allowable "effort" of the `i`-th control, and i$ \rho i$ is a proportionality constant.

For this simulation, I found that the error-based method did not provide proper results, so I used trial-and-error to find an appropriate cost function for the “scale” rocket cases.  However, trial-and-error did not yield a robust solution for the full-scale Falcon 9 simulation, so cost function weight selection is still an area of significant work.

### LQR Implementation

The cost function and system matrices are computed for each specific system under study offline, before running the simulation.  However, given that the rocket is a variable-mass system and mass was the 7-th state eliminated in the linearization procedure, the pre-computed cost function and state-feedback gain matrix is not strictly valid once the rocket begins to produce thrust.  

In practicality, I found that the pre-computed feedback gains were sufficient to provide reasonable operation of the rocket.  However, within the control loop of the simulation, I added a mass-change flag: if the mass of the rocket changes by a certain threshold value, then the feedback gains are recomputed.  This reduces computational effort and provides robustness for the solution.  

In summary, the control strategy is:
1. Consider the current state of the system 
2. If mass has changed by threshold value, recompute the feedback gain matrix 
3. Use feedback gain matrix to compute the required thrust and thrust vector direction of the rocket engine. 

### Limitations of the LQR Controller

The LQR controller itself has significant limitations if strictly implemented:
* Plant must be linear
* Constraints on states and controls cannot be represented 
* The weights placed on the cost function often may not have physical meaning and cause difficulty tuning the controller

In this application, the plant is very much nonlinear (especially when considering it as a variable-mass system) and there are significant constraints on the states and controls.  One of the most obvious issues is that of the control - the controller may often 'request' output from the plant that is not possible, i.e. negative thrust or thrust vectoring outside the gimbal limits.  These issues significantly reduce the native capability of the controller to support this system without external workarounds.  Some of these workarounds are:
* Computing constraints on states and controls outside the control loop (i.e. 'clipping' the control signal) 
* Using excessive cost function weights to prevent undesired system states 

In general, the LQR controller performed exceptionally well despite these limitations.  However, the future of this project is likely with MPC (model predictive control), as that type of controller supports nonlinear systems and state/control constraints.

