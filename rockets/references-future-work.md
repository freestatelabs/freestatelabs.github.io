---
layout: default
title: References
parent: Rockets
nav_order: 6
---

# `rockets`

<small> [<< Back: Results](results) </small>

## References 

To complete this project, I relied primarily on the following sources of information, as well as others I linked to throughout the website:

### Textbooks 

* [Modern Control Engineering](www.amazon.com/Modern-Control-Engineering-Katsuhiko-Ogata/dp/0136156738) (2015) by Ogata
* [Discrete-Time Control Systems](https://www.amazon.com/Discrete-Time-Control-Systems-Katsuhiko-Ogata/dp/0130342815/) (1995) by Ogata
* [Introduction to Space Dynamics](https://www.amazon.com/Introduction-Space-Dynamics-Aeronautical-Engineering/dp/0486651134/)  (1986) by Thomson

### Online 

* [Control Bootcamp](https://www.youtube.com/watch?v=Pi7l8mMjYVE&list=PLMrJAkhIeNNR20Mz-VpzgfQs5zrYi085m) by [Steve Brunton](https://www.eigensteve.com/) (University of Washington)
* [katkimshow](https://www.youtube.com/channel/UCRCdl2SXma02BG384RuZPqg) by [Katherine Kim](http://katherinekim.net/wp/) (PEARS Lab, National Taiwan University)

### Graduate Theses and Academic Papers

* [A Robust Control Approach for Rocket Landing](https://project-archive.inf.ed.ac.uk/msc/20172139/msc_proj.pdf) (2017) by Reuben Ferrante
* [Powered Descent and Landing of an Orbital-Class Rocket](http://apmonitor.com/do/uploads/Main/Report_rocket_landing2019.pdf) (2019) by Gunnell, Mansfield, Rodriguez, and Medina  

In particular, the paper by Ferrante was very helpful.  We essentially solved the same problem, but with different techniques.  

## Future Work

I have a lot of work planned for this project.  Some of the highlights include:
* Implementing a more robust method of selecting cost function weights for the LQR controller and using this to compute the flight of a Falcon 9 rocket 
* Implementing model-predictive control (MPC) to replace the LQR controller; this will reduce some of the approximations made in the LQR controller and allow for a more optimal solution 
* Incorporate noise, errors, perturbations in the simulation, such as wind/aerodynamics, state measurements, c.g. offset, etc. and determine additional methods of making controller more robust 
* Studying the use of continuous-time reinforcement learning algorithms in solving this problem
