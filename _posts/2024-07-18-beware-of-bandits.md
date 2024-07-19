## Beware of Bandits! 
### Stochastic Bandits and Their Assumptions 

Welcome to my first-ever blog post! The research I'm currently doing under UCLA's math department heavily revolves around stochastic bandits and related algorithms.
In this post, I'll hash over bandits, their properties, and some important assumptions we'll decompose under. 
<br><br>
Most of what I'm learning and the material I regurgitate comes from a holy grail book some affectionately coin as the [*Bandit Bible*](https://banditalgs.com). 
Written by Tor Lattimore and Csaba Szepesvari, this book encompasses everything you need to know about bandit algorithms. However, as a cheeky plug, if you would like a shortened version with my annotations I reference when reviewing, keep on reading!
<br><br>
> *An old bandit adage: A bell is a cup until it is struck.*
> 
> Colin Meloy
---
### Core Assumptions
#### Definition: Stochastic Bandits 
A stochastic bandit is a collection of distributions $\mathcal{v} = (P_a:a \in \mathcal{A})$, where $\mathcal{A}$ is the set of available actions. In this environment, we have two players: the learner and the environment. In this ecosystem the following actions and states exist: 

* In an environment there are $t$ rounds such that $t \in \{ 1, \dots, n \}$.
    - The *horizon* n, or total encompassing rounds, is finite (sometimes we allow $n=\inf$). 
* On each round a learner chooses an action $A_t \in \mathcal{A}$.
* The environment then samples a reward $X_t \in \mathbb{R}$ from distribution $P_{A_t}$ and reveals the reward $X_t$ to the learner.
* This interaction between learner and environment induces a probability measure on a sequence of outcomes $A_1, X_1, \dots, A_n, X_n$.

We also impose some assumptions on our environment: 
1. The conditional distribution of reward $X_t$ given our sequence of outcomes is $P_{A_t}$. Intuitively this makes sense as we sample our reward from $P_{A_t}$ in some round $t$. 
2. Our action $A_t$  the player chooses from $\mathbb{R}$ is $\pi_t(\cdot |A_1, X_1, \dots, A_{t-1}, X_{t-1})$[^1]. $\pi_t$ where $t \in \{ 1, \dots, n \}$ is the sequence of probability kernels that characterize the learner.

$\pi_t$ is essentially the function that provides the probability distribution over $A_t$ given some past action sequence $A_1, X_1, \dots, A_{t-1}, X_{t-1}$. Think of $\pi_t$ as the describing function that characterizes how the learner decides on an action at round $t$ based on historical rounds. 

### The Learning Objective
Like any good self-optimizing student, the goal of the learner is to maximize the reward $X_t$ across the horizon $n$. This is a random quantity that depends on the interaction between the environment and player and interestingly enough is NOT an optimization problem. Why?

1. Maximizing rewards is a process built on incomplete information. We don't know the value of $n$ rounds we will need.
2. Our reward value itself is random.
3. Our distributions that govern each reward is unknown.

So basically we know nothing...right? Well like everything in math, we can scoot some things around to adapt to this lack of information. To do this, we construct a *policy* that assumes this loss of information and *proves* that this loss is minimal anyway. 

But to assign utility[^2] to our distirbutions of $S_n = \sum _{t=1}^{n} X_t$ is harder. By convention, we choose the *largest expected value of the reward distributions*[^3]. 


[^1]: This dot represents a variable which the probability distribution is defined on. We replace this with any given specific action. 
[^2]: The utility of a function is the outcome of our probability distribution (ie. our preference for one reward over the other).
[^3]: Exceptions like variance and tail behavior are analyzed later. In general, this convention holds. 

