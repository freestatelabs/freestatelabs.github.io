---
layout: page
title:  "Conclusions"
date:   2024-01-10 
parent: wired-benchmarks
permalink: /wired-benchmarks/conclusions
katex: true
nav_order: 5
---

[<< Julia Implementation](/wired-benchmarks/julia)

## Julia is *Really* Fast 
My original Julia code was not very fast, but the final product is! It outperforms
its nearest competitor by about 2x - a result that really impressed me, given the
slow start I had. It turns out that writing code in Julia really doesn't 
sacrifice speed or convenience. 

## Use the Right Tool for the Job
Speed isn't everything here. Python, C, and even Fortran have their uses for 
certain applications, as well. If I want to distribute the code as an executable 
or as part of a larger end-user application, I'd write it in C rather than Julia: I can compile it
in advance without the user needing a Julia installation, and its performance is 
still pretty good. Python is widely used everywhere, especially in scientific computing, 
so it has a very large user base compared to Julia. Perhaps the end users of the code 
don't want to or can't switch to Julia, and that's my problem, not theirs. 

For my library, though, Julia seems to be the right choice. It's really efficient, 
it's easy to write, debug, and test, and working out of the REPL is a natural choice 
for supporting scientific calculations. 

## Redoing the Same Thing a Bunch of Times in Different Ways Can Be Pretty Hard 
This project took *far* longer than I anticipated. Part of the problem was that I
wrote the same code again and again, slightly differently, in four very different 
languages. The core algorithm is pretty straightforward (a few vector operations 
inside a pair of `for` loops!), but eking out the best possible performance across 
a variety of languages was a lot to keep up with. In total, I think I rewrote the
same algoithm about 25-30 separate times! In the future, I'm definitely 
just going to stick with one implementation, if I can.

## Writing Efficient, Optimized Code is Important
There's a lot of talk in the software world (and in a different way, the hardware world, too) 
suggesting that writing fast or efficient code is a waste of time.   

*Just write an algorithm that works and throw more cores at it! Developers' time 
is far more valuable than compute time!*  

I've always struggled with this idea, because it feels so lazy. I get the business 
case - an engineer's time is very expensive compared to waiting a little longer for the
program to finish running - but its a wasteful mindset and shouldn't be applied across the 
board. If you write an inefficient program, doesn't that mean that you really didn't do 
the best that you could? If you didn't optimize it, do you *really* know how it works?
Again - speed isn't everything - but efficient algorithms tend to be the ones 
that produce fewer errors and are easier to maintain, too. 

I learned a lot by forcing myself to optimize my code and view it from the perspective 
of other languages, and I'm going to keep doing this in the future. 