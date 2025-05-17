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
The first complexity notation which will be discussed is Big O, or Big Order, notation.  It is also called the theoretical upper-bound limit or the worst-case complexity.  When analyzing the runtime complexity of different algorithms, one of the most frequently considered is the worst-case performance to assess the scalability of the solution.  In other words, when looking at the scalability, we are interested in how many operations are being performed by the algorithm as the input size increases.  By assessing the worst-case scenario, there can be more confidence in asserting the scalability of the solution.  The question, "what is the most amounts of operations that this algorithm is going to perform?" can be answered by big-O notation.

Another way to think of big O notation is as a comparison between the growth of different functions.  As previously mentioned, there are many other factors which can impact how 'fast' in literal time it takes for the program to execute.  However, when looking at big O notation, the goal is to simplify the function as much as possible.  This would mean that, in practice, the environmental factors such as programming language or hardware is expressed in terms of constants.  By simplifying the expression of the functions, the constants can be dropped in order to assess the growth rates of the functions. So, for example the function:
$$ T(n) = 10000 + 10(n) $$
can be used to express a program which takes 10000 ms to load and 10 ms to execute each transaction.  Both the 10000 ms and 10 ms are reliant on factors outside of the algorithm itself.  These constants can change when improvements are made to the environment which is executing the program.  However the equation can be simplified to ignore the constants, giving us
$$ T(n) \in O(f(n)) $$
With the simplified run time, it becomes much easier to compare the performance of the algorithms.  This can allow us to have a more formal definition of what is big O.

> $$ T(n) \in O(f(n)) $$ if and only if $$ T(n) \leq cf(n) $$, where c is some constant

This definition shows that the focal point of the analysis would be set at the point at which the growth of $$ cf(n) $$ overtakes the growth of $$ T(n) $$.  It also establishes that big O is not necessarily just a quantity or a metric, but is more than that.  Big O describes the set of all functions which satisfy:

> There exists positive constants $$ c $$, $$ N $$ such that, for all $$ n \geq N $$, $$ T(n) \leq cf(n) $$
> where $$ N $$ is the point at which $$ T(n) \leq cf(n) $$

As shown, big O is mostly conserned with expressing the upper bound limit of a function, thus will not be revealing much on the lower bound.  This means that while it is possible to use big O notation to establish the higher performance of a function compared to another, it does not reveal the lower bound.  So to prove that the function is slower, another notation is needed (Omega (Ω)).

## Big Omega (Ω) Notation
While Big O measures the upper bound or worst-case performance of a function, Big Ω looks at the lower bound of the function.  This means that big omega notation would reveal the best-case performance of a function which means that the notation measures the function's minimal amount of runtime and space complexity.  Just as previously mentioned with big O, big Ω notation examines the set of possible functions to fit certain criteria.  To provide a more mathematical understanding of big Ω notation, the following definition can provide a baseline understandng:

> Given Two functions, $$ f(n) $$ and $$ g(n) $$, we can say $$ f(n) = Ω(g(n)) $$ if there exists constants $$ c \gt 0 $$ and $$ n_{o} \ge 0 $$ such that $$ f(n) \ge c\cdot g(n) $$ for all $$ n \ge n_{o} $$.

From the definition, we can gather that Ω notation provides the justification of whether a function $$ f(n) $$ will grow faster than another function multiplied by a constant, $$ c\cdot g(n) $$.  This establishes Ω notation as a reliable measure of the best-case performance of a function, or its lower-bound asymptotic growth.

The steps to defining the Ω notation of a functions goes as follows:
    1. Break the function into smaller, modular segments.
    2. Find the complexity of each segment.
    3. Add the constants together and drop the constants.

By following the steps, the Ω notation can be guarteed to establish the tight lower bound of the function, and give a good estimate of what the best case performance of the algorithm is.

While it can be very useful and revealing, big Ω notation is not frequently used to analyze the function's asymptotic growth compared to Big O notation.  The main reason for why the notation is not used is because the notation gives an accurate but imprecise measure of function performance.  For example, say we define a function such that:

