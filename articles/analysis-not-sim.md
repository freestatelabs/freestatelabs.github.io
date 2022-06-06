---
title: Engineering Analysis is Not Simulation
parent: Articles
nav_order: 1
date: 2022-06-05
layout: default
---

# Engineering Analysis is Not Simulation
*5 June 2022*

Engineering analysis is not simulation. I will repeat this as many times as I have to in order to get the point across. 

Engineering analysis is not simulation. 

I, like all people who write, know that word choice matters. Choosing to use a specific word, or omit another, shapes the meaning of text and therefore understanding. Writing, a visual form of communication, is about conveying understanding from one person to another. 

The term *simulation* refers to a digital representation of the physical world. In particular, *simulation* conveys a sense of a perfect representation of the real, physical world on a computer. Think of the Matrix or the **OASIS** in *Ready Player One*. These simulations mimic reality so well that a user finds it nearly impossible to tell the difference. 

Engineering analysis does not do this. Engineering analysis converts a set of *assumptions* about reality into *expectations* of reality via a mathematical *model* of reality. **These assumptions and models are foundational to the results of engineering analysis.** 

Classic engineering analysis one-liners include:

>*The outputs are only as good as the inputs.*

>*Garbage in, garbage out.*

> *State your assumptions clearly and carefully.*

These types of slogans might sound dull and last-century to the current generation (my generation) of engineers, but these concepts are so necessary for understanding what the calculations *mean.*

Of course, when I refer to 'engineering analysis', what I'm talking about are both finite element analysis (FEA) and classic closed-form calculations, i.e. hand calcs: **F/A**, **Mc/I**, etc. With a hand calc, it's immediately obvious that the calculation is based on a set of assumptions. With just a few scribbles on a paper or keystrokes in a spreadsheet, those inputs can be changed and the results seen immediately.  With finite element analysis, it's a different story.

FEA programs provide a level of ambiguity to the user. The user enters in the model information, including CAD data, mesh parameters, material information (this is a big one), loads, boundary conditions, and any other input data or settings necessary to produce a solution. Afterwards, the computer determines the answer and displays it to the user. While in this case, the user must enter more data manually than that required for a hand calc, the actual solution itself is, by and large, hidden behind the scenes. In most software, this is now a design choice (SolidWorks in particular does a great job of eliminating nearly all reference to the underlying finite element method). 

This means that there are **many more** assumptions made in finite element analysis than a typical hand calculation! 

FEA software companies have recently (or perhaps always, I'm not old enough to really know) rebranded themselves as 'simulation' software providers. With SolidWorks and Dassault Systemes, it's in the name: [SolidWorks Simulation](https://www.solidworks.com/domain/simulation) in the first case, and [SIMULIA](https://www.3ds.com/products-services/simulia/) in the latter. ANSYS' current tagline is *"Engineering Simulation Software"* and as I'm writing this, they're hosting "Simulation World 2022". All of these are disingenuous attempts to establish credibility with their software tools - in my opinion, a dangerous play. 

I've used all of these software packages extensively for performance-critical applications such as submarine, satellite, and nuclear reactor design. None of them is *anything* like a simulation. (Two far more than the third, anyone who knows this industry will immediately recognize which ones I mean.)

In physics labs in college, we painstakingly covered the procedures for determining the uncertainty of measurements. The quality of the measurement is dictated by the uncertainty of the instrument used to produce the measurement. For example, let's say you are performing an experiment on the number of calories contained in apples. But each apple you use for the experiment is not going to be exactly the same mass, so before performing the experiment, you need to measure the apple. If you use a scale that measures to the nearest kilogram (like one you might use for measuring cars and elephants), it will only tell you that each apple weights 0 or 1 kg. Neither of those measurements is accurate or useful! In this case, you might choose a scale that measures to the nearest gram or tenth of a gram.

In the same vein, the quality of an engineering calculation is determined by the accuracy of the input data and the uncertainty in the measurements of that data. Another example: let's say you measured the tensile force on a bar to be **F=10N** and the length and width of the bar to be **length=3mm** and **width=2mm**. A calculator will give the stress in the bar as **S=F/A=1.6667MPa**, but the actual answer is **2MPa**! Since each measurement was made only to a single significant figure, the answer cannot be known past this value. This isn't semantics or a trick question - it's simply stating the correct mathematics of the situation. 

The same logic applies to FEA. The results of the analysis cannot be known to greater precision than the input. If any of the inputs are assumed (in most uses of the software, most are), then the precision of the result is limited by these assumptions. Some assumptions and questions about the inputs that I personally have overlooked in the past include:
* At which temperature are the material properties evaluated?
* Are the materials being used truly isotropic, or does the grain structure based on the manufacturing method cause anisotropy?
* Is the mesh fine enough to capture gradients in the solution variable(s)?
* Will the part or assemblies under evaluation be manufactured to a tolerance that does not meaningfully influence the results of the analysis?
* Was there any conservatism when choosing the set of input loads used to perform the analysis?
* To what tensile force are the bolts being preloaded?
* Is the inefficiency in thermal contact conductance between mating parts accounted for?
* Are the boundary conditions truly fixed, or is there significant elasticity at the base of the structure?
* Are the mass properties of interfacing components included in the modal calculations?
* What is the residual stress remaining in the welds after fabricating a component and does this cause failure earlier than expected?

The bottom line is that engineering analysis constitutes an extremely contrived situation. Anyone attempting to make use of the results needs to understand the limitations of the information used to perform the calculations. Such limitations are not present in a simulation - but alas, engineering simulations do not yet exist. 



## References
[1] https://www.omnicalculator.com/math/sig-fig  
[2] https://phys.libretexts.org/Bookshelves/College_Physics/Book%3A_College_Physics_(OpenStax)/01%3A_The_Nature_of_Science_and_Physics/1.03%3A_Accuracy_Precision_and_Significant_Figures#:~:text=Accuracy%20of%20a%20measured%20value,agreement%20is%20between%20repeated%20measurements.

## Misc Notes
* Linear elastic analysis vs plasticity
* Damping and time stepping for dynamic analysis