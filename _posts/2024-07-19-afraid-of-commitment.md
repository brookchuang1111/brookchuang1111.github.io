---
layout: post
title: "Afraid of Commitment: Understanding the Explore-then-Commit Algorithm"
tags: Bandits
---
## Afraid of Commitment: Understanding the Explore-then-Commit Algorithm

Now that we understand the basics of bandits, we can start exploring some basic algorithms that utilize the idea of regret and reward! The algorithm we'll be exploring is called the Explore-then-Commit algorithm (ETC). ETC is split into two phases: exploring and committing by playing each arm a fixed number of times and committing to that arm for the rest of the rounds. 

Note the prerequisite for this blog post:
* [Beware of Bandits!](https://brookchuang1111.github.io/2024/07/18/beware-of-bandits.html)

Source material:
* [Bandit Algorithms](https://tor-lattimore.com/downloads/book/book.pdf)
---
## The Algorithm 

For the rest of this post, we assume that all bandit instances are $\xi_{SG}^k(1)$ where the reward distribution for all arms is 1-subgaussian. The sub-gaussian distribution has strong tail decay and is characterized (in this context of bandits) by its variance proxy,

$$\mathbb{E}{[}e^{(X-E{[}X{]}t}{]} \leq e^{\frac{s^2t^2}{2}}$$

This property bounds the tails of the distribution implying that the random variable $X$ does not produce extreme outliers too frequently. For 1-subgaussian random variables, and in this context our reward distribution, this inequality holds for $\sigma = 1$. 

Ok sorry, let's get back to the algorithm. ETC is characterized by the number of times it explores each arm, denoted $m$. Because there are $k$ actions, the total number of times ETC explores is $mk$ rounds until committing. The *average reward* is denoted as $\hat{\mu}_i(t)$ such that, 

$$\hat{\mu_i}(t) = \frac{1}{T_i(t)} \sum_{s=1}^{t}I\{ A_s=i \}X_s$$

The term $T_i(t) = \sum_{s=1}^{t}T{A_s=i}$ is the number of times action $i$ has been played after round $t$ where ties are broken arbitrarily. The policy is given as:

---
1. ***Input*** $m$
2. In round $t$ choose action

$$\begin{equation*}
A_t = 
\begin{cases} 
(t \mod k) + 1 & \text{if } t \leq mk \\
\arg\max_i \hat{\mu_i}(mk) & \text{if } t > mk
\end{cases}
\end{equation*}$$

---

Given this, we can bound our regret given our suboptimality gap $\Delta_i = \mu* - \mu_i$ and mean reward $\mu_i$[^1].

**Theorem 2.1**

When ETC is interacting with any 1-subguassian bandit and $1\leq m \leq n{\}k$, 

$$R_n \leq m\sum_{i=1}^{k}\Delta_i + (n-mk)\sum_{i=1}^{k}\Delta_iexp(\frac{-m\Delta_i^2}{4})$$

*Proof:*
The proof is quite interesting but long so buckle up!
W.l.o.g. that the first arm is optimal. This means $\mu_1 = \mu*=max_i\mu_i$. By decomposing Lemma 1.4 $R_n= \sum_{a \in \mathcal{A}} \triangle _a \mathbb{E}{[}T_a(n){]}$ we have.

$$\tag{2.1} R_n= \sum_{i = 1}^k \triangle_i \mathbb{E}{[}T_i(n){]}$$

In the first $mk$ rounds the policy is deterministic (ie produces the same action each time because our first arm is optimal). Therefore, the single action chosen maximizes the average reward during the exploration phase,

$$
\begin{align}
\tag{2.2} \mathbb{E}[T_i(n)] &= m + (n - mk)\mathbb{P}(A_{mk+1} = i) \\
&\leq m + (n-mk)\mathbb{P}\Bigl( \hat{\mu_i}(mk) \geq max_{j \neq i} \hat{\mu_j}(mk)\Bigl)
\end{align}
$$

The probability on the right side is bounded by:

$$
\begin{align}
\mathbb{P}\Bigl(\hat{\mu_i}(mk) \geq max_{j \neq i} \hat{\mu_j}(mk)\Bigr) &\leq \mathbb{P}(\hat{\mu_i}(mk) \geq \hat{\mu_1)(mk)) \\
&= \mathbb{P}(\hat{\mu_1)(mk) - \mu_i - (\hat{mu_1(mk) - \mu_1 \geq \Delta_i)
\end{align}
$$


[^1]: Review these concepts [here](https://brookchuang1111.github.io/2024/07/18/beware-of-bandits.html)
