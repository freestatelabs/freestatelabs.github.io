---
layout: default 
title: Jupiter
nav_order: 3
has_children: true
---

# `Jupiter`
*updated 8 July 2022*

`Jupiter` expands upon the work of [`rockets`](/rockets/) to develop a hardware prototype of a model rocket with thrust vectoring. I am still in the early phases, but when completed this project will include:
- [ ] A full 3D 6DOF simulation of the hardware, with control strategies and hyper-parameter testing
- [ ] A hardware prototype that uses ducted fans for propulsion and is autonomously controlled
- [ ] Supporting test hardware to develop mathematical models (for the simulation) with actual flight hardware
- [ ] A cool flight demo video from onboard cameras!

See [this video](https://www.youtube.com/watch?v=_kd64VE3A1c) for an example of the inspiration for this project.

Completion of this project will take quite a lot of time and effort, but I'm excited to get started! Some of the things I hope to learn along the way:
- PID tuning and use of these controllers inline to reduce overall system error
- Kalman filters, for multi-sensor fusion and state estimation
- [Constrained](https://minds.wisconsin.edu/bitstream/handle/1793/10888/file_1.pdf;jsessionid=E37EE713768126B67D0EDB398335C683?sequence=1) [LQR](https://underactuated.mit.edu/lqr.html)
- Robust control techniques
- Inertial navigation
- Embedded systems and "pseudo-real-time" development
- Further learning of C++ and Python programming

## Similar Projects
Other people have completed similar projects! Some of the interesting ones I found:
- [Daniel Riley/rctestflight](https://www.youtube.com/watch?v=zrONFl19QlI)
- [Tom Stanton](https://www.youtube.com/watch?v=_kd64VE3A1c) (linked previously)
- [Rocketry Forum](https://www.rocketryforum.com/threads/edf-rocketry.168878/)
- [Brian Brocken](https://www.youtube.com/watch?v=41UrzTPhG0g)
- [Mulyana and Faiz, 2018](https://iopscience.iop.org/article/10.1088/1757-899X/306/1/012004)

It looks like most of these "Electric Ducted Fan Rockets" (EDF) are designed to be remotely controlled and fly like a drone, rather than autonomously. 

