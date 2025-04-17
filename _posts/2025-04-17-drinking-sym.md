---
layout: post
title: "Drinking Symmetrically: A study on Catalan numbers"
tags: Math 
---
## Not That One! 

Over winter break, I opened the kitchen fridge to see, on the middle shelf to the left, two lines of LaCroix. The left most can was a guava while the flavor besides it was key lime. I certainly knew my choice, but as I reached towards my preferred flavor (key lime of course), I heard a screech in my ear. 

*"Don't pick that one!"*

It was my brother who was also home for winter break. I rolled my eyes - attributing his diva-ness to the fact that he had to spend the better part of the year in wintery New Jersey hell, but he knocked my hand aside and pointed to the pink guava can, screeching in his superior holier-than-thou-tone (paraphrased because I filter out most of what he says anyways), 

*"You have to drink it symmetrically - you see the guava one has an extra can. You're going to drink all the key lime and I won't have any options to choose from!"*

What in the world...drink symmetrically? Anyways, its not like you could taste the flavors in LaCroix. Maybe whatever he tasting was the byproduct of the chemical imbalance (more like illness) corroding his brain. 

I made sure he sashayed away before I reached for the *other* can and flung myself on the couch. Cracking open the tab, I took my first sip and cheered myself to the liberation from the carbonated water police.

Even so, his slight OCD proposed a rather interesting question. How many times could I get away drinking asymmetrically without him ever noticing, ie. always having two unique drink flavors left for him? Did the count of each flavor contribute to the probability of me being yelled at? How many ways could my brother and I drink LaCroix such that there would always be more guava? Could I say the same for key lime? 

And herein I introduce the topic of this post - a stupid real life application of very non-stupid combinatorics principles that involve counting valid sequences of drawing drinks. I hope you enjoy this exercise of my free will. 

<figure style="display: flex; flex-direction: column; align-items: center;">
  <img src="/assets/2025_04_17/allegory_cave.png" alt="cave" width="400">
  <figcaption>Allegory of the cave...LaCroix edition</figcaption>
</figure>

## The LaCroix Problem  

**The Problem Statement**
- How many valid permutations of drawing an equal number of pink (guava) or green (key lime) cans will result in the last two cans being unique flavors given we always have more pink cans, $\mathcal{P} > \mathcal{G}$?
  
*Variations*: 
1.  What if I loosened the inequality to $\mathcal{P} \geq \mathcal{G}$? 
2. What if I drank multiple green cans per visit to the fridge? 
3. What if I completely scrap the restrictive inequality such that I only care that the last two drinks are green and pink?
  
For a simple combinatorics exercise, let's calculate the total number of sequences without any restrictions. Let's say I have six green cans $(\mathcal{G})$ and six pink cans $(\mathcal{P})$. Drawing all 12 is a permutation of uniquely ordering either the six cans in $\mathcal{G}$ or $\mathcal{P}$. Therefore the total number of ways to arrange these is with a simple 12 choose 6, 

$$
\text{Total Sequences } = {12\choose6} = \frac{12!}{6!6!} = 924. 
$$

To aid our journey of solving our LaCroix problem, it's useful to be able to geometrically visualize our permutations. Without further ado, let me introduce lattice walks. 

### Lattice Walks 
Our counting of total sequences can be visualized with a lattice walk where each step (reaching for a drink) represents either or of a flavor. This can be visualized by a 6x6 grid for our six green and six pink cans where moving horizontally represents choosing $\mathcal{P}$ while moving vertically represents choosing $\mathcal{G}$. Counting such lattice walks so we reach $(6, 6)$ (or any arbitrary cartesian point we assign to each grid intersection) is represented by how many ways we can travel right $x$ times and up $y$ times. Our linear line $y=x$ represents the balanced count between flavors; each vertex of our path touching the line symbolizes equal counts of pink and green cans for that given step. 

<figure style="display: flex; flex-direction: column; align-items: center;">
  <img src="/assets/2025_04_17/lattice_walk.png" alt="lattice_walk" width="350">
  <figcaption>Figure 1: Representation of a drinking permutation as a lattice walk</figcaption>
</figure>

Intuitively we know we have drank symmetrically if we reach $(5,5)$ of our lattice walk. We can observe, under a prior step, that five pink and five green cans have been consumed, leaving us with one pink and one green can left. We can further analyze these patterns, but first I need to introduce some foundational building blocks of paths.

