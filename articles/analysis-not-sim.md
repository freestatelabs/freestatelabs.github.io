---
title: Engineering Analysis is Not Simulation
parent: Articles
nav_order: 2
date: 2022-06-05
layout: default
---

# Engineering Analysis is Not Simulation
*5 June 2022*

Engineering analysis is not simulation. 

I've noticed this confusing terminology a lot, particularly among newer engineers or those unfamiliar with this type of work, so I wanted to address it here. 

The term *simulation* refers to a digital representation of the physical world. In particular, *simulation* conveys a sense of a perfect representation of the real, physical world in electrons on a computer. Think of *the Matrix* or the OASIS in *Ready Player One*. These simulations mimic reality so well that a user finds it nearly impossible to tell the difference. 

Engineering analysis does not do this. Engineering analysis converts a set of *assumptions* about reality into *expectations* of reality via a mathematical *model* of reality. **These assumptions and models are foundational to the results of engineering analysis.** 

Classic engineering analysis one-liners include:

>*The outputs are only as good as the inputs.*

>*Garbage in, garbage out.*

> *State your assumptions clearly and carefully.*

These types of slogans might sound dull and last-century to the current generation (my generation!) of engineers, but these concepts are so necessary for understanding what the calculations mean.

Of course, when I refer to 'engineering analysis', what I'm talking about are both finite element analysis (FEA) and classic closed-form calculations, i.e. hand calcs: **F/A**, **Mc/I**, etc. With a hand calc, it's immediately obvious that the calculation is based on a set of assumptions. With just a few scribbles on a paper or keystrokes in a spreadsheet, those inputs can be changed and the results seen immediately.  With finite element analysis, it's a different story.

FEA programs provide a level of ambiguity to the user. The user enters in the model information, including CAD data, mesh parameters, material information (this is a big one), loads, boundary conditions, and any other input data or settings necessary to produce a solution. Afterwards, the computer determines the answer and displays it to the user. In this case, the user must enter more data manually than that required for a hand calc, but the actual solution is itself, by and large, hidden behind the scenes. In most software today, this now appears to be a design choice.

This means that there are *many* more assumptions made in finite element analysis than a typical hand calculation! 

FEA software companies have recently (or perhaps always, I'm not old enough to really know) rebranded themselves as 'simulation' software providers. This is an attempt to establish credibility with their software tools at the cost of being somewhat misleading about their capabilities - in my opinion, a dangerous play. I've used multiple of these software packages extensively for critical applications such as ship, satellite, and nuclear reactor design. None of them is *anything* like a simulation. 

In physics labs in college, we painstakingly covered the procedures for determining the uncertainty of measurements. The quality of the measurement is dictated by the uncertainty of the instrument used to produce the measurement. For example, let's say you are performing an experiment on the number of calories contained in apples. But each apple you use for the experiment is not going to be exactly the same mass, so before performing the experiment, you need to measure each apple. If you use a scale that measures to the nearest kilogram (like one you might use for measuring cars and elephants), it will only tell you that each apple weights 0 or 1 kg. Neither of those measurements is accurate or useful! In this case, you might choose a scale that measures to the nearest gram or tenth of a gram.

In the same vein, the quality of an engineering calculation is determined by the accuracy of the input data and the uncertainty in the measurements of that data. Another example: let's say you measured the tensile force on a bar to be **F=10N** and the length and width of the bar to be **length=3mm** and **width=2mm**. A calculator will give the stress in the bar as **S=F/A=1.6667MPa**, but the actual answer is **2MPa**! Since each measurement was made only to a single significant figure, the answer cannot be known past this value. This isn't semantics or a trick question - it's simply stating the correct mathematics of the situation. 

The same logic applies to FEA. The results of the analysis cannot be known to greater precision than the input. If any of the inputs are assumed (in most uses of the software, most are), then the precision of the result is limited by these assumptions. Some assumptions and questions about the inputs that I personally have overlooked in the past include:
* At which temperature are the material properties evaluated?
* Are the materials being used truly isotropic, or does the grain structure based on the production method cause [anisotropy](https://www.tandfonline.com/doi/pdf/10.1179/1743284715Y.0000000118)?
* Is the mesh fine enough to capture gradients in the solution variable(s)?
* Will the part or assemblies under evaluation be manufactured to a tolerance that does not meaningfully influence the results of the analysis?
* Was there any conservatism when choosing the set of input loads used to perform the analysis?
* To what approximate tensile force are the bolts being preloaded?
* Is the inefficiency in thermal contact conductance between mating parts accounted for?
* Are the boundary conditions truly fixed, or is there significant elasticity at the base of the structure?
* What is the residual stress remaining in the welds after fabricating a component, and does this cause failure earlier than expected?

To be clear, though: modern engineering tools are amazing. They truly are. I am only presenting disagreement here based on marketing and perception. Engineering analysis software allows engineers today to far more accurately design novel buildings, vehicles, and devices on a time scale that dwarves the same efforts at any previous point in human history. We are truly pushing the limits of known physics using these tools, but they have their own limits as well.

The bottom line is that engineering analysis constitutes an extremely contrived situation. Anyone attempting to make use of the results needs to understand the limitations of the information used to perform the calculations. Such limitations are not present in a simulation - but alas, engineering simulations do not yet exist. 

-ryan