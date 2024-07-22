---
layout: post
title: " "
tags: Bandits
---
## 


Prerequisite Posts:
* []()
Source Material: 
* [Optimal Cooperative Multiplayer Learning Bandits with Noist Rewards and No Communicaiton](https://arxiv.org/pdf/2311.06210)

## Review of Regret and Reward
Although we looked at regret and rewards in *Beware of Bandits*, I'll reiterate some information that William has put in slightly different terminology compared to the *Bandits Bible*.  

**Joint Action**

Consider a set of $M$ players $P_1, \dots P_n$ in which player $P_i$ has a set of $\mathcal{K}$ of $K_i$ arms to pick from. At each round,  a player can pick an arm independently and simultaneously from other players from their set of $\mathcal{K}_i$. 
This joint action can be represented as a $M$-tuple of arms picked and denoted by $a = (a_1\dots a_M)$[^1]. 

This generates $M$ iid random rewards $X_a^i \in$[0,1] with $i \in$ [M] from a 1-subgaussian distribtuion $F_a$ with mean $\mu_a$. 

**Reward Asymmetry**

The idea that each player $P_i$ can only observe their rewards $X_i^a$ but are oblivious to all the other rewards is called *reward asymmetry*. Only after joint action is taken can they observe the actions of players. 
All players can determine a strategy and know the joint action space beforehand. However, during the learning process, they are not allowed to communicate. 

**Regret**

The *optimal arm* among all arm tuples is denoted as $\Delta_a = \mu*-\mu_a$ where $\mu*$ is the *highest reward mean*. The goal of these players is to pull the optimal arm as often as possible. 

Let $a_t(i) \in (1, \dots K_i)$ be the arm chosen by player $i$ at time $t$ and deonte $a_t = (a_t(1), \dots, a_t(m))$. 
For the players to pull the optimal arm, the high-level strategy is to collectively identify the best set of arms $a*$ corresponding to mean reward $\mu*$ given that they don't know the distribution or the means $\mu_a$. 
To do this, they must learn by *playing* and *exploring*. The learning efficiency can be represented as *expected regret*,

$$\tag{1} R_t = \mathbb{E}\Bigl( T\mu* - \sum_{t=1}^T X_{a(t)}(t) \Bigr)$$

$T$ is the number of learning instances and $X_{a(t)} (t)$ is the random reward if $a(t)$ is pulled. 
We let $\eta_a(t)$ be the *number of times joint arm* $a$ *has been pulled up* to but not including time $t$. Let $\hat{\mu_a^i}(\eta_a(t))$ to be the *empirical mean of arm* $a$ for player $i$ at time $t$ after $\eta_a(t)$ pulls the joint arm $a$. 
This empircal mean is indexed by the player since each get their own iid reward. In contrast, the regret $R_T$ is the same for each player because the reward for each joint arm has the same mean across all players [^2].
$\eta_a$ is not indexed by the player $i$ becuase each player contributes to the same joint action $a$ every round. 

**Note**:
While each player will likely have different rewards, the rewards are iid and the regret will therefore be the same across all players. 
This paper uses the the suggested lower regret bound $O(logT)$ for the multi-player decentralized learning algorithm with the same regret order. 

## Main Results

To maximize the cumulative rewards we define the *UCB index, also known as the Upper COndifence Bound for each joint action. The player's objective is to pull the largest UCB index as often as possible. For each player $i$ we can deifne the UCB index as,

$$\tag{2} \eta^i_a(t) = \begin{cases} 
      \infty & \text{if } \eta_a(t) = 0, \\
      \hat{\eta_a^i}(\eta_a(t)) + \sqrt{\frac{2log(1/\delta}{\eta_a(t)}} & \text{otherwise.}
   \end{cases}
$$

Let $\epsilon_a(\dots)$ be the constant added to the empirical mean for arm $a$ in calculating the UCB index. 
This constant is the same for every player and therefore not indexed by $i$. Our algorithm introduced further in the post wil be of length $2\epsilon_a(\dots)$. 
Because of this we add a tuning parameter $\gamma$ such that,

$$\tag{3} \epsilon(\eta_a, \delta, \gamma) := \gamma\sqrt{\frac{log(1\delta}{\eta_a}}$$

Using Hoeffding's bound for subgaussian variables, the true mean $\mu_a$ is within the interval

$$\tag{4} I_a^i = (\hat{\mu_a^i} - \epsilon_a, \hat{\mu_a^i} + \epsilon_a)$$


with high probability. We can use this confidence interval to create a set of arms that are likely to be optimal and to make this selection from this set. 
While this interval is different for each player $i$ given some joint action $a$ due to the empirical means $\hat{\mu_a^i}$ being different, $\epsilon_a)$ is not indexed by $i$. 


[^1]: Where $a$ is a vector.
[^2]: Expected regret does not actually depend on the value of the reward received but the differences in expected reward. 
[^3]: More on Hoeffding's inequality [here](https://en.wikipedia.org/wiki/Hoeffding%27s_inequality). 