## An Introduction to Catalan Numbers 
Lattice paths allow us to enter a peculiar world. Visualizations of sequences into paths start as a generalized lattice but can morph into complex and elegant representations of different path dynamics under $y=x$. These paths, which will help us efficiently count our LaCroix problem, are built upon Catalan numbers[^1]. But first, let me introduce you to Dyck paths and an arsenal of propositions that will help us build intuition. 

**Dyck Paths**
A Dyck path is a lattice path that doesn't cross the lime of $y = x$ from below. A visual representation can be seen in our drink path in figure 1. 

In addition to Dyck paths I'll introduce some propositions that you'll convince yourself are factual; you can take my word for it or look at this heinous 113 long slide deck [^2]. 

**Lemma 1.** For any $m$ and $n$ there are ${{m+n}\choose{m}}$ lattice paths from $(0,0)$ to $(m, n)$ in the mxn grid. 

*Proof.* We can easily see this by flattening the dimensionality of the problem. Imagine the sum $m+n$ as a row of slots. In each slot we have six green and six pink chips to enter in any particular order. Hence for any six green chips the complement of the other six pink chips in inevitable. Hence 12 choose 6. 

**Proposition 1** The lattice paths in a nxn grid that cross the line $y=x$ are in bijection with the lattice paths in the $(n-1)$x$(n+1)$ grid. 

*Proof.* Let $Q$ be the lattice path in the $(n-1)$ x $(n+1)$ grid and $P$ of the nxn grid. We can construct $Q$ as the same as $P$ up to a certain point $p$. After $p$ let us denote this path $Q_p$ and swap path $P$ directions for every step for $Q_p$'s path. We can see that $Q$ has $n-1$ east steps and $n+1$ north steps. For $P$ there must be n east and n north steps, hence, there must be exactly one more east step than north steps after $p$. This intuition is classically called the Andre Reflection Method[^3]. More on this later.  

<figure style="display: flex; flex-direction: row; justify-content: center; align-items: center; text-align: center;">
  <div style="margin-right: 20px;">
    <img src="/assets/2025_04_17/crossy_x.png" alt="crossy_x" width="360">
    <figcaption>Figure 2: A grid that crosses y=x at point p</figcaption>
  </div>
  
  <!-- Another Image -->
  <div>
    <img src="/assets/2025_04_17/bijection.png" alt="bijection" width="255">
    <figcaption>Figure 3: The skewed grid</figcaption>
  </div>
</figure>

This proposition allows us to reduce the complexity of counting 'bad' paths that cross $y=x$ by mapping unique paths on the nxn grid to unique paths on the skewed grid, creating a one-to-one correspondence. 

Now we're ready to dive into Catalan numbers. 

**Definition 1. Catalan numbers.** 
Catalan numbers are given by the formula,   
$$C_n = {{2n} \choose n} - {{2n} \choose {n-1}}$$

Other forms include:
$$
C_n = \frac{1}{n+1}{{2n} \choose n} \\\text{  }
\\
= \frac{1}{2n+1}{{2n + 1} \choose n} 
$$

*Proof.* $C_n$ counts the number of lattice paths that do not cross $y=x$ on the nxn grid. From our previous exploration we know there are ${{2n} \choose n}$ total paths with the number of'bad' paths in the nxn grid bijecting onto the skewed $(n-1)$x$(n+1)$ grid. We therefore can measure 'bad' paths as the total amount of paths in the $(n-1)$x$(n+1)$ grid. 

Hence $C_n =$ {number of total paths} - {number of bad paths}, reaching our decomposition of $C_n$. In summary we combined the principles of counting symmetry and the skewed grid bijection to decompose Catalan numbers as the subtraction of the total number paths with the total number of 'bad' paths. 

**Combining It All Together**
In many ways a Dyck sequence is a geometrical representation of balance, like a surface of a pond. A fish, water bug, or duck that does not disrupt the well-formed waterline is a representation of our one-to-one correspondence, called a *bijection*, to each other. Their path is the same, but its meaning changes depending on the lens you use. A fish's underwater trail can parallel a string of kelp's sway to the current, but they serve as mathematical refractions caused by the watery environment they live in, their form as Dyck paths casting long shadows onto the pond floor. 

Catalan numbers are the representation of the pond depths. They count of all valid paths our pond inhabitants and the refractions of these paths, tallying each specular reflection to hold a single balanced truth on top of its surface. 

<figure style="display: flex; flex-direction: column; align-items: center;">
  <img src="/assets/2025_04_17/monet.jpg" alt="monet" width="500">
  <figcaption>"Monet's Lilies II" by Erin Hanson</figcaption>
