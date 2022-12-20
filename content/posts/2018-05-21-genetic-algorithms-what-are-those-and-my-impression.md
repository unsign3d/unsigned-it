---
template: post
title: Genetic Algorithms, what are those and my impression
slug: genetic-algorithms-what-are-those-and-my-impression
draft: false
date: 2018-05-21T12:44:00.000Z
---

## Genetic Algorithms, what are those and my impression

### **What is a Genetic Algorithm (GA) and why use it**

Let’s pretend that you have a problem in which you have **a set of constraints** and you want to find the maximum \[or minimum\] acheivable, this is one option.

One of the main advantages is that is **highly parallelizable**, so you can start with random (or less random) points in which you think that your solutions are good enough to be considered and then you find the perfect combination.

#### Structure of a GA

In a normal GA you have the following elements in play

**An individual**: the individual is responsible more or less to carry on his genes

**A population**: It’s a collection of individual

Some sort of **representation of the problem**, which includes:

*   **fitness funciton** (that gives a score to each individual)
*   selection of the **fittest couple** and the **unfittest individual**
*   **crossover** (mating) of the fittest couple and creation of the new individual
*   **mutation** of the individual in order to guarantee the variety of the population and not converge with an unoptimal solution

**An example of output from a simple GA**

> yarn run v1.6.0  
> $ ./node\_modules/.bin/babel-node ./src/basic\_structure/demo.js  
> The fittest individual score: 2 with genes: \[010100\]  
> The fittest individual score: 3 with genes: \[110100\]  
> The fittest individual score: 4 with genes: \[111100\]  
> The fittest individual score: 5 with genes: \[111110\]  
> The fittest individual score: 4 with genes: \[111100\]  
> The fittest individual score: 3 with genes: \[110100\]  
> The fittest individual score: 2 with genes: \[100100\]  
> The fittest individual score: 1 with genes: \[100000\]  
> The fittest individual score: 0 with genes: \[000000\]  
> The fittest individual score: 1 with genes: \[100000\]  
> The fittest individual score: 2 with genes: \[110000\]  
> The fittest individual score: 3 with genes: \[110001\]  
> The fittest individual score: 4 with genes: \[110011\]  
> The fittest individual score: 5 with genes: \[111011\]  
> The fittest individual score: 6 with genes: \[111111\]  
> Done in 1.02s.

In this simple case I wanted to find the candidate that score the most with a sum of boolean genes.

#### **Possible optimization in GA**

First of all, you can calculate the fitness score (which is the most time expensive computationally) in multiple cores or even machines, in this case the algorithm is highly parallelizable.

If the fitness function is strictly related to the genes you can cache it and see just the one from the individual that is newly born, but in this case, in a real world scenario, I would argue that you can find a better algorithm.

### My take on this algorithm

First of all, this is the easiest and more broad example of the evolutionary algorithms, so the judgment cannot be that harsh, it’s like judging A\*, it’s kinda pointless.

I think that if you take it isolated and you try to apply it to everything you fall under the A\* Manhattan problem in which, yes you can solve a lot of problems, but you probably have better tools and optimization. As in A\* Manhattan, this is a **easy and fairly accessible** algorithm that can put you in front of a category of problems and start from there.

This is article is heavily influenced by [this article](https://towardsdatascience.com/introduction-to-genetic-algorithms-including-example-code-e396e98d8bf3) on Medium.

I started a [project on Github](https://github.com/unsign3d/evolutionary_algo) with evolutionary algorithms in node js.