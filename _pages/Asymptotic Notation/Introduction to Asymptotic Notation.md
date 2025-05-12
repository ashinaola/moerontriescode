---
title: "Introduction to Asymptotic Notation"
date: "2025-05-12"
bookmark: true
thumbnail: "/assets/img/thumbnail/bigograph.jpg"
---
> "The key to performance is elegance, not batallions of special cases."
> Doug Bently and Jon Mcllroy

When thinking about software, there are different components which can work together to create a tool which can help users organize and retrieve large stores of information.  Programmers use a variety of tools to measure the performance of the algorithm which drives the solution.  The basket of tools that are deployed to measure performance of the program depends on the attribute that is being assessed (such as user friendliness, data integrity, etc.). However, the attribute that will be discussed is the theoretical performance of what powers the solutions.  So while there are many different ways to determine whether the software meets the requirements of the users, the focus will fall mostly on the assessment of the runtime and spacetime complexities of the solutions.

# How to Assess Performance of Programs
There are different variables which may impact the runtime performance of programs which include environmental factors such as hardware.  However, when dealing with algorithms, it would be ideal to ignore those environmental factors and focus on comparing the number of operations that the algorithm will perform on the input.  By not taking hardware into account, we can see the limitations of the algorithms that are being compared.  To put it into better wording, an inefficient algorithm being executed in a modern computing environment may be able to achieve seemingly better results than an effecient algorith being executed in an legacy computing environment.

To better assess the performance of programs, different notations are used to gain a better understanding of the theoretical limits of the algorithms.  'Big O' notation is used as a means to gain a general idea of the worst-case performance or upper-bound limit of the algorithm.  'Big Theta' notation is encased between Big O and Big Omega notations, giving the average complexity of the algorithm.  And as previously mentioned, 'Big Omega' sits below Big Theta, giving the lower-bound limit or best-case performance of the algorithm.  

## Big O Notation
The first complexity notation which will be discussed is Big O notation.  It is also called the theoretical upper-bound limit or the worst-case complexity.  When analyzing the runtime complexity of different algorithms, one of the most frequently considered is the worst-case performance to assess the scalability of the solution.  In other words, when looking at the scalability, we are interested in how many operations are being performed by the algorithm as the input size increases.  By assessing the worst-case scenario, there can be more confidence in asserting the scalability of the solution.  The question, "what is the most amounts of operations that this algorithm is going to perform?" can be answered by big-O notation.

## Big Theta (Θ) Notation

## Big Omega (Ω) Notation

# Common Runtimes of Algorithms

## Factorial

## Exponential

## Polynomial

## Linear

## Constant