</figure>

## Objects Counted by Catalan Numbers 
With this obscure and seemingly tepid equation we can do some real magic. Catalan numbers can count many objects, from chords to arcs to binary trees[^1],  but we'll shift our focus onto two that are seemingly divergent in their relation but provide us with a way to bring this back full circle. To do this  I'll need to introduce some more propositions and definitions.

Firstly, we'll look at a ballot sequence. 

**Definition 2. Ballot sequences.**
A ballot sequence of $2n$ is a sequence with n negative and n positive 1's such that every partial sum is nonnegative. Obviously this means we have more 1's that -1's. Interestingly enough a ballot sequence can be counted by Catalan numbers through a bijection of Dyck Paths. 

**Proposition 2.** There are $C_n$ ballot sequences of length 2n.

*Proof.* First we convert the ballot sequence to a lattice path where 1's are green and -1's are pink. Given that we have a nonnegative sequence, this means we have more or equal to the number of horizontal moves that vertical in an given path subset. Hence we never cross $y=x$, essentially mapping the ballot sequence to a Dyck path. 

To chain it together:
A.  Dyck paths are paths that do not cross $y=x$
B.  Catalan paths are composed of up of Dyck paths 
C.  Ballot sequences are sequences where 1 is never behind (in count) of -1
  
We can show that A = B by bijection, and B = C by bijection,  then A = C. Hence we can show ballot sequences are counted by Catalan numbers. 

### Parenthesization
Now we can introduce parenthesization, a way for us to model hierarchies and nested structures to help us count more efficiently that are also counted by Catalan numbers [^4]. 

**Definition 3.** A parenthesization is an insertion of $n-1$ open parentheses and $n-1$ close parentheses such that the resulting expression involves products of two adjacent things at a time. 

An example of this can be seen with the term 'abcd'. With $n=4$ we have 3 sets of parentheses that allow us to subset the statement like,
$$
(a)(b)(cd) \\
((ab)(cd)) \\
(a(bc))(d) \\
((ab)c)(d) \\
(a(b(cd))).
$$

It all connects back I promise! Because these parentheses are - as you probably guessed - Dyck paths where each right and left parentheses corresponds to a horizontal movement and a letter a vertical one. A example can be seen in the statement 'abcdef' mapped onto a 6x6 grid with the parenthesization of $(a((bc)d))(ef)$, 

A invalid parenthesization corresponds to a Dyck path that crosses $y=x$ by having more green vs pink moves (more vertical moves); in translation this means that the parenthesization has more opening parenthesis than letters. This is nonsensical. 

<figure style="display: flex; flex-direction: column; align-items: center;">
  <img src="/assets/2025_04_17/parent.png" alt="parent" width="350">
  <figcaption>Figure 4: A parenthesizations as a Dyck path</figcaption>
</figure>

## The Ballot Theorem
We're almost at the home stretch! Our LaCroix problem, if you even remember, is a variation of the ballot problem which combines lattice walks, Catalan numbers, and skewed grid bijections for a magus opus of combinatorics and logic. The diversity and depth of proofs for this theorem are really quite beautiful [^3][^5], but for our instances we'll focus on the Andre-Reflection Method. 

**The Problem Statement:**
In 1887 Joseph Bertrand introduced a ballot problem where candidates $(\mathcal{A})$ and $(\mathcal{B})$ are in election. $(\mathcal{A})$ receives $a$ total votes and $(\mathcal{B})$ receives $b$ total votes with the caveat $\mathcal{A} > \mathcal{B}$ at all times. How many ballot permutations could be made? 

Desire Andre produced a combinatorics proof for $k=1$ downturns (under the generalized ballot theorem problem) by counting the number of bad ballot permutations and subtracting that from the total amount of ballot permutations (not unlike of composition of Catalan numbers)[^6]. Andre understood that unfavorable permutations could be stratified into permutations starting with the starting vote as either $(\mathcal{B})$ or $(\mathcal{A})$, and for permutations starting with $(\mathcal{B})$, a bijection existed with all permutations of $b-1$ ballots $(\mathcal{B})$ and $a$ ballots of $(\mathcal{A})$. The same was understood for permutations starting with $(\mathcal{A})$.

While Andre's proof has no geometric reasoning, we'll use a combination of both Andre's symmetry logic to sketch out the Andre-Reflection Method. 

