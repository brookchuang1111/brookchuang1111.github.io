---
layout: post
title: Beware of Bandits! Stochastic Bandits and Their Assumptions 
tags: Bandits
---
## Beware of Bandits! Stochastic Bandits and Their Assumptions 

(Proceed with caution: This was my first post and honestly is pretty shit, but I'm attached so I can't archive it.)

The research I'm currently doing under UCLA's math department heavily revolves around stochastic bandits and related algorithms.

Much of what I synthesize comes from the holy grail text some affectionately coin as the [*Bandit Bible*](https://banditalgs.com). Written by Tor Lattimore and Csaba Szepesvari, this textbook is widely regarded as as a ground up manual and gateway into bandits research.  

> *An old bandit adage: A bell is a cup until it is struck.*
> 
> Colin Meloy

---

### Core Assumptions

  <div style="display: flex; justify-content: space-between;">
  <div style="text-align: center;">
    <img src="https://github.com/brookchuang1111/brookchuang1111.github.io/raw/main/post_assets/Bandit.jpg" style="width: 100%; height: 300px; object-fit: cover;">
    <p>A different kind of "Bandit"</p>
  </div>
</div>


#### Definition: Stochastic Bandits 

A stochastic bandit is a collection of distributions $\mathcal{v} = (P_a:a \in \mathcal{A})$, where $\mathcal{A}$ is the set of available actions. In this environment, we have two players: the learner and the environment. In this ecosystem the following actions and states exist: 

* In an environment there are $t$ rounds such that $t \in \{ 1, \dots, n \}$.
    - The *horizon* n, or total encompassing rounds, is finite (sometimes we allow $n=\infty$). 
* On each round a learner chooses an action $A_t \in \mathcal{A}$.
* The environment then samples a reward $X_t \in \mathbb{R}$ from distribution $P_{A_t}$ and reveals the reward $X_t$ to the learner.
* This interaction between learner and environment induces a probability measure on a sequence of outcomes $A_1, X_1, \dots, A_n, X_n$.

We also impose some assumptions on our environment: 
1. The conditional distribution of reward $X_t$ given our sequence of outcomes is $P_{A_t}$. Intuitively this makes sense as we sample our reward from $P_{A_t}$ in some round $t$.
  
2. Our action $A_t$  the player chooses from $\mathbb{R}$ is $\pi_t ( \cdot \| A_1, X_1, \dots, A_{t-1}, X_{t-1})$ [^1]. $\pi_t$ where $t \in \{ 1, \dots, n \}$ is the sequence of probability kernels that characterize the learner.

$\pi_t$ is essentially the function that provides the probability distribution over $A_t$ given some past action sequence $A_1, X_1, \dots, A_{t-1}, X_{t-1}$. Think of $\pi_t$ as the describing function that characterizes how the learner decides on an action at round $t$ based on historical rounds. 



### The Learning Objective

Like any good self-optimizing student, the goal of the learner is to maximize the reward $X_t$ across the horizon $n$. This is a random quantity that depends on the interaction between the environment and player and interestingly enough is NOT an optimization problem. Why?

1. Maximizing rewards is a process built on incomplete information. We don't know the value of $n$ rounds we will need.
2. Our reward value itself is random.
3. Our distributions that govern each reward is unknown.

So basically we know nothing...right? Well like everything in math, we can scoot some things around to adapt to this lack of information. To do this, we construct a *policy* that assumes this loss of information and *proves* that this loss is minimal anyway. 

But to assign utility[^2] to our distirbutions of $S_n = \sum _{t=1}^{n} X_t$ is harder. By convention, we choose the *largest expected value of the reward distributions*[^3]. 



### The Regret

  <div style="display: flex; justify-content: space-between;">
  <div style="text-align: center;">
    <img src="https://github.com/brookchuang1111/brookchuang1111.github.io/raw/main/post_assets/no_regrets.jpg" style="width: 100%; height: 300px; object-fit: cover;">
    <p>No Regrets!</p>
  </div>
</div>



Unlike the tattoo artist in the above Snickers commercial, bandit's have regrets! Many of them to be precise. Regret is a central principle of bandits and is how we measure the performance of bandit algorithms. In the most basic terms regret is the deficit suffered by the learner relative to the optimal policy. If, by earlier definitions, $\mathcal{v} = (P_a: a \in \mathcal{A})$ is a stochastic bandit, then we define our *expected or mean reward*[^4] given $P_a(x) as

$$\tag{1.1}
\mu_a(\mathcal{v}) = \int_{-\infty}^{\infty}xdP_a(x)$$

The regret of policy $\pi$ on bandit instance $\mathcal{v}$ is 

$$\tag{1.2}
R_n(\pi, \mathcal{v}) = n\mu*(\mathcal{v}) - \mathbb{E}[\sum_{t=1}^{n}X_t]$$

The regret after $n$ time steps over the policy $\pi$ and bandit instance $\mathcal{v}$ is
* $\mu*(\mathcal{v})$: the *optimal reward term*
* $\mathbb{E}[\sum_{t=1}^{n}X_t]$: the *total expected reward*

Here's some boring stuff I have to include because... *math*.


**Lemma 1.3**

* $R_n(\pi, \mathcal{v}) \geq 0$ for all policies $\pi$
* the policy $\pi$ choosing $A_t \in argmax_a\mu_a$ for all $t$ satisfies $R_n(\pi, \mathcal{v}) = 0$
* if $R_n(\pi, \mathcal{v}) = 0$ for some $\pi$ then $\mathbb{P}(\mu_{A_t} = \mu*) = 1 \forall t \in [n]$



### Decomposing the Regret

Now let's introduce the *suboptimality gap*, also known as the *action gap* or *immediate regret* of action $a$, 

$$\tag{1.3}
T_a(t) = \sum_{s=1}^{t}I(A_s = a)$$

We interpret $T_a(t)$ as the number of times action $a$ is chosen by the learner after the end of round $t$. $A_t$ inherits randomness from past observational randomness. 

Now let's look at the dependence of the various quantities of policy $\pi$ and the environment $\mathcal{v}$ is suppressed seen in Lemma 1.4. 


**Lemma 1.4**

For any policy $\pi$ and stochastic bandit environment $\mathcal{v}$ with countable $\mathcal{A}$ and horizon $n \in \mathbb{N}$ the regret $R_n$ of policy $\pi$ in $\mathcal{v}$ satisfies,

$$\tag{1.4}
R_n= \sum_{a \in \mathcal{A}} \triangle _a \mathbb{E}{[}T_a(n){]}$$

This regret decomposition decomposes regret in terms of loss due to using each of the arms. This tells us that to keep the regret small the learned should aim to use an arm with a larger suboptimality gap fewer times (sorta like "learning from its mistakes"). For the most optimal arm, suboptimality gaps are zero. 

---
Now you know the bare bones of stochastic bandits! From how we formally define bandits to the introduction of decomposing regret, we can now explore more complex and accurate algorithms and their bounds, as well as create new bounds with different environments and bandit parameters.

[^1]: This dot represents a variable on which the probability distribution is defined. We replace this with any given specific action. 
[^2]: The utility of a function is the outcome of our probability distribution (ie. our preference for one reward over the other).
[^3]: Exceptions like variance and tail behavior are analyzed later. In general, this convention holds. 
[^4]: We assume that the mean reward is finite and the $argmax_{a \in \mathcal{A}}$ is non-empty.

