---
layout: post
title: Gambling Addicts Love This One Game! The St. Petersburg Paradox 
tags: Game Theory
---
## Gambling Addicts Love This One Game! The St. Petersburg Paradox 

Let me set the scene. It's a Thursday night, 9:59 pm and I'm death scrolling through Glassdoor reading through semi-snark of salty rejected interview candidates when I stumble on something interesting. Among a long rant of technical grilling, someone drops something called the St. Petersburg paradox. Huh, now what could that be? 

This is how I've found myself reading the [correspondence of old dead farts](https://web.archive.org/web/20210414011124/http://cerebro.xu.edu/math/Sources/NBernoulli/correspondence_petersburg_game.pdf); Nicolas Bernoulli and amalgamation of even older and stodgier men to be exact but that's neither here nor there. What's interesting is that they seem to be squabbling over the St. Petersburg Game.

## The Game
The premise of the game is simple; given a fair coin, the payoff for flipping heads is two dollars and the game is over. If we flip tails we stay and we get to flip the coin again, restarting the state of the game. If we flip the coin again and land on heads, then we get 4 dollars and leave the game. After each round, if we stay in the game, our payoff doubles and we take home $2^k$ dollars for some $k$ rounds. 

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
  
## Generalizing the Game 
We can generalize the formulation of the Bernoulli game into a set of lotteries $\{L_n\}$ such that $L_n = \{x_1, p_1 {|} x_2, p_2 {|} \dots {|} x_n, p_n {|} 0, p_n\}$ with some $x_m$ payoff and it's characterizing probability $p_m$. 

With this generalization and the utility constructed, the optimal expected utility is $U_n = \sum_{m=1}^{n}u(x_m)p_m$. 

**Theorem 1** 
For each nonincreasing probabiltiy distirbtuion $p_m$ there exists nondecreasing utility functions $u(x_m)$ that $\forall m > m*$ one has the inequality,

$$\frac{u(x_{m+1})p_{m+1}}{u(x_m)p_m} \geq 1$$

By the ratio test (hello AP calc!!) the sequence $\{U_n\}$ diverges as $n \rightarrow \infty$. 



[^1]:These [pringle-duck-lip-looking inequalities](https://math.stackexchange.com/questions/669085/what-does-curly-curved-less-than-sign-succcurlyeq-mean) are generalized inequalities and can represent partial orderings. 