### The Andre-Reflection Method 
Think back to Proposition 1. where we state that the lattice paths in a nxn grid that cross the line $y=x$ are in bijection with the lattice paths in the $(n-1)$ x $(n+1)$ grid. In essence we're mapping a bad path (one where $b > a$, crossing $b = a$) to a good path onto a different grid that semantically still represent an unbalanced outcome.  

<figure style="display: flex; flex-direction: column; align-items: center;">
  <div style="display: flex; flex-direction: row; align-items: center;">
    <div style="margin-right: 20px;">
      <img src="/assets/2025_04_17/badpath_ballot.png" alt="badpath_ballot" width="350">
    </div>
    <div>
      <img src="/assets/2025_04_17/ballot_bij.png" alt="bbij" width="265">
    </div>
  </div>
  <figcaption style="margin-top: 10px; text-align: center;">
    Figure 5: A bad path mapped to a skewed grid
  </figcaption>
</figure>

By reflecting the bad ballot sequence at point $p$ where it crosses $b=a$, we rebalance upturns and downturns to make the path valid again. We can bijectively map the path to another with $a-1$ x $b+1$ grid for a total of $a+b$ steps. Using this reflection method we don't count the paths directly - instead we allow ourselves to take advantage of this peculiar correspondence to count paths in the skewed grid. For bad permutations that start with $(\mathcal{A})$ we must subtract one from $a$ such given this step is not reflected. For all bad paths this gives us:
- Starting with A: $(a-1) + b = a + b - 1$
- Starting with B: $a + (b-1) = a + b - 1$

Hence the bad paths with different starts are symmetric; starting with either candidate essentially leads to the same problem given symmetry, so by subtracting the bad paths with a multiplier of 2 (for $(\mathcal{A})$ and $(\mathcal{B})$ starts) we achieve the solution to the ballot problem.

**Solution. The Ballot Theorem**
$$
{{a + b}\choose {a}} - 2{{a + b -1} \choose a} = \frac{a-b}{a+b}{{a+b}\choose a}.
$$


## Back to the LaCroix Problem
Finally! Let's answer our problem statement and variants. 

**The problem statement**
- How many valid permutations of drawing a equal number of pink (guava) or green (key lime) cans will result in the last two cans being unique flavors given we always have more pink cans $\mathcal{P} > \mathcal{G}$?

Our original problem statement hinges on the condition of always having two unique drink flavors left from the original six. Given $\mathcal{P} > \mathcal{G}$, we can directly apply the generalized ballot theorem where the number permutations is, assuming I only drink one at a given instance,

$$
\frac{p-g}{p+g}{{p+g}\choose p} = \frac{0}{12}{{12}\choose 6} = 0.
$$

**Catalan Numbers**
Weird, but this actually makes a lot of sense. If we want two unique flavors for the last two cans we need the previous draw to balance the count ie. reach $(5, 5)$ on our grid. This isn't possible with our inequality constraint of $\mathcal{P} > \mathcal{G}$, hence we have 0 valid permutations. 

If we had a mismatched number of cans, lets say six pink and 5 green, then the number of drink permutations is given as, 

$$
\frac{p-g}{p+g}{{p+g}\choose p} = \frac{1}{12}{{12}\choose 6} = 77.
$$

### Variation 1.
1. What if I loosened the inequality to $\mathcal{P} \geq \mathcal{G}$? 

Assuming we have the *same number of cans for each flavor*, let's say six, then the loosened inequality lets us touch but not cross the line $\mathcal{G} = \mathcal{P}$ from under. Therefore counting valid paths is just a process of counting all Dyck paths on the grid. Hence we can use a Catalan number and our number of drinking permutations is, 

$$C_6 = {{12} \choose 6} - {{12} \choose {5}}\\= 132.$$

**The Weak Ballot Theorem** 
If we had *different numbers of cans* per flavor our approach is different such that we use the weak ballot theorem. Any ballot permutation where $a$ maintains at least $b$ can be converted to the traditional ballot theorem where $\mathcal{A} > \mathcal{B}$ by simply appending a vote for $\mathcal{A}$ at the beginning of the permutation[^5]. Therefore the weak ballot theorem is the same as the "strict" version when $\mathcal{A}$ receives $a+1$ votes and $\mathcal{B}$ receives $b$ votes, 
$$ $$
$$
\frac{a-b + 1}{a+b + 1}{{a+b + 1}\choose a + 1} = \frac{a-b + 1}{a+1}{{a+b}\choose a}
$$
If we have six pink cans and five green cans given $\mathcal{P} \geq \mathcal{G}$, our number of valid permutations becomes, 
$$\frac{6-5 + 1}{6+1}{{6+5}\choose 6} = 132.
$$

