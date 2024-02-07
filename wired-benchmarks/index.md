---
layout: default 
title: wired-benchmarks
nav_order: 4
has_children: true
katex: true
---


[Home](/) \| [Background >>](/wired-benchmarks/background)

I've been writing [`Wired.jl`](), which is a Julia library for calculating static 
magnetic fields in 3D space using the Biot-Savart law. As I was writing the 
library, I was surprised by how *slow* my code was running, despite my best 
efforts to keep it fast and efficient, so got the idea to benchmark the core 
algorithm by writing it in other languages. 

At the time, I thought that perhaps Julia wasn't as fast of a language as I 
expected, and that by writing it in Julia, I was "leaving some speed on the 
table". I also wanted to try my hand at learning another language like Fortran, 
or brushing up on my C skills, so I thought it would be a fun little project. 

As it turns out, I wasn't writing the Julia version very well. Now, the Julia 
implementation is the fastest one. I'm sure that others could write Fortran 
or C code that's far faster than mine, but to my surprise, my best efforts resulted 
in slower implementations in those two languages. 

I published this section of the website to:
* Publish some of my notes and lessons learned, in case someone else could learn from them
* Document the optimizations I performed to make the `Wired.jl` library as fast and efficient as possible 

All source code for this series of benchmarks is published here:  
[https://github.com/freestatelabs/wired-benchmarks/](https://github.com/freestatelabs/wired-benchmarks/)

## Prior Art 
Note that I am by far not the first person to think of writing this sort of code; 
for instance, see: 
* [https://github.com/vuthalab/biot-savart](https://github.com/vuthalab/biot-savart)
* [Biot Savart Law integrator BioSaw](https://arxiv.org/abs/1511.01629) (I couldn't find the source code anywhere)
* [Computation of the Biot-Savart line integral with higher-order convergence using straight segments](https://physics.paperswithcode.com/paper/computation-of-the-biot-savart-line-integral), code located [here](https://github.com/nickmcgreivy/biot-savart-line-integral)