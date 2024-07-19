---
layout: post
title: some witty title
tags: Game Theory
---
## 

Let me set the scene. It's a Thursday night, 9:59 pm to be exact, and I'm death scrolling through Glassdoor reading through semi-snark of salty rejected interview candidates when I stumble on something interesting. Someone comments about the St. Petersburg paradox. Huh.

This is how I've found myself reading the [correspondence of old dead farts](https://web.archive.org/web/20210414011124/http://cerebro.xu.edu/math/Sources/NBernoulli/correspondence_petersburg_game.pdf); Nicolas Bernoulli and amalgamation of even older and stodgier men to be exact but that's neither here nor there. What's interesting is that they seem to be squabbling over the St. Petersburg Game.

## The Game
The premise of the game is simple; given a fair coin,  the payoff for flipping heads is two dollars and the game is over. If we flip tails we stay and we get to flip the coin again, restarting the state of the game. If we flip the coin again and land on heads, then we get 4 dollars and leave the game. After each round, if we stay in the game, our payoff doubles and we take home $2^k$ dollars for some $k$ rounds. 

*What should our buy-in for the game be?*
Our expected payoff is easy to calculate given that any heads or tails is $\frac{1}{2}$ and our reward doubles each time. Using the linearity of expectation we can add up each state of achieving payoffs for $k = 1, \dots, \infty$ rounds,

$$\mathbb{E} = \frac{1}{2} \cdot 2 + \frac{1}{4} \cdot 4 + \dots = \sum_{i=1}^{\infty}\frac{1}{2^i} \cdot 2^i = \sum_{i=1}^{\infty} = \infty$$  

If $X$ is the amount we are willing to pay for this game, our profit from this game would be $X - \infty = \infty$. The naive intuition of the game follows that only at the expected value of our profit, we should play the game at any price offered. 

Yet would one really sell their house to play such a game? 

### Using Utility Theory
The *optimal* utility is the largest expected utility. We can consider the linear utility that represents the payoffs $x$ of the game $u(x) = x$  and an affine utility function w.l.o.g. $u(x) = const + cx$ where $c$ is some monetary unit. 

*Note: A quick recap of von Neumann-Morgenstern axioms*
There are four axioms of expected utility theory that represent a *rational* decision maker. 
1. **Completeness**
2. **Transitivity**
3. **Independence of irrelevant alternatives**
4. **Continuity**







