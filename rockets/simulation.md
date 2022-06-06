---
layout: default
title: Simulation
parent: Rockets
nav_order: 4
---

# `rockets`

<small>[<< Back: LQR Controller](lqr-controller) | [Next:Results >>](results) </small>

## Simulation 

The simulation was developed using Julia and is dependent on the following packages:
* [`DifferentialEquations.jl`](https://github.com/SciML/DifferentialEquations.jl)
* [`Plots.jl`](https://github.com/JuliaPlots/Plots.jl)
* [`MatrixEquations.jl`](https://github.com/andreasvarga/MatrixEquations.jl)

All may be imported via the `using Pkg; Pkg.add(PACKAGE_NAME)` command in the REPL.  

The source code is not yet publicly available. 

### Program Structure

The program is organized into three modules:
* `Physics`: contains data structures and functions to compute the motion of the rocket 
* `LQR`: contains data structures and functions to compute the control strategy of the rocket 
* `Vis`: contains data structures and functions for plotting and visualization of the flight

### Program Execution 

The program is designed to be run via test scripts.  Each test script:
* Defines the parameters of the rocket, including mass, maximum thrust, etc.
* Defines the controller: cost function weights, setpoints, control limits
* Defines the parameters of the simulation, such as time stepping and initial conditions
* Executes a function called `run_3dof()` that executes the simulation and produces results data
* Plots the state and control variables via `plot_3dof_sol()` and creates an animation via `animate_scene()`

### Notes on the Source Code
* The test script defines a discrete time step, but the equations of motion are integrated between time steps using numerical methods found in `DifferentialEquations.jl` - therefore, the control strategy is discrete, but the simulation itself is "piecewise-continuous"
* User-defined composite types (structs) are used throughout to package data in meaningful ways for compatibility between functions in different modules
* Physics of the landing legs are not modelled directly, but still used to determine if a landing was successful
* The animations are created by manipulated `Shape` objects in `Plots.jl`; this is a similar approach to creating animations in MATLAB in that the library was not necessarily designed for this
* The simulation does not execute in real-time with the animation - this was chosen specifically to separate the two functional portions of the program 
* Solving the simulation takes significantly less computational time than plotting the results, even with small time steps and long simulation run times