**A Map from Strong to Weak**
This sorcery would surely resurrect another witch burning! But just as it seems, the reason why the ballot theorem has such a nice closed form solution is because of its inherent bijection with constrained lattice paths.

By adding the additional $\mathcal{A}$ vote we added a buffer such that:
- Every strict path from $(0,0) \rightarrow (a+1, b)$ with $\mathcal{A} > \mathcal{B}$ starts with A being ahead 
- If we ignore the first path step of $\mathcal{A}$, the path becomes $(0,0) \rightarrow (a, b)$ for $\mathcal{A} \geq \mathcal{B}$

In other words each unique valid weak path is mapped to a unique strong path by just the addition of an $\mathcal{A}$ vote. We can therefore, not unlike how we used our skewed grid in proposition 1, utilize this bijection and make our counting lives easier.

<figure style="display: flex; flex-direction: column; align-items: center;">
  <div style="display: flex; flex-direction: row; align-items: center;">
    <div style="margin-right: 20px;">
      <img src="/assets/2025_04_17/weak.png" alt="weak" width="330">
    </div>
    <div>
      <img src="/assets/2025_04_17/strong.png" alt="strong" width="395">
    </div>
  </div>
  <figcaption style="margin-top: 10px; text-align: center;">
    Figure 6: A weak path mapped to a strong path 
  </figcaption>
</figure>

**Catalan Numbers Revisited** 
Why does our number of drink permutations for unequal counts among flavors match the instance when we have the same number of drinks for each flavor counted by $C_6$? It's a coincidence in value, but not in structure. If we let $a=b=n$ for $\mathcal{A} \geq \mathcal{B}$ we also find that our weak ballot theorem is generalized by a Catalan number, 

$$
\frac{a-b + 1}{a+1}{{a+b}\choose a} = \frac{1}{n+1}{{2n}\choose n} = C_n. 
$$

While this observation seems redundant, this gives us an algebraic understanding of the weak ballot theorem and further strengthens our intuition of Dyck paths and Catalan numbers. 

### Variation 2. 
2. What if I drank multiple green cans per visit to the fridge?  

**Generalized Ballot Theorem**
With our initial condition of $\mathcal{P} > \mathcal{G}$, multiple green drinks taken out of the fridge for each visit is a downturn step that has a greater magnitude that an upturn. Hence, we can reformulate our ballot theorem for some relative size $k$ such that $\mathcal{A} > k\mathcal{B}$. This is called the generalized ballot theorem[^5]and introduces new caveats with lead margins and rotated lattice walks. 

For this theorem we hinge our linear line of $B=A$ on the grid such that our x-axis is our edict for a good or bad path. For example if a path dips below the x-axis then it is considered bad, while a path that stays above the x-axis is good. A downstep that starts above the x-axis and ends below it (negative slope) is a bad step. 

Hence for each candidate step we have, 
- $\mathcal{A}$ upturn: $(1, 1)$ 
- $\mathcal{B}$ downturn: $(1, -k)$ 

Let $B_0, \dots, B_k$ represent the number of bad paths where $B_i$ is a path that lands exactly $i$ units below the x-axis. These sets are disjoint and their union $B_0 \cup \dots \cup B_k$ is the collection of all bad paths. $B_k$ is all paths that start with a downturn where the first step lands $k$ units below the x-axis. Therefore, if we let the x-axis denote $\mathcal{A}$ and the y-axis $\mathcal{B}$, we can see that the number of $B_k$ paths is the total $a+b$ subtracted by the first initial step, hence $a+b-1$. It follows that $B_k$ is, 
$$
|B_k| = {{a+b-1}\choose a}.
$$

Interestingly enough we can show for $k \neq i$ that 
$$
|B_k| = |B_i|.
$$

<figure style="display: flex; flex-direction: column; align-items: center;">
  <img src="/assets/2025_04_17/general.png" alt="general" width="380">
  <figcaption>Figure 7: A x-axis representation of a lattice walk (M. Renault) </figcaption>
</figure>

To prove this let $P$ be the path in $B_i$ where $k \neq i$ and $X$ the initial segment of P that ends $i$ units below the x-axis. Let path $P=XY$ where $Y$ is the rest of the path not including $X$. Let $\tilde{X}$ represent the path that results from rotating $X$ 180 degrees. Given $X$ ends with a downturn $\tilde{X}$ starts with a downturn. 

