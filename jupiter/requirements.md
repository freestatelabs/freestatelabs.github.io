---
layout: default 
title: Requirements
nav_order: 2
has_children: false
parent: Jupiter
---

# Requirements

My previous work with [`rockets`](\rockets\) was a bit haphazard at times and lacked a robust framework for developing the project and coding it. It was fun at first, but towards the end I suffered from a bit of disorganization - I should have been a bit more neat about how I kept the code. To fix this problem for a much more complicated endeavor, I am going to implement more 'professional' engineering project management, such as keeping a list of requirements and writing UML diagrams before starting the coding portions. 

## Mission Statement
`Jupiter` is a autonomous rocket-shaped flying vehicle that uses ducted fans for propulsion and thrust-vectoring for attitude control.  

`Jupiter` will take-off from a designated launch pad, fly to a maximum altitude of 2 meters, and land on a second launch pad that is no less than 2 meters from the launch site. 

## Top-Level Requirements

### [J.1] `Jupiter` shall include a full 6DOF 3D simulation of the rocket and control strategies
It is much faster to prototype on the computer than to iterate with hardware.

### [J.2] The vehicle shall fly to a maximum altitude of 2 meters.
This allows testing to occur indoors.

### [J.3] The vehicle shall land on a designated landing site that is no less than 2 meters away from the launch site.
Effectively, the testing should be able to be conducted in a small room.

### [J.4] The vehicle shall be no greater than 250g in mass.
For design purposes, I would like to stay below the [FAA drone regulation](https://www.faa.gov/uas/getting_started), if it were to be tested outdoors.

### [J.5] The vehicle shall land on a landing site within a radius of 125mm. 
Defines the precision that the control algorithm and sensors must achieve. Basically, I'm estimating the vehicle will be about 250mm tall, so the landing pad will be more or less the size of a standard piece of paper. 

### [J.6] The vehicle shall use ducted fans for propulsion and thrust-vectoring for attitude control.
This makes it interesting - many others have created all sorts of multirotors (i.e. quadcoptors), but an underactuated flying vehicle such as this is much more unique.

## Simulation Requirements

### [S.1] The simulation shall include an ability to test hyperparameters and variations in the design.
This shall support Monte-Carlo-style simulations of as-built variations of the hardware from the theoretical. Structuring the simulation in this way allows much easier tuning of these parameters without writing hard-to-debug test code - a lesson learned from `rockets`.

### [S.2] The simulation shall be written using Python.
For professional development and for speeding up the software development process, as I am both familiar with the language and there are many open-source libraries available for numerical analysis and visualization.

### [S.3] The simulation shall include full 6DOF physics.
I hope this isn't a bigger challenge than I think it is. 

### [S.4] The simulation shall include a robust framework for testing control strategies.
Part of the interest in using Python instead of Julia is that I am far more well-versed in the object-oriented nature of Python and have a better shot of making the simulation as modular as I need it to be. 

### [S.5] The simulation shall include full 3D visualization of the output data, as well as a "dashboard" for evaluating a simulated flight by comparing "actual" to "estimated" state values, control inputs, etc.
This gives me a chance to learn rudimentary GUI design. From `rockets`, I learned that visualization techniques were paramount to efficient debugging of control strategies. Visualization could take the form of (perhaps) a [Blender](https://demando.se/blogg/post/dev-generating-a-procedural-solar-system-with-blenders-python-api/) interface or the [VPython](https://vpython.org/) library. [Processing](https://processing.org/tutorials/p3d/#3d-transformations) may also be a good alternative.

This element of the simulation may actually be quite tough.

## Vehicle Requirements

### [V.1] The vehicle shall be fabricated from readily available hobby parts and 3D prints.
I have a 3D printer that I don't use enough; this will be a good project to make some custom parts from it. Unfortunately, the 3D printed parts are not quite mass-efficient and I may have to make use of cardboard, etc.

### [V.2] The vehicle shall include fixed landing legs and simple safety covers for flight electronics and actuators.
Rockets tend to crash and [explode during testing](https://www.youtube.com/watch?v=bvim4rsNHkQ). Hopefully, no explosions with this project, but I do expect a lot of crashes, so it would be nice not to have to build a new vehicle for each flight. 

## Performance Requirements

### [P.1] The vehicle shall be able to accelerate vertically at 1g at nominal (not peak) power. 
This lends the vehicle agility and a "wow" factor as it takes off. 

### [P.2] The vehicle shall be able to run for 15min of continuous flight at full throttle and maneuvering capability.

## Control System Requirements

### [C.1] The control system must run on a Arduino Nano microcontroller.
This is due to my familiarity with the platform. Multiple microcontrollers are permissible (i.e. for processing the flight control separately from the sensor data fusion and state estimation), as is the addition of a Raspberry Pi for video acquisition and telemetry.

### [C.2] The control system shall have a fail-safe killswitch with three modes.
1. On/standby: allows operation when receiving control signals from the base station.  
2. Off: disallows operation (kills thrust) when not receiving control signals from the base station.
3. Abort/standby: causes the vehicle to land when receiving this control signal from the base station.

### [C.3] The controller shall implement a linear state-feedback closed-loop controller.
*This area is under significant investigation.*
- I don't want to spend a lot of time actively trying to stay within the limits of the microcontrollers available - no use of online optimizers or neural networks is permissible, as they are computationally expensive and I don't even yet know how to write a real-time software program. 
- The controller will make use of a feed-forward model of the plant (i.e. the vehicle dynamics)
- The controller will make use of the "cleaned" state estimation provided by the onboard INS.

### [C.4] The controller shall include an inertial navigation system (INS).
This requirement [may not be possible](https://redshiftlabs.com.au/wp-content/uploads/2018/02/an-1007-estimatingvelocityandpositionusingaccelerometers.pdf) to achieve with the hardware available. It may also be an incredible effort to create. However, it is my hope that using a laser distance sensor for altitude measurements may be sufficient to eliminate the ["drift"](https://forum.arduino.cc/t/inertial-navigation-system/417158/5) caused by accumulated sensor error.

### [C.5] The controller shall perform state estimation, fusing several different sensor types with a Kalman filter at the core.

