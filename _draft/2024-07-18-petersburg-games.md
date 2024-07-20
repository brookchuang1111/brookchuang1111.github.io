---
layout: post
title: Gambling Addicts Love This One Game! The St. Petersburg Paradox 
tags: Game Theory
---
## Gambling Addicts Love This One Game! The St. Petersburg Paradox 

It's a Thursday night, 9:59 pm and I'm death-scrolling through Glassdoor reading through company snark written by some salty rejected interview candidate when I stumble on something interesting. Among a long rant of technical grilling, someone drops something called the St. Petersburg paradox. Huh, now what could that be? 

After looking through some articles and wasting a good hour of my life reading through the [correspondence of old dead farts](https://web.archive.org/web/20210414011124/http://cerebro.xu.edu/math/Sources/NBernoulli/correspondence_petersburg_game.pdf) (Nicolas Bernoulli and amalgamation of even older and stodgier men to be exact but that's neither here nor there), I'm reluctantly intrigued. 

Source material:
* [A Resolution of St. Petersburg Paradox](https://arxiv.org/pdf/2111.14635)

---

## The Game
The premise of the game is simple; given a fair coin, the payoff for flipping heads is two dollars, and the game ends. If we flip tails we get to flip the coin again, restarting the state of the game. If we flip the coin and it lands on heads, we get 4 dollars and leave the game. After each round, if we flip tails, our payoff doubles and we take home $2^k$ dollars for some $k$ rounds. 

*What should our buy-in for the game be?*
Our expected payoff is easy to calculate given that any heads or tails is $\frac{1}{2}$ and our reward doubles each time. Using the linearity of expectation we can add up each state of achieving payoffs for $k = 1, \dots, \infty$ rounds,

$$\mathbb{E} = \frac{1}{2} \cdot 2 + \frac{1}{4} \cdot 4 + \dots = \sum_{i=1}^{\infty}\frac{1}{2^i} \cdot 2^i = \sum_{i=1}^{\infty} = \infty$$  

If $X$ is the amount we are willing to pay for this game, our profit from this game would be $X - \infty = \infty$. The naive intuition of the game follows that only at the expected value of our profit, we should play the game at any price offered. 

Yet would one really sell their house to play such a game? 

### Using Utility Theory
The *optimal* utility is the largest expected utility. We can consider the linear utility that represents the payoffs $x$ of the game $u(x) = x$  and an affine utility function w.l.o.g. $u(x) = const + cx$ where $c$ is some monetary unit. 

Using the expected utility theory axioms, one can come to the utility of the lottery,
$$U_n = \sum_{m=1}^{n}u(2^m)\frac{1}{2^m} = n$$

The optimal utility then corresponds with $n=\infty$ tosses such that $U_{max} = U_\infty$ where $n \rightarrow \infty$. 

*Note: A quick recap of von Neumann-Morgenstern axioms*

There are four axioms of expected utility theory that represent a *rational* decision maker. 
1. **Completeness**: For every $A$ and $B$ either $A \preceq B$ or $A \succeq B$ or both[^1].
    * This means we want either A over B, B over A, or indifferent between the two
3. **Transitivity**: For every $A, B, C$ with $A \preceq B$ and $B \succeq C$ we must have $$A \preceq C$.
    * This means that our rational player chooses consistently.
4. **Independence of irrelevant alternatives**: For every $A, B$ s.t. $A \preceq B$ the preference $pA+(1-p)C \preceq pB + (1-p)C$ hold for every $C$ and $p\in{[}0, 1{]}$.
    * Given three choices with one being irrelevant, the ordered preferences of choices stay the same
6. **Continuity**: Let $A, B, C$ be lotteries with $A \preceq B \preceq C$. Then $B$ is equally preferred to $pA + (1-p)C$ for some $C$ and some $t\in{[}0, 1{]}$.
    * If the player prefers $A$ to $B$ and $B$ to $C$, there is a combiantion $A$ to $C$ where choice $B$ is indifferent between two relations.

---

## Generalizing the Game 
We can generalize the formulation of the Bernoulli game into a set of lotteries $\{L_n\}$ such that $L_n = \{x_1, p_1 {|} x_2, p_2 {|} \dots {|} x_n, p_n {|} 0, p_n\}$ with some $x_m$ payoff and it's characterizing probability $p_m$ [^2]. 

*The question now becomes, which lottery from the set of lotteries is optimal?*

With this generalization and the utility constructed, the optimal expected utility is $U_n = \sum_{m=1}^{n}u(x_m)p_m$. 

---

**Theorem 1** 

For each nonincreasing probability distribution $p_m$ there exists a nondecreasing utility function $u(x_m)$ such that the expected utility $U_n$ diverges as $n \rightarrow \infty$. 

*Proof*
We can define a utility function $\forall m > m*[^3], 

$$\frac{u(x_{m+1})p_{m+1}}{u(x_m)p_m} \geq 1$$

By the ratio test (hello AP calc!!)[^3] the sequence $\{U_n\}$ diverges as $n \rightarrow \infty$. $\square$

---

## Stochastic Decision Making 
Before we can look at the specific approach of the St. Petersburg Paradox, we have to analyze the idea of deterministic versus stochastic decision-making. These models are important for the specific perspective the paradox is solved under. 

### Tremble model 
The Tremble model is one of the simplest models within decision theory pertaining to probabilistic choice. In this model, individuals have a unique preference relation on the set of risky lotteries but they do not choose according to their preference all the time. 

A *tremble* occurs when an individual does not choose their preference with a probability of $p > 0$. With a probability of $1-p$ an individual acts in accordance with their preference. With a constant error model, this model fails as a general theory of stochastic choice. 

### Fechner model
The Fechner model allows individuals to have unique preference *relations* on the set of lotteries but reveal their preferences with a random error as a result of carelessness and insufficient motivation. This random error is drawn from a Gaussian distribution $\mathcal{N}(0, \sigma)$. 

When the utilities of choices are close, errors are more likely, unlike the Tremble model where error is constant. 

### Random Preference model 
The random preference model assumes that individuals have several preference relations over the set of risky lotteries and the probabilities of these choices. When choosing, individuals draw a preference relation and then choose an alternative that they prefer according to the selected preference relation. 

This model assumes that the individuals possess a probability measure that captures the likelihood of a lottery being chosen over other lotteries. In other terms, individuals have underlying deterministic preferences but how we choose from these preferences is random. The *mediator* is the distribution of the deterministic preferences. 

### Natural Stochasticy 
But at the end of the day, decision-makers never truly follow a deterministic model as decisions vary from different environments. Even with one decision, the brain processes with noise leading to random choice. This random choice causes variability. This variability causes choice inconsistent at repeated decisions. 

Pertaining to the Bernoulli game, the choice of the decision making is not deterministic and should be treated stochastically. Obviously from a theoretical approach, the buy-in for the game would be $\infty$, but because the player is human and is prone to this randomness from choice-making, we must use the idea of expected utility. *The crux of the St.Petersburg Paradox does not come from the game itself but from the application of the game to a deterministic preference criterion*. Therefore, we have to use a preferred criterion. 

## Probabilistic Preference Criterion 

A probabilistic preference criterion is characterized by the idea of having one choice being preferred over the other. THis manifests into three main principles:

1. 


[^1]: These [pringle-duck-lip-looking inequalities](https://math.stackexchange.com/questions/669085/what-does-curly-curved-less-than-sign-succcurlyeq-mean) are generalized inequalities and can represent partial orderings.

[^2]: We assume that the probability measure is normalized, $\sum_{m=1}^n p_m + p_n = 1$
[^3]: $m*$ denoting some critical index  




