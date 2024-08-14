---
layout: post
title: "A Review of Cooperative Multiplayer Learning Bandits"
tags: [Bandits]
---
## A Review of Cooperative Multiplayer Learning Bandits

I think I already posted about multi-player bandits but I have to present this paper to my PI and I'm a little rusty - so a blog post should help me get through this meeting (fingers crossed). 
Source Material
* [Optimal Cooperative Multiplayer Learning Bandits with Noisy Rewards and No Communication](https://arxiv.org/abs/2311.06210)
---

### Bandit Setting
The paper centers around problem B of multiplayer bandit learning problems where rewards are iid within players and actions are observable. Each player receives a noisy version of a reward that can not be shared with other players.
Asymmetry follows as the information to select actions is not fully optimal at the get-go. 

Using the upper and lower confidence bounds, players can choose optimal actions despite this asymmetry in the reward information.

### Asymmetry Setting 
In the most classical setting of Stochastic Multi-armed bandits (MAB), there exists a single agent $m := 1, \dots, m$ where each action is associated with a round. 
In each round, the objective is to select an arm with the highest expected reward. The success of such a policy is measured by regret (where the suboptimal arm is pulled). 
With the UCB algorithm, we find the lower bound regret. 

While the classical setting is well established, it fails to concretely model the influence of one player onto another. This is called *information asymmetry* and it follows that *reward asymmetry* is present.
In this setting, agents do not observe rewards obtained by other agents. 

### mUCB-Intervals
It follows that we can create a variant of the classical UCB algorithm called mUCB-Intervals. By combining interval methods for best arm selection, applying to minimization tasks, and including coordination within the MAB setting, 
we find that a merry-go-around version of the UCB algorithm works well.  

The algorithm in summary follows:
- players decide on an ordering beforehand prior to learning
- during the process, they will pull this order
- they will maintain a desired set with all arms being present in the beginning
- this desired set will remain the same for all players each round
- based on the UCB intervals each player decides if an arm will be in the set or not

Note, that while there is no explicit communication in the environment, players can eliminate arms from a desired set given a player's actions to maintain the same desired set. 

### Preliminary
Consider a set of $M$ players $P_1, \dots, P_M$ which each player has a set of $\mathcal{K}_i$ of $K_i$ arms to pick from. 
The *joint action* of the players, ie their independent arm selection, is denoted by a $M$-tuple of arms $a = a_1, \dots, a_M$. 
The $N$ actions a player can pick from gives us a total of $K = N^M$ joint actions that generate $M$ iid random rewards, denoted $X^i_a \in 0, 1$ where i is 1-subgaussian distribution $F_a$ with a mean of $\mu_a$. 
Note that each player can only observe their rewards (reward asymmetry), but can observe actions. 

We denote $\Delta_a = \mu^* - \mu_a$ as the highest reward mean among all arm tuples, also known as the *optimal arm*. Players share the goal to pull the most optimal arm, 
ie to collectively identify the best set of arms $a$*$ corresponding to the mean reward $\mu^*$. 
TO capture the learning efficiency of such a process, we look at the expected regret, 
$$R_T = \mathbb{E}[T\mu^* - \sum^T_{t=1}X_{a(t)}(t)]$ where T is the number of learning instances and $X_{a(t)}(t)$ is the random reward if arm tuples $a(t)$ are pulled. 

The empirical mean $\hat{\mu_a^i}\eta_a(t)$ is indexed by player because since each player gets their own copy of the iid reward. 
Because the reward of each joint arm has the same mean among all players, the $R_t$ is the same for each player. 
The number of times joint arm $a$ is pulled, though, denoted $\eta_a(t)$ is not indexed by player since each player is contributing to the same joint action $a$ at every round. 

### Main Results 
To maximize the cumulative rewards, the players define the UCB index for each joint action (not just their own action) and try to pull arms with the highest UCB indices. 
This index is given by (2) and is indexed by player given the fact each player observes a different empirical reward mean. 
Using Hoeffding's bound, the true mean lies within the interval of (4). 

Note that when an arm is not pulled, we have an infinite interval that guarantees an arm be pulled at least once. 

Now proposing mUCB-Intervals:
- all players will maintain a desired set which contains the joint arms that are candidates for the optimal arm
- all players will agree before the learning process on an ordering for the joint actions in the desired set 
- at a particular round a joint action is called *considered* if the arm in the desired set pulled in that round (following order) is agreed upon

If there are $l$ joint actions, $c_1, \dots, c_l$ then the ordering of the desired set can be seen in flow chart (5). 
A joint arm is eliminated from this desired set if at some round $t$ a player $i$ observes the considered joint arm has a UCB internal that is below and disjoint from another arm. 
Player $i$ will "communicate" this elimination by not pulling the considered arm and eliminating it from its desired set. 

### Example 