Our new rotated path of $\tilde{X}Y \in B_k$. We can reverse this process from $B_k$ to $B_i$ but in any case, we model a bijection where 
$$
|B_i| = |B_k| = {{a+b-1}\choose a}.
$$
Given there are $k+1$ such bad path sets given $0 \leq i \leq k$ we have 

$$
(k+1){{a+b-1}\choose a}.
$$

Subtracting good paths from bad paths we finally achieve 
$$
{{a+b-1}\choose a} - (k+1){{a+b-1}\choose a} = \frac{a-kb}{a+b}{{a+b} \choose a}. 
$$

Applied to our problem statement let us assume we take two green cans ($k=2$) at a given time given 12 pink and five green cans. Our total number of drinking permutations such that $\mathcal{P} > k\mathcal{G}$ is,
$$
\frac{a-kb}{a+b}{{a+b} \choose a} = \frac{12-(2)5}{12+5}{{12+5} \choose 12} = 728. 
$$

**Uniform Partitioning** 
It can be shown that 
$$
|B_0| = \dots = |B_k| = {{a+b-1}\choose a}.
$$

The same cardinality of the sets of $B_i$ regardless of the value of $i$ is a example of uniform partitioning. Instead of counting all paths separately we can group each path by definitive characteristics (like downturn location on the x-axis) and construct a bijection. This principle is coined the  Chung-Feller theorem but was originally introduced by MacMahon in 1909[^7].  

### Variation 3
3. What if I completely scrap the restrictive inequality such that I only care that the last two drinks are green and pink?

<figure style="display: flex; flex-direction: column; align-items: center;">
  <img src="/assets/2025_04_17/restrict.png" alt="restrict" width="380">
  <figcaption>Figure 8: The restricted 6x6 grid </figcaption>
</figure>

This problem lets us step away from the ballot theorem to look at some good old lattice walks. If we assume equal number of cans per flavor, let's say six, then we know that we must reach coordinate $(5, 5)$. We are restricted by the the $(5,5)$ grid where we can take five steps up (green can) or 5 steps horizontally (pink can). It's a simple scenario of how many ways we can order the five steps vertically or horizontally. Hence the number of valid drinking permutations is given as,   
$$
{{p+g}\choose{p}} = {{10}\choose{5}} = 252.
$$ 

Even if our number of drinks per flavor differ we can still use our strategy. If we have six pink and five green cans we must reach the coordinates $(5, 4)$. Therefore our valid drinking paths can be represented as,
$$
{{p+g}\choose{p}} = {{9}\choose{5}} = 126. 
$$

## Conclusions 
Well well well... what a great exercise of free will. Trust humans to make something as simple as counting so pedantic. 

Safe to say this post had me feeling like:
<figure style="display: flex; flex-direction: column; align-items: center;">
  <img src="/assets/2025_04_17/crazy.png" alt="restrict" width="380">
</figure>

Next steps? Maybe I'll dabble in chords or triangulations - those seem stupidly fun. Heck I might even take a look into knot theory; it'll be fun to tell my friends I'm studying something that'll acquire me a girl scout badge. 



[^1]: ["Catalan Numbers, Their Generalization, and Their Uses" Pedersen. Hilton.](https://www.math.uakron.edu/~cossey/636papers/hilton%20and%20pedersen.pdf)

[^2]: ["Catalan Numbers" Stanley.](https://math.mit.edu/~rstan/transparencies/china.pdf)

[^3]: To my understanding, the Reflection method, which is synonymous with Andre, was never actually employed by him. Andre used purely combinatoric and algebraic representations. ["Lost and Found" Renault.](http://webspace.ship.edu/msrenault/ballotproblem/LostAndFound.pdf)

[^4]: Meszaros gives a great high level overview of Catalan numbers and other more interesting applications like triangulations and plane trees. ["Catalan Numbers" Meszaros.](https://pi.math.cornell.edu/~karola/dimex/catalan.pdf)

[^5]: Other techniques include, but are not limited to, counting, reflecting, induction, using the cycle lemma, and uniform partitions. ["Lost and Found" Renault.](http://webspace.ship.edu/msrenault/ballotproblem/LostAndFound.pdf)

[^6]: A translation of the original solution to Bertrand's problem by Andre ["Direct solution of the problem solved" Andre.](https://webspace.ship.edu/msrenault/ballotproblem/EnglishAndre.pdf)  

[^7]: MacMahon's solution for $k=1$ of the Ballot problem using partitions ["Memoir on the Theory of the Partitions of Numbers" MacMahon.](https://www.jstor.org/stable/91034)