```
function(input list: n, element)
    do
    compare (list[index] == element)
        true -> stop
        false -> continue
```

In other words, the defined function will perform a linear search on an input and stop once the matching element is found.  The best case performance for the algorithm can be O(1), since the first element encountered can come as a match.  However, this is not necessarily precise since the algorithm will not perform in constant time most of the time.  For this reason, big Ω notation is not used frequently to analyze and compare algorithmic performance due to its imprecise nature.

## Big Theta (Θ) Notation
While big O returns the upper-bound and big Ω returns the lower-bound of the function, big Θ returns the average growth of the function.  Also, big Θ returns more precise results compared to big Ω due to the average case needing to compute the upper and lower bounds of the function.  The definition of big Θ notation goes as follows:

> Let g and f be functions, f is said to be Θ(g) if there are two constants $$ c_{1}, c_{2} \gt 0 $$ and a natural number $$ n_{0} $$ such that $$ c_{1} \cdot g(n) \le f(n) \le c_{2} \cdot g(n) $$ for all $$ n \ge n_{0} $$.

In other words, if a function f is Θ(g), the values of f will be encased between the function g(n) multiplied by two constants, $$ c_{1} $$ and $$ c_{2} $$.  This guarantees that the Θ notation will give the average case of the function.  So by providing the upper and lower bounds of the function, the notation can find the average case complexity of the function.  This precise measure can be useful as well as powerful when analyzing the asymptotic growth of the function.

To find the average complexity of the function, the high level overview of the steps are similar to finding the Ω notation with several differences:
    1. Break the function into smaller segments.
    2. Find all possible inputs for the algorithm.
    3. Calculate the amount of operations that can be performed on the input.
    4. Divide the amount of operations by the number of segments to find the average of all complexities.

*So, if Θ notation encapsulates both upper and lower bounds, why isn't it mentioned more frequently?*  Might be a question that may be asked.  This is because, as algorithms become more complex, it becomes more difficult to be able to find all possible inputs and then calculate the operations.  In this case, many will default to using big O notation to find the upper-bound limit of the function's asymptotic growth.  While Θ notation is precise, it can be a complex process to be able to return any useful information from analysis, so big O notation is more applicable in this scenario since it reveals more than Θ notation.

# Common Runtimes of Algorithms
![Graph of growth rates](/assets/img/asymptoticgrowths.png "Graph of complexities")

From this point, the runtimes that will be discussed will mainly be in big O, due to the frequency of its use.  When discussing different runtimes, the default which is used is big O notation.  While there are many different runtimes, the most common run times are factorial, exponential, polynomial, linear, and constant.  These all describe asymptotic growth patterns of different algorithms into 5 general categories of runtimes.  This allows programmers to compare the efficiency of different solutions by supposing an infinite or progressively larger input size.  These aren't only used to analyze runtime, they can also be used to analyze space-time complexity.  Space-time complexity measures how well a solution works with memory, assessing whether it is efficient or a horrible use of memory.  It is generally accepted that complexities which are exponential and factorial scale very badly, whereas solutions in polynomial, linear, or constant time scale very well.

## Factorial
This is considered the worst possible complexity.  This general set of solutions run at a complexity of O(n!), hence the name.  These solutions are extraordinarily terrible to scale as demonstrated in the above graph relative to other complexities.  One of the important aspects to notice is the near immediate increase in the amount of operations which is performed by the solution.  Most solutions which fall within this category of complexity are generally considered extraordinarily innefficient and impractical.  However, there can be instances where factorial runtimes can be useful, such as proposing a brute-force solution to an unsolved problem.
Examples of algorithms with factorial runtimes include:
* Travelling salesman (Brute force)
* Generating all possible permutations of a set
* Password cracking (Brute force)
* Bogosort

Each of the previously mentioned algorithms are brute force algorithms which try every possible combination until the solution is reached.  For instance, bogosort is a simple two step solution which takes an input which is comprised of elements which can be sorted and randomly shuffles the elements until they are confirmed sorted.  As such the algorithm can be broken down into two segments, where the shuffling of elements create O($$ n! $$) runtime and the confirmation of whether the elements are sorted reveal an O($$ n $$) runtime.  By combining these runtimes, we get O($$ n! + n $$) upper bound, or O($$ n! $$).
As previously mentioned, these algorithms are considered generally useless due to its impractical nature when it comes to scaling.  However, the importance of solutions with factorial runtimes is due to the problem being novel and, normally, there not being any previously established solution.  It is encouraged to try and find a more efficient solution to allow for its nature to be practical in the context of 'the real world'.

## Exponential
While somewhat an improvement from factorial, exponential runtimes are still very terrible at scaling and still encompass some brute force solution.  On the above graph, the asymptotic complexity is shown to grow faster than all other runtime complexities on the graph other than factorial.  Exponential solutions scale upwards at a rate of $$ n^n $$, hence its big O complexity is notated O($$ n^n $$).
Some examples of algorithms that have exponential runtimes include:
* Naive solution to the n-queens problem
* Generating the Fibonacci sequence (recursive)

Each of the previous algorithms approach the problem in an naive way and is still considered generally impractical due to its inability to scale to be applied to larger sets.  For example, when solving for the n-th Fibonacci number recursively, the algorithm returns the solution by first generating a recursion tree from a base case of 1.  The function calls are then pushed onto a callstack and then popped to return the solution.  One of the most important characterstics of this runtime is that it encompasses naive approaches just like factorial solutions.  This means that while the solutions may be hard to apply to larger inputs, the importance of improving upon an naive solution like the previously mentioned solutions should not be dismissed.

## Polynomial
Polynomial runtimes, generally notated as O($$ n \cdot log(n) $$) but officially defined O($$ n^k $$), are the first set of functions and solutions which are considered practical for larger sets.  Also, the runtime O($$ n^2 $$) is considered its own category, quadratic, despite the runtime seemingly mapping to exponential runtime.  Algorithms with quadratic runtimes are also considered poloynomial, so they can be defined as a subset of solutions which have polynomial runtimes.

The set of functions which have polynomial runtimes can scale well as the input size increases relative to exponential and factorial growth rates, as seen in the graph above.  There are plenty of different sorting algorithns, string parsing solutions, backtracking solutions, etc. which can have a polynomial runtimes.  More familiar examples of algorithms which are considered polynomial time inclulde the operations used in arithmetics such as addition, multiplication, division, and subtraction.

Polynomial runtimes are considered "fast" and are frequently encountered within the area of algorithmic analysis, due to its smoother growth rate relative to the other previously mentioned growth patterns.

## Linear
One of the introductory searching algorithms that computer science students are shown is the linear search.  The linear search algorithm is very simple:
```
Input: A list of elements, element to find

1. Start at the beginning entry
2. Compare the element to the input element to see if they are matching
3. If match: Return the index of the matched element
   If not matched: Continue to the next index
```
This is an example of an algorithm or solution which has a linear, or O($$ n $$), worst case runtimes.  The reason is because as the input size grows, the worst case scenario is for the algorithm to not find any matches within the list.  In this case, it will traverse the entire list and return false.  With this understanding, there are other examples of solutions which run in linear time which might be as intuitive as linear search:
* Deleting and item from a linked list
* Checking if a string is a palindrome

Algorithms which run in linear time are considered very fast, however can lead to problems when the input size increases to larger amounts.  Generally, linear searches perform worse when the list size begins to increase to larger sizes.

## Constant
Functions which run in constant time are considered the best since it will take the same amount of time to execute the solution, no matter how large the size is.  Often denoted as O(1), there are different examples of solutions which run in constant time.  For example, if we are given an indexed list such as an array, returning an element in the array based on the index would run in constant time.  The idea being, if there was an indexed list of elements, returning the seventh element of the list would take about the same amount of time no matter the size of the list whether it is 10, 100, or 1000 elements large. Some examples of well-known indexed lists include:
* Hash maps
* Arrays
* Databases

All of these can be ideal if the goal is to store and retrieve the elements frequently.  Execution of a retrieval function would not take long and would not change as the input size increases.  This can allow for the solution to offer a mechanism of consistency within runtime complexities.