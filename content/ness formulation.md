---
title: I. Things!
draft: false
tags: 
aliases:
  - I. Things!
date: "{{date}}"
description: This post explains the NESS (non-equilibrium steady state) formulation of the Free Energy Principle.
---
*Meta*: This article is an opinionated distillation of [Friston, 2019](https://arxiv.org/abs/1906.10184) and [Millidge et al., 2021](https://arxiv.org/abs/2108.13343).

---

If you are reading this sentence, then you exist.

What information can we deduce from this fact? It turns out, quite a lot. We can deduce that the universe is governed by laws such that your existence was possible, which constrains the value of some fundamental physical constants. This is the [anthropic principle](https://en.wikipedia.org/wiki/Anthropic_principle).

The key moves here are to (1) make a really obvious observation – to notice that “hey, I exist!” – (2) to formalize that observation somehow, and (3) squeeze the formalization really hard to see what else you can deduce about the world based on it.

But why stop here? Why stop at observing that *you* exist? Bacteria also exist. So do fungi, and other humans, and cities, and plants… Maybe we can generalize what we did with the anthropic principle to all of these “things” somehow, i.e. we can (1) observe that these “things” exist, (2) formalize this observation, (3) deduce some cool stuff about how the world must be, given this observation.

This is the core idea of Karl Friston’s Free Energy Principle (FEP). The specific question we are asking here is:
> If **things exist**, **what must they do**?

To answer this question, we need to formalize what exactly is meant by
- **things exist**
- **what must things do**

First, what kinds of **things** are we even talking about? We are curious about the kind of thing that is self-organizing and maintains its “thingness” regardless of external perturbations, up to a point. We are not for the moment concerned with particles or snowflakes, even though they are things in some sense (although we can apply similar logic to them, since they are still things - that are a lot worse at maintaining their thingness.) We are concerned with things like bacteria, plants, humans, cultures… etc.

By **what must things do,** we just mean “what must the thing’s [mechanics](https://en.wikipedia.org/wiki/Mechanics) be”, where “mechanics” refers to *how* the states that comprise a thing “move” or *change* through space and time.

We can now rephrase the extremely vague question we had at the start into a less vague but still really vague question:

> If **self-organizing things that maintain their thingness exist**, **what must the mechanics of those things be**?

Overall, we will try to answer this question by:

1. Formalizing “thingness”
2. Slotting the formalized definition into a general mathematical description of physical systems
3. Rearranging a bunch of equations and interpreting what pops out

Eventually, we will get to a theorem like “self-organizing things that maintain their thingness must minimize a quantity called **variational free energy**“. Hence why the FEP is called the “Free Energy” principle.

Also, note that the FEP is unfalsifiable since it is mathematically true. It is a principle, not a theory.
- The right question is *not* to ask “is the FEP true?”. Because the answer to this question is yes, it is tautologically true in math-land, like all theorems, if you include all the assumptions.
- The right question *is* to ask “do the assumptions of the FEP apply to the system I am modeling?”. If the assumptions do in fact hold true, you can then construct falsifiable theories about the system by making specific modeling choices (i.e. picking a specific generative model – this sentence will make sense later).



## I. What’s a thing?

  

In this section we are trying to define precisely what it means for a thing to exist (in space, over some timescale) by formulating a set of “thingness conditions”.

  

### Bounding things in space

Intuitively, for a thing to exist in space, there must be:

- Stuff inside the thing – *ex: lungs, plant cells, stem cells…*
- Stuff outside the thing (i.e. the environment in which the thing exists) – *ex: petri dish…*
- Stuff that separates the inside from the outside (i.e. the thing’s boundary) – *ex: cell membrane, skin, sensory receptors…*

Once you’ve defined the boundary of the thing you’re talking about, you’ve basically defined everything else, since now you know that reality can be neatly carved into three subsets: (1) a boundary, (2) stuff on one side of the boundary, and (3) stuff on the other side of the boundary. Usually, we call the side of the boundary with less stuff in it “inside”, while the side that has more stuff is called “outside”.

The boundary divides everything into three regions: “inside”, “outside”, and “the region on the boundary”.

Now to formalize this idea. If we model the system of interest as a bunch of random variables, some of which influence other random variables causally (specifically if we model the system as a [causal graph](https://en.wikipedia.org/wiki/Causal_graph) of [random variables](https://en.wikipedia.org/wiki/Random_variable)), then we can define:

- **internal states** as the subset of states that comprise the “inside” of the system; we pick these states manually based on what we define as “inside”
- **blanket states** as the subset of states which insulate/separate the internal states from the rest of the network, i.e. the “boundary” of the system; we know what these states are after picking the internal states
- **external states** as the subset of states which are *not* the internal states and *not* the blanket states, i.e. the states left over *after* considering the internal and blanket states

  
<details>
<summary> Background on causal graph of random variables </summary>

**Prerequisites**: [random variables](https://en.wikipedia.org/wiki/Random_variable), [conditional probability](https://en.wikipedia.org/wiki/Conditional_probability), [joint probability](https://en.wikipedia.org/wiki/Joint_probability_distribution), [Bayes theorem](https://youtu.be/HZGCoVF3YvM?si=QpHgFNbLDLoKu-vr)

What does it mean for event $A$ to cause event $B$? A reasonable first stab at defining causation probabilistically might be to say that event $A$ causes event $B$ iff. event $A$ occurring raises the probability of event $B$ occurring, i.e.

$$

p(A \mid B) > p(A \mid \neg B)

$$

But there are two issues with this:

- The statement above is only true iff. $p(B \mid A) > p(B \mid \neg A)$, which means that under our definition of causation $A$ causing $B$ is equivalent to $B$ causing $A$. Our definition of causation should be [asymmetrical](https://en.wikipedia.org/wiki/Correlation_does_not_imply_causation): $A$ causing $B$ should not imply that $B$ causes $A$.


	1 - Show that $p(A \mid B) > p(A \mid \neg B) \implies p(B \mid A) > p(B \mid \neg A)$ 
	
	$$
	
	\begin{align*}
	
	p(A \mid B) &> p(A \mid \neg B) \\
	
	\frac{p(B \mid A) p(A)}{p(B)} &> \frac{p(\neg B \mid A) p(A)}{p(\neg B)} \\
	
	\frac{p(B \mid A)}{p(B)} &> \frac{p(\neg B \mid A)}{p(\neg B)} \\
	
	p(B \mid A)p(\neg B) &> p(\neg B \mid A)p(B) \\
	
	p(B \mid A)p(\neg B) &> (1 - p(B \mid A))p(B) \\
	
	p(B \mid A)p(\neg B) &> p(B) - p(B \mid A)p(B) \\
	
	p(B \mid A)p(\neg B)+p(B \mid A)p(B) &> p(B) \\
	
	p(B \mid A) &> p(B) \\
	
	p(B \mid A) &> p(B, A) + p(B,\neg A) \\
	
	p(B \mid A) - p(B \mid A)p(A) &> p(B,\neg A) \\
	
	p(B \mid A)(1 - p(A)) &> p(B \mid \neg A)p(\neg A) \\
	
	p(B \mid A)p(\neg A) &> p(B \mid \neg A)p(\neg A) \\
	
	p(B \mid A) &> p(B \mid \neg A) \square
	
	\end{align*}
	
	$$
	

2 - Show that $p(B \mid A) > p(B \mid \neg A) \implies p(A \mid B) > p(A \mid \neg B)$

We can use the same proof as above and just swap $A$ and $B$. $\square$

- The statement also holds true if there is some confounding variable $C$ that raises *both* the probability of $A$ and $B$, or if there is some variable $D$ between $A$ and $B$ (i.e. $A$ causes $D$ which causes $C$. But ideally, we’d only want our definition of causation to hold when $A$ *directly* causes $B$.

So we need some additional conditions on our definition of causation to satisfy (1) asymmetry and (2) deal with confounding variables.

Here’s [one way to fix our definition of causality](https://plato.stanford.edu/entries/causation-probabilistic/#ScreOff). We can say that $A$ (directly) causes $B$ iff. three conditions are met:

- $p(A \mid B) > p(A \mid \neg B)$, i.e. $B$ occurring raises the probability of $A$ occurring

Same condition as above.

- The time at which $A$ occurs, $t_A$ must be *before* the time at which $B$ occurs, $t_B$

This makes our definition of causation asymmetrical since time only flows one way.

- There are no variables that **screen off** $A$ from $B$

A variable $C$ screens off $A$ and $B$ iff. $p(A \mid B, C) = p(A \mid C)$. There are two cases in which this might be true:

- $C$ is causally *between* $A$ and $B$, i.e. the causal structure of the system being modeled is $A \to\ C \to\ B$, where $X \to Y$ indicates $X$ causes $Y$.

- $C$ is a common cause (or confounder) of $A$ and $B$, i.e. the causal structure of the system being modeled is $A \leftarrow C \rightarrow B$.

We can express this notion of probabilistic causation visually with a [directed acyclic graph](https://en.wikipedia.org/wiki/Directed_acyclic_graph). If $A$ causes $B$, there will be an arrow pointing from $A$ to $B$. Because of the **screening off** condition stated above, we know that if – on the graph – we have some structure $A \to C \to B$ then by definition (1) $A$ causes $C$ and $C$ causes $B$ so (2) $C$ screens off $A$ from $B$ so (3) $p(A \mid B,C) = p(A \mid C)$. This also means that $p(A,B \mid C) = p(A \mid C) \cdot p(B \mid C)$.

**Read more**: [probabilistic causation](https://plato.stanford.edu/entries/causation-probabilistic/#ProbForReguTheo)

</details>
  

Visually:

  

![Source: [https://datasciencestation.com/markov-blanket/](https://datasciencestation.com/markov-blanket/)](Things!%20FEP%20Explained,%20Part%201%20118fcfd4925d8035ba35c1609bd81243/image.png)

  

Source: [https://datasciencestation.com/markov-blanket/](https://datasciencestation.com/markov-blanket/)

  

The blanket states $b$ – also called the [Markov blanket](https://en.wikipedia.org/wiki/Markov_blanket) of the system – are defined such that

  

$$

p(e\mid i, b) = p(e\mid b) \\

p(i\mid e, b) = p(i\mid b) \\

p(i, e \mid b) = p(i\mid b) \cdot p(e \mid b)

$$

  

where $i$ = internal states, $e$ = external states. This means that to describe the probability distribution on external states or internal states, we *only* need to know the blanket states and nothing further (see lines 1 and 2). This also means that the distributions on $i$ and $e$ are independent, *conditional on* blanket states $b$. In most cases – but not always – blanket states correspond to physical barriers that enclose a system (e.g. a cell membrane).

  

We can further partition the blanket states into sensory states $s$ and active states $a$, where sensory states are blanket states that influence but are not influenced by internal states, and active states are blanket states that are influenced by but do not influence internal states. If the system being modeled is a human, examples of sensory states are the states that characterize sensory receptors (e.g. rods and cones in the eye), and examples of active states are the states that characterize physical actuators (e.g. muscle cells). Visually:

  

![image.png](Things!%20FEP%20Explained,%20Part%201%20118fcfd4925d8035ba35c1609bd81243/image%201.png)

  

Broadly speaking, all of the waffling we’ve done above allows us to partition all the states we’re considering $x$ into subsets of conceptual significance (e.g. the subset $b$ corresponds to the boundary between the system and its environment. Specifically, we can write $x = \{i, b, e\} = \{i, \{a,s\}, e\}$ since $b = \{a, s\}$. This is important because now we’ve identified subsets $i$ and $a$ – let’s group them together and call them autonomous states $\alpha = \{i, a\}$ – that we care about. We care about $\alpha$ because they comprise the “inside” of the thing $i$, as well as how the thing can influence its environment (through $a$). We can now be more specific with our initial question, and turn it from

  

> If **self-organizing things that maintain their thingness exist**, **what must the mechanics of those things be**?

>

  

to

  

> If **self-organizing things that maintain their Markov blanket exist**, **what must the mechanics of those things’ *autonomous states* be**?

>

  

Thus far, we’ve formalized what it means for a system to be statistically separated (and distinct) from its environment in space. Our answer is that, for the system to exist continually, it has to maintain a Markov blanket that surrounds its internal states. This **Markov blanket assumption** is the first “thingness condition”.

  

### Bounding things in time

  

By stipulating that the system we’re considering maintains its Markov blanket over time, we’ve not only implicitly bounded the system in space, but also implicitly bounded the system in time. (Because Markov blankets are not maintained forever!) But is this enough?

  

Consider the scenario:

  

- The system we’re modeling is a human that maintains its Markov blanket. (We’re modeling at a sufficiently high level of abstraction that the constantly dying skin cells don’t count as the Markov blanket not being maintained.)

- The human joins a cult and goes through some serious trauma that they never recover from.

  

Arguably, on some intuitive level, the human before the trauma and the human after the trauma are not the same “thing”, even though the human’s Markov blanket was maintained.

  

From this we can infer that we need more stringent bounds on “thingness” in time, and that more specifically we need to formalize the notion of a constant [phenotype](https://en.wikipedia.org/wiki/Phenotype) (since constant Markov blanket does not necessarily imply constant phenotype). We can do this pretty easily by assuming that the probability distribution over all the states $x$ is constant, i.e.

  

$$

\frac{dp(x, t)}{dt} = 0

$$

  

Note that this implicitly defines phenotype to be equivalent to a specific probability distribution function. This assumption is called the **steady state condition**, because the probability distribution function doesn’t change w.r.t. time.

  

<aside>

🔄

  

**Recap**

  

In this section we’ve formalized what it means to be a “thing” (more precisely, what it means to be the “same thing”) over some timescale. The two thingness conditions are:

  

- **Markov blanket assumption**: you need a constant Markov blanket, and

- **Steady state condition**: you need to have a probability distribution that doesn’t change w.r.t time.

  

We can now rephrase our really general initial question

  

> If **self-organizing things that maintain their thingness exist**, **what must the mechanics of those things be**?

>

  

into a less general question

  

> Given a **self-organizing thing that maintains its Markov blanket**, **what must the mechanics of that thing’s autonomous states be at steady state**?

>

</aside>

  

## II. **From extremely general physics to slightly less general but still really general physics**

  

In this section, we’ll (1) consider an extremely general description of a physical system, (2) introduce the thingness conditions established in the previous section one by one, and (3) reshuffle/rearrange a bunch of equations to see what we get.

  

### Langevin dynamics

  

Our starting point is to assume that our system follows [Langevin dynamics](https://en.wikipedia.org/wiki/Langevin_dynamics), i.e. that the change of states with respect to time can be described with the following [differential equation](https://en.wikipedia.org/wiki/Differential_equation)

  

$$

\frac{dx}{dt} = f(x) + \omega

$$

  

where $x$ is a [vector](https://en.wikipedia.org/wiki/Euclidean_vector) of all the states we’re considering, $f(x)$ is some function (a vector field), and $\omega$ is a random variable drawn from a [normal distribution](https://en.wikipedia.org/wiki/Normal_distribution) with variance $\Gamma$ where $\Gamma$ is some scalar constant. Essentially we’re assuming that the dynamics of the states we’re describing (i.e. how the states we’re describing change over time) can be split into two parts: a part described by some function $f$, plus another part that consists of well-behaved randomness $\omega$.

  

We can rewrite the equation above in terms of the rate of change w.r.t. time on the probability density of states $p(x,t)$, instead of on the rate of change w.r.t. time on the states $x$ themselves through the Fokker-Planck equation.

  

$$

\begin{align*}

\frac{dp(x, t)}{dt} &= \nabla \cdot [(\Gamma\nabla_x - f(x,t))p(x,t)] \\

&= \nabla \cdot [\Gamma\nabla_xp(x,t) - f(x,t)p(x,t)]

\end{align*}

$$

  

To be clear:

  

- $\nabla \cdot$ here is the [divergence operator](https://www.youtube.com/watch?v=rB83DpBJQsE),

- $\nabla_x$ is the [gradient operator](https://en.wikipedia.org/wiki/Gradient) on the probability density $p(x, t)$ (which is a scalar field).

  

- Background on partial derivatives $\frac{\partial f}{\partial x}$ , gradient operator $\nabla$, vector fields, divergence operator

Say we have some function and we want to describe how it changes over time. In the single-variable case, e.g. for some function $y = g(x)$ we can just calculate $\frac{dg}{dx}$. In the multi-variable case, e.g. $z = f(x, y)$, we need a new concept to do the same thing: the partial derivative.

If we want to know how $f$ changes in the $x$ direction we take the [**partial derivative**](https://en.wikipedia.org/wiki/Partial_derivative) w.r.t. $x$ and write $\frac{\partial f}{\partial x}$, which is computed by applying the usual rules of differentiation to $f$ while treating $y$ as a constant; and we compute $\frac{ \partial f}{\partial y}$ if we want to know how $f$ changes in the $y$ direction.

Visually:

![Source: [https://calcworkshop.com/partial-derivatives/partial-derivative/](https://calcworkshop.com/partial-derivatives/partial-derivative/)](Things!%20FEP%20Explained,%20Part%201%20118fcfd4925d8035ba35c1609bd81243/image%202.png)

Source: [https://calcworkshop.com/partial-derivatives/partial-derivative/](https://calcworkshop.com/partial-derivatives/partial-derivative/)

But what if we wanted to talk about how $f$ changes in general, and not how it changes specifically w.r.t $x$ or $y$? It would be useful to have some single quantity that packages all the partial derivatives of $f$ into one. This is basically the [**gradient operator**](https://en.wikipedia.org/wiki/Gradient#Relationship_with_total_derivative) $\nabla$, which is defined as a vector of all the partial derivatives:

$$

\nabla_{f(x,y)} = \left <\frac{\partial f}{\partial x}, \frac{\partial f}{\partial y} \right >

$$

The gradient operator takes as input a **scalar field** – i.e. a function that maps $n$ **inputs to $1$ output – and outputs a **vector field** (a function that maps $n$ inputs to $n$ outputs). Visually:

![Source: [https://angeloyeo.github.io/2019/08/25/gradient_en.html](https://angeloyeo.github.io/2019/08/25/gradient_en.html)](Things!%20FEP%20Explained,%20Part%201%20118fcfd4925d8035ba35c1609bd81243/image%203.png)

Source: [https://angeloyeo.github.io/2019/08/25/gradient_en.html](https://angeloyeo.github.io/2019/08/25/gradient_en.html)

![On the left is the gradient field (i.e. the result of the gradient operator); on the right is the scalar field that the gradient operator is being applied to.

Source: [https://youtu.be/v0_LlyVquF8?si=O8hjwbuk29R18hcd](https://youtu.be/v0_LlyVquF8?si=O8hjwbuk29R18hcd)](Things!%20FEP%20Explained,%20Part%201%20118fcfd4925d8035ba35c1609bd81243/image%204.png)

On the left is the gradient field (i.e. the result of the gradient operator); on the right is the scalar field that the gradient operator is being applied to.

Source: [https://youtu.be/v0_LlyVquF8?si=O8hjwbuk29R18hcd](https://youtu.be/v0_LlyVquF8?si=O8hjwbuk29R18hcd)

The divergence operator does the opposite. It takes as input a **vector field** and outputs a **scalar field**. Intuitively, the scalar field tells you how much (at each point) the vector field acts as a source or a sink.

![Left: divergence is positive; the point acts as a source. Right: divergence is negative; the point acts as a sink. Middle: divergence is zero; the point acts as neither a source nor a sink.](Things!%20FEP%20Explained,%20Part%201%20118fcfd4925d8035ba35c1609bd81243/image%205.png)

Left: divergence is positive; the point acts as a source. Right: divergence is negative; the point acts as a sink. Middle: divergence is zero; the point acts as neither a source nor a sink.

**Learn more:**

[https://www.youtube.com/watch?v=rB83DpBJQsE](https://www.youtube.com/watch?v=rB83DpBJQsE)

  

Now, we have a really general description – the Fokker-Planck equation – that describes how lots of physical systems behave in terms of the probability distribution on the states of the system. The next step is to slot in our “thingness assumptions” and to see what comes out.

  

### Solving the Fokker-Planck equation

  

Recall from before that the second thingness condition was the steady state assumption, i.e. that $\frac{dp(x,t)}{dt} = 0$. We can directly apply this as an [initial condition](https://en.wikipedia.org/wiki/Initial_condition) to the Fokker-Planck equation above:

  

$$

\frac{dp(x, t)}{dt} = \nabla \cdot [(\Gamma\nabla_x - f(x,t))p(x,t)] = 0

$$

  

Now we just need to solve this nasty-looking differential equation and find $p(x)$! …Right?

  

But wait:

  

- We have two unknowns – the probability density $p(x)$ and the flow $f(x)$ – and only one equation. So if we did solve the differential equation, we’d have to find $p(x)$ in terms of $f(x)$ somehow.

- Also, *do we even care* about $p(x)$ *at all*? Remember that our initial question was “Given a **self-organizing thing that maintains its Markov blanket**, **what must the mechanics of that thing’s autonomous states be at steady state**?” where “mechanics” here means something like “how does the thing change w.r.t time” (so we can actually replace “mechanics” with “dynamics”). Well, $f(x)$ is quite literally the flow function that defines how $x$ changes w.r.t. time – it’s the only non-stochastic term in both the Langevin and Fokker-Planck differential equations. So technically, finding an expression for $f(x)$ would answer our question exactly.

  

So our actual goal now is to find an expression for $f(x)$ in terms of $p(x)$ that, when plugged into the equation above, satisfies the steady-state condition (i.e. it makes $\frac{dp(x,t)}{dt} = 0$) and then to figure out what that expression means.

  

It turns out that $f(x) = (\Gamma - Q) \nabla_x \ln(p(x))$ has the properties we want, where

  

- $\Gamma$ is an [identity matrix](https://en.wikipedia.org/wiki/Identity_matrix) scaled by a constant,

- $Q$ is an antisymmetric matrix (i.e. a matrix equal to its negative transpose $Q = -Q^T$) and the gradient of $Q$ is [orthogonal](https://en.wikipedia.org/wiki/Orthogonality_(mathematics)) to the gradient of the log density $\ln(p(x))$, i.e. $\nabla_x Q \cdot \nabla_x p(x) = 0$.

  

We can verify this:

  

- Proof that initial condition is satisfied

We will show that $f(x) = (\Gamma - Q) \nabla_x \ln(p(x)) \implies \frac{dp}{dt} = 0$

$$

\begin{align*}

\frac{dp(x, t)}{dt} &= \nabla \cdot [(\Gamma\nabla_x - f(x,t))p(x,t)] \\

&= \nabla \cdot [(\Gamma\nabla_x - (\Gamma - Q) \nabla_x \ln(p(x)))p(x)] \\

&= \nabla \cdot [(\Gamma\nabla_x - (\Gamma - Q) \nabla_xp(x)\frac{1}{p(x)})p(x)] && \text{chain rule} \\

&= \nabla \cdot [(\Gamma\nabla_xp(x) - (\Gamma - Q) \nabla_xp(x)] \\

&= \nabla \cdot [(\Gamma\nabla_xp(x) - \Gamma\nabla_xp(x) + Q\nabla_xp(x)] \\

&= \nabla \cdot [Q\nabla_xp(x)]

\end{align*}

$$

We end up with $\nabla \cdot [Q \nabla_x p(x)]$ which means we are taking the divergence of $Q\nabla_x p(x)$.

In this case, the $i$th component of $Q \nabla_x p(x)$ is $\sum_j Q_{ij}\frac{\partial p}{\partial x_j}$. To take the divergence of this w.r.t. $x$ we have to $\frac{\partial}{\partial x_i}$ each term and sum everything, i.e.

$$

\nabla \cdot [Q \nabla_x p(x)] = \sum_i \frac{\partial}{\partial x_i}(\sum_j Q_{ij}\frac{\partial p}{\partial x_j}) = \sum_i\sum_j Q_{ij} \frac{\partial^2p}{\partial x_i \partial x_j}

$$

We also know that $Q = -Q^T \implies Q_{ij} = -Q_{ji}$ and that $\frac{\partial p}{\partial x_i x_j} = \frac{\partial p}{\partial x_j x_i}$, which means that everything sums to $0$.

  

The expression for the vector field $f(x)$ we have above is actually a generalization of the Helmholtz decomposition, a.k.a. the [fundamental theorem of vector calculus](https://en.wikipedia.org/wiki/Helmholtz_decomposition), which states that any “well-behaved” vector field can be split into the sum of two vector fields, where one of these vector fields is curl-free and the other is divergence-free.

  

- Background on Helmholtz decomposition

- Divergence and curl

[Divergence and curl](https://youtu.be/rB83DpBJQsE?si=Ma7WoThV5-gje9SF) are **vector operators**, i.e. functions that take vector fields as inputs. Suppose we have some vector field $V(x, y)$. Then:

- **Divergence** $\nabla_x \cdot V(x,y)$ is a measure of how much that vector field behaves like a “source” or a “spring” at a given point. If the vector field behaves like a “sink” or a “plughole”, the divergence at that point is negative. More broadly, it is a measure of whether the rate at which things flow “out of” that point is faster than the rate at which things flow “into” that point. Divergence turns **vector fields** into a **scalar field**.

![Source: Wikipedia](Things!%20FEP%20Explained,%20Part%201%20118fcfd4925d8035ba35c1609bd81243/image%206.png)

Source: Wikipedia

- **Curl** $\nabla_x \times V(x,y)$ is a measure of how much that vector field rotates counterclockwise at a given point. If it rotates clockwise at a given point, the curl is negative. (This is based on the [right hand rule](https://en.wikipedia.org/wiki/Right-hand_rule).) Curl turns an input vector field into another vector field, where

- the output vector field is composed of vectors orthogonal to the vectors on the original vector field and

- the magnitude of the vectors of the output vector field indicate how much the original vector field was rotating counterclockwise at a particular point (if the magnitude is large and negative, this indicates the original vector field was rotating clockwise at a particular point).

- For example, the original vector field (on the left) rotates counterclockwise at every point so the **curl** of that vector field (displayed on the right) is composed of all-positive, orthogonal vectors:

![Source: Wikipedia](Things!%20FEP%20Explained,%20Part%201%20118fcfd4925d8035ba35c1609bd81243/Screenshot_2024-10-09_at_9.19.00_PM.png)

Source: Wikipedia

The Helmholtz decomposition states that any “well-behaved” vector field can be written as

$$

V(x,y)=\nabla_{x,y}\cdot U(x,y)+\nabla_{x,y} \times W(x,y)

$$

where $U(x,y)$ is a curl-free vector field, i.e. $\nabla_{x,y} \times U(x,y) = 0$

- In our expression for $f(x)$ this corresponds to $\Gamma \nabla_x \ln(x)$.

and $W(x,y)$ is a divergence-free vector field, i.e. $\nabla_{x,y} \cdot W(x,y) = 0$.

- In our expression for $f(x)$ this corresponds to $-Q \nabla_x ln(x)$.

This decomposition is quite intuitive visually (left = curl-free, right = divergence-free):

![Source: [https://link.springer.com/article/10.1007/s12650-018-0534-y](https://link.springer.com/article/10.1007/s12650-018-0534-y)](Things!%20FEP%20Explained,%20Part%201%20118fcfd4925d8035ba35c1609bd81243/image%207.png)

Source: [https://link.springer.com/article/10.1007/s12650-018-0534-y](https://link.springer.com/article/10.1007/s12650-018-0534-y)

  

We actually have a preliminary answer to our question in the form of an expression for $f(x)$:

  

$$

f(x) = (\Gamma - Q)\nabla_x \ln p(x)

$$

  

But what does this expression actually mean? Right now it’s just a pile of symbols. We’ll explore this in the next section.

  

### The Helmholtz decomposition

  

We now have an expression that describes the flow function $f(x)$ – i.e. how all the states we’re considering change – at steady-state:

  

$$

f(x) = (\Gamma - Q)\nabla_x \ln p(x)

$$

  

Graphing what this looks like (in three dimensions) will give us more intuition and insight on what this expression means, and the significance of each component.

  

Visually:

  

![Untitled_Artwork 4.png](Things!%20FEP%20Explained,%20Part%201%20118fcfd4925d8035ba35c1609bd81243/Untitled_Artwork_4.png)

  

We can thus see the geometric significance of the $\Gamma$ and $Q$ parts of the flow

  

- The $\Gamma$ part climbs the log density

- The $Q$ part, also called the **solenoidal flow**, circulates around the log density

  

The former means that the flow on the states $f(x)$ will try to maximize the log density $\ln p(x)$. But recall that, all the way back in the Langevin equation, there was another component of the change in states w.r.t time $\frac{dx}{dt}$: the normally distributed, random fluctuations $\omega$ with variance $\Gamma$. So while the $\Gamma$ component of the flow tries to *ascend* the log density, $\omega$ will try to oppose the $\Gamma$ component of the flow by *descending* the log density.

  

Why is this significant? Well, because the “things” we are considering – humans, bacteria, plants … – only remain “things” (can only maintain their Markov blankets in) a *small number of states* (call these states the **characteristic states** of a “thing”). If I teleported a person from Massachusetts to Egypt, they’d feel quite hot, but still survive and maintain their Markov blanket due to the $\Gamma$ part of the flow. If I teleported this person to the sun, however, their Markov blanket would dissolve. This is because I’ve changed the internal states of the person – specifically, their temperature state – *so much* that I’ve moved the “thing” out *too far* from its small region of characteristic states.

  

The kinds of things we’re considering are able to continue to exist in the face of small fluctuations (Massachusetts → Egypt), but dissolve when faced with very large fluctuations (Massachusetts → Sun). This concept of resistance to external perturbations offers an intriguing way to quantify how “thing-like” (agent-like?) a given “thing” is.

  

- Background – but why do $\Gamma \nabla_x \ln p(x)$ and $-Q\nabla_x \ln p(x)$ do that on the graph?

- Why does $\Gamma \nabla_x \ln p(x)$ climb up the log density?

Recall that $\Gamma$ is defined as a scaled identity matrix, so the only effect it has on $\nabla_x \ln p(x)$ is that it scales up the magnitude of the vectors (the direction of the vectors remain unchanged).

Also recall from earlier that the gradient operator $\nabla_x$ on some scalar field $S(x)$ by definition outputs a vector field, where [each vector points in the direction of steepest ascent](https://math.stackexchange.com/questions/223252/why-is-gradient-the-direction-of-steepest-ascent) w.r.t the original scalar field.

Thus, $\Gamma \nabla_x \ln p(x)$ is a vector field where all the vectors point towards the peak of the probability density scaled by magnitude $\Gamma$, which means that this component of the flow “climbs up” the density.

- Why does $-Q\nabla_x \ln p(x)$ circulate around the log density?

Recall that $Q$ is defined as an antisymmetric matrix, i.e. $Q = -Q^T$. Antisymmetric matrices are [linear transformations](https://www.youtube.com/watch?v=kYB8IZa5AuE) that (geometrically) result in [infinitesimal rotations](https://en.wikipedia.org/wiki/Infinitesimal_rotation_matrix#Relationship_to_skew-symmetric_matrices), which is why the $Q$ portion of the flow circulates around the log density. It’s quite easy to show why the infinitesimal rotation matrix (which rotates a given vector by $d\theta$) is antisymmetric in two dimensions.

The matrix below [rotates a given vector by $\theta$](https://math.stackexchange.com/questions/852530/whats-the-intuition-behind-the-2d-rotation-matri):

$$

M = \begin{bmatrix}

\cos \theta & -\sin \theta \\

\sin \theta & \cos \theta

\end{bmatrix}

$$

We want to find a matrix that rotates an input vector by $\theta$ as $\lim_{\theta \to 0} \theta = d \theta$. As $\lim_{\theta \to 0}$, $\cos \theta \to 1$ and $\sin \theta \to d\theta$. Thus our original rotation matrix becomes

$$

M = \begin{bmatrix}

1 & -d\theta \\

d\theta & 1

\end{bmatrix}

$$

We can rewrite this as

$$

M = \begin{bmatrix}

1 & 0 \\

0 & 1

\end{bmatrix} + \begin{bmatrix}

0 & -d\theta \\

d\theta & 0

\end{bmatrix} = I + A

$$

where $I$ is the identity matrix, and $A$ is the matrix on the right. Note that $A = -A^T$ is antisymmetric!

Hopefully this example gives you some idea of why antisymmetric matrices represent infinitesimal rotation.

  

The Helmholtz decomposition of the flow function, in addition to telling us that the the flow on the states will try to maximize $\ln(p(x))$ also tells us something else.

  

Specifically, the solenoidal flow $Q$ tells us that our system is *not only* at steady-state, but actually at a specific *type* of steady-state: [**non-equilibrium** steady state](https://en.wikipedia.org/wiki/Non-equilibrium_thermodynamics) (NESS).

  

- At equilibrium steady-state, the behavior of a system is time-reversible. That is, if you observe the dynamics of the system at equilibrium, you cannot tell if time is running forwards or backwards (ex: inside a cup, when tea has fully dissolved into milk).

- Non-equilibrium steady states are *not* time-reversible: the dynamics of the system at equilibrium do not look the same if time runs forwards vs backwards (ex: inside a cup, when tea has fully dissolved into milk, but someone is constantly stirring the tea; if you reverse the dynamics, the stirring will go from clockwise to counterclockwise, or vice versa).

  

The solenoidal flow $Q$ indicates that we are at NESS because this part of the flow renders the system time-irreversible – if you reverse clockwise motion it looks counterclockwise, and vice versa. The $\Gamma$ portion of the flow, on the other hand, is completely time reversible (since $\omega$ opposes it exactly by descending on the log density with the same magnitude $\Gamma$; on average, the flows will look the same if time runs forwards vs backwards).

  

Why is the fact that we’re at NESS and not ESS important? Well, it actually reflects a pretty deep property of the types of things we’re considering. Maintaining a Markov blanket against external perturbations – as, for example, biological systems do – requires a constant influx of energy. This is why biological systems are called *dissipative structures*: they increase the entropy of the environment to maintain constant entropy within the system.

  

Finally, notice that $f(x) = (\Gamma - Q)\nabla_x \ln p(x)$ is equivalent to $f(x) = (Q - \Gamma)\nabla_x -\ln p(x)$. The former expression tells us the flow at NESS will try to *maximize* the log density $\ln p(x)$; the latter expression tells us the flow at NESS will try to *minimize* the negative log density $- \ln p(x)$ since the $\Gamma$ portion of the flow (which originally climbed up the log density) has been flipped. Why I’m pointing this out might seem mysterious and trivial for now, but I promise it will make sense later. The second interpretation is actually quite important.

  

Now we are left with some questions. What’s the significance of $-\ln p(x)$? And why does the flow $f(x)$ minimize this quantity at NESS? The answer to these questions will (finally!!) lead us to variational free energy.

  

<aside>

🔄

  

**Recap**

  

In this section we’ve (1) laid out a really general setup that describes a wide range of physical systems, (2) slotted in our first thingness condition (the **steady-state assumption**) and (3) interpreted the resultant equation that describes the dynamics at steady state.

  

- **Langevin dynamics:** A wide range of physical systems can be described by the differential equation $\frac{dx}{dt} = f(x) + \omega$ where $f(x)$ is some flow function and $\omega$ is normally distributed noise with variance $\Gamma$.

- **Fokker-Planck equation:** We can rewrite the Langevin equation in terms of the change of probability density on states w.r.t. $\frac{dp(x,t)}{dt}$ instead of the change of the states themselves w.r.t. $\frac{dx}{dt}$. This is useful because it allows us to neatly slot in one of our thingness conditions.

- **Steady-state assumption:** The steady-state thingness conditions is that $\frac{dp(x,t)}{dt} = 0$. Thus we can set the Fokker-Planck equation to $0$ and solve for $f(x)$ in terms of $p(x)$. This directly answers our initial question, since $f(x)$ is the flow function that describes the dynamics of the thing at steady-state.

- **Helmholtz decomposition:** We find via the Helmholtz decomposition that $f(x) = (\Gamma - Q) \nabla_x \ln p(x)$ satisfies the steady-state condition, i.e. it makes $\frac{dp(x,t)}{dt} = 0$.

- The $\Gamma$ part of the flow climbs the log density, allowing the thing to stay within the small set of its characteristic states (which keeps its Markov blanket intact) in the face of random fluctuations $\omega$.

- The $Q$ part of the flow circulates around the log density, making the dynamics *time-irreversible*, rendering the steady-state a *non-equilibrium* steady state (NESS). This property reflects the fact that biological systems are dissipative structures that perform processes to increase the entropy of their environment to maintain the system’s internal entropy.

  

Our initial question

  

> Given a **self-organizing thing that maintains its Markov blanket**, **what must the dynamics of that thing’s autonomous states be at steady state**?

>

  

now has a preliminary answer: the dynamics of that thing are described by the equation

  

$$

f(x) = (\Gamma - Q)\nabla_x \ln p(x)

$$

  

or equivalently as

  

$$

f(x) = (Q - \Gamma)\nabla_x -\ln p(x)

$$

  

But notice that:

  

- Our equation describes the flow on all the states, whereas we really only care about the flow on **autonomous** states. We haven’t applied the Markov blanket condition yet! (We will do this later.)

- We don’t know what the significance of $-\ln p(x)$ is, and why the dynamics at NESS minimize this quantity. We will explore this in the next section.

</aside>

  

## III. Interlude: variational **free energy**

  

In this section I’ll be trying to explain an important concept – variational inference – from the bottom up. Eventually this will lead us to why $-\ln p(x)$ is important. Things might not immediately make sense or connect for a while, but they will eventually.

  

### I want to infer stuff but I hate adding

  

Suppose that the world has a simple causal structure $u \to v$, that we can only observe $v$ but not $u$, and that we’re trying to compute the posterior probability $p(u \mid v)$. (Thus $u$ is called a hidden state and $v$ is called an observable state.) Assume we only have access to some generative model factored in terms of the prior distribution and the likelihood distribution, i.e. $p(u, v) = p(u) \cdot p(v \mid u)$.

  

To compute $p(u \mid v)$ exactly we’d have to use [Bayes theorem](https://youtu.be/HZGCoVF3YvM?si=QpHgFNbLDLoKu-vr):

  

$$

p(u \mid v) = \frac{p(u,v)}{p(v)}

$$

  

We’d have to compute the term in the denominator $p(v)$ by [marginalizing](https://en.wikipedia.org/wiki/Marginal_distribution) over the joint probability distribution, i.e. calculating $\sum_{u}^{} p(u,v)$. In many cases this quantity is intractable because $u$ is really large, so the sum is hard to calculate. It gets even worse if we’re dealing with probability densities instead of probability distributions and – ew, disgusting integrals.

  

So… how can we compute $p(u \mid v)$ without calculating $p(v)$?

  

The solution is to turn this inference problem into an optimization problem. That is, suppose we create some simpler probability distribution parametrized by $\phi$, $q_\phi(u)$. And further suppose we compute $p(u \mid v)$ by adjusting $\phi$ such that the approximate distribution $q_\phi(u)$ gets closer and closer to $p(u \mid v)$. This way we won’t have to directly calculate $p(v)$ at all!

  

### KL Divergence

  

But first, we need a way to measure the difference between two probability distributions so that we have a metric to minimize. The standard way to measure how different a probability distribution $P$ is from another distribution $Q$ is [KL divergence](https://en.wikipedia.org/wiki/Kullback%E2%80%93Leibler_divergence#Properties), which is defined as the [expected value](https://en.wikipedia.org/wiki/Expected_value) on $P$ of $\log(P) - \log(Q)$, i.e.

  

$$

D_\text{KL}[P \mid\mid Q] = \mathbb{E}_P[\log(P) - \log(Q)]

  

$$

  

Note that KL divergence is not symmetric, i.e. $D_\text{KL}[P \mid\mid Q] \neq D_\text{KL}[Q \mid\mid P]$ and that KL divergence is always non-negative.

  

- Background on KL divergence

There are [many ways to (explain) and arrive at KL divergence](https://www.lesswrong.com/posts/no5jDTut5Byjqb4j5/six-and-a-half-intuitions-for-kl-divergence). This is only one of them, and probably(?) the most relevant in this context.

The big picture idea here is that $D_\text{KL}[P \mid\mid Q]$ measures how surprised you would be, if you found out that $P$ was the true probability distribution instead of $Q$. To rephrase this another way: you’re treating $P$ as the [territory](https://en.wikipedia.org/wiki/Map%E2%80%93territory_relation) and $Q$ as your [map](https://en.wikipedia.org/wiki/Map%E2%80%93territory_relation), and measuring how surprised you’d be (by the territory) if you treated your map as the territory.

The first thing we need to do is formalize a measure of surprise. There’s already a concept for this called [surprisal](https://charlesfrye.github.io/stats/2016/03/29/info-theory-surprise-entropy.html) from information theory defined as $I(p) = -\log(p) = \log(\frac{1}{p})$.

From here, it’s quite straightforward to see (intuitively) why the definition of KL divergence measures what we want it to measure. We’re taking the expectation over $P$ because we want to take the weighted average of how surprised we are over each possible state of reality.

$$

\begin{align*}

D_\text{KL}[P \mid\mid Q] &= \mathbb{E}_P[\text{how surprised by the model?} - \text{how surprised by reality?}] \\

&= \mathbb{E}_P[I(Q) - I(P)] \\

&= \mathbb{E}_P[-\log(Q) + \log(P)] \\

&= \mathbb{E}_P[\log(P) - \log(Q)]

\end{align*}

$$

  

The quantity that we will be trying to minimize is $D_\text{KL}[q_\phi \mid\mid p] = \mathbb{E}_{q_\phi(u)}[\log(q_\phi) - \log(p)]$. But wait… why not go the other way? Why not minimize $D_\text{KL}[p \mid\mid q_\phi]$ instead? KL divergence is not symmetric, so how do we know which way is “right”?

  

We actually *cannot* go the other way, i.e. we cannot compute $D_\text{KL}[p \mid\mid q_\phi] = \mathbb{E}_{p(u \mid v)}[\log(p) - \log(q_\phi)] = \sum_{u} p(u \mid v) \cdot [\log(q_\phi) - \log(p)]$. Because the fact that we don’t know $p(u \mid v)$ is why we’re trying to minimize KL divergence in the first place! Thus we are forced to minimize the *reverse* KL divergence $D_\text{KL}[q_\phi \mid\mid p]$, instead of the forward KL divergence $D_\text{KL}[p \mid\mid q_\phi]$.

  

We still have a problem, though. Calculating $D_\text{KL}[q_\phi(u) \mid\mid p(u \mid v)]$ still requires us to know $p(u \mid v)$ which… we obviously don’t, because this is what we are trying to compute in the first place. So somehow, we need to rewrite the reverse KL divergence into a quantity we *do* know how to minimize.

  

### Rewriting KL divergence

  

$$

\begin{align*}

D_\text{KL}[q_\phi \mid\mid p] &= \sum_{u} q_\phi(u) \cdot [\log q_\phi(u) - \log p(u \mid v)] \\

&= \sum_{u} q_\phi(u) \cdot \log \frac{q_\phi(u)}{p(u \mid v)} \\

&= \sum_{u} q_\phi(u) \cdot \log\frac{q_\phi(u) \cdot p(v)}{p(u, v)} && \text{Bayes theorem} \\

&= \sum_{u} q_\phi(u) \cdot [\log\frac{q_\phi(u)}{p(u, v)} + \log p(v)]\\

&= \sum_{u} q_\phi(u) \cdot \log\frac{q_\phi(u)}{p(u, v)} + \sum_{u} q_\phi(u)\log p(v) \\

&= \sum_{u} q_\phi(u) \cdot \log\frac{q_\phi(u)}{p(u, v)} + \log p(v) \\

\end{align*}

$$

  

In the last line, the $\sum$ disappears since $\log p(v)$ does not depend on $u$ and $q_\phi(u)$ sums to $1$ because it is a probability distribution.

  

Notice that the final expression we obtain has two parts, one of which is dependent on $\phi$ and the other of which is not:

  

$$

D_\text{KL}[q_\phi(u) \mid\mid p(u \mid v)] = \underbrace{\sum_{u} q_\phi(u) \cdot \log\frac{q_\phi(u)}{p(u, v)}}_{\text{depends on }\phi} + \underbrace{\log p(v)}_{\text{does not depend on }\phi}

$$

  

So since we’re trying to adjust $\phi$ to minimize $D_\text{KL}[q_\phi \mid\mid p]$, we actually only care about minimizing the part of the expression that depends on $\phi$. Let’s give this part a special name: **variational free energy (VFE)**, and denote it $F[q_\phi, p]$. (Yay! We finally got to the “free energy” part of “Free Energy Principle”.)

  

Notice that

  

$$

\begin{align*}

F[q_\phi, p] &= \sum_{u} q_\phi(u) \cdot \log\frac{q_\phi(u)}{p(u, v)} \\

&= \mathbb{E}_{q_{\phi}(u)} [\log q_\phi(u) - \log p(u,v)] \\

&= D_\text{KL}[q_\phi(u) \mid\mid p(u,v)]

\end{align*}

$$

  

What just happened here? After a bunch of symbol shuffling, we’ve rewritten the quantity we initially wanted to minimize by adjusting $\phi$ but couldn’t, $D_\text{KL}[q_\phi(u) \mid\mid p(u \mid v)]$, into a quantity that we actually *can* minimize: $D_\text{KL}[q_\phi(u) \mid\mid p(u, v)]$. We’ve figured out how to approximate the posterior $p(u \mid v)$ when you can’t marginalize over $p(u, v)$ to calculate $p(v)$: **just minimize VFE**.

  

There turns out to be lots of other interesting ways to rewrite VFE: some have interesting theoretical implications and map on nicely to biological theories and theories of cognition; others are practically useful for computing it.

  

Also notice that if we arrange the last line of our initial attempt to rewrite $D_\text{KL}[q_\phi \mid\mid p]$ we get

  

$$

F[q_\phi, p] = D_\text{KL}[q_\phi(u) \mid\mid p(u \mid v)] - \log p(v)

$$

  

This decomposition is impractical if we want to calculate VFE, but is conceptually significant for our attempt to understand how the FEP is derived. Notice that

  

$$

D_\text{KL}[q_\phi(u) \mid\mid p(u\mid v)] \geq 0 \implies -\log p(v) \leq F[q_\phi, p]

$$

  

**In other words, $-\log p(v)$ is a lower bound on VFE**. This is very important. Keep this in mind.

  

<aside>

🔄

  

**Recap**

  

In this section we’ve established that (1) minimizing VFE is equivalent to approximate Bayesian inference – i.e. computing the posterior probability without using Bayes theorem and (2) $-\log p(\text{blah})$ is a lower bound on VFE.

  

Our initial question was

  

> Given a **self-organizing thing that maintains its Markov blanket**, **what must the dynamics of that thing’s autonomous states be at steady state**?

>

  

We are quite close to answering it! In the next section, we will:

  

- Find an expression for the flow on *autonomous states* at NESS, specifically (rather than our previous equation which expressed the flow on *all the states* at NESS)

- Conceptually link that expression with VFE and interpret what this means

</aside>

  

## IV. Finally answering the question!

  

In this section, we will finally obtain a formal answer to our question posed at the beginning.

  

### Marginal flow lemma

  

> Given a **self-organizing thing that maintains its Markov blanket**, **what must the dynamics of that thing’s autonomous states be at steady state**?

>

  

We can *almost* answer our question with the Helmholtz decomposition we obtained earlier:

  

$$

f(x) = (\Gamma - Q)\nabla_x \ln p(x)

$$

  

The only thing left to do now is to find an equation that describes the flow of **autonomous states** $\alpha = \{a, i\}$ at NESS. But to do this, we first need to define what it even means to express the flow of a subset of states.

  

Suppose we want to express the flow of some subset of states $\eta$, conditioned on us knowing the values of some other subset of states $\mu$. To compute this quantity $f_\eta(\mu)$, we have to [marginalize out](https://math.stackexchange.com/questions/1511622/what-does-it-mean-to-marginalise-out-something) the effects of $\tilde\mu$, i.e. we need to integrate over the joint distribution $f_\eta(\mu, \tilde{\mu})$ and weight the integrand by $p(\tilde{\mu} \mid \mu)$. Thus we can define $f_\eta(\mu)$ as

  

$$

f_\eta(\mu) := \mathbb{E}_{p(\tilde{\mu} \mid \mu)}[f_\eta(\mu, \tilde{\mu})] = (\Gamma_{\eta\eta} - Q_{\eta\eta}) \nabla_\eta \ln p(\mu) - Q_{\eta\tilde{\eta}} \nabla_\eta \ln p(\mu)

$$

  

The second equality holds due to the marginal flow lemma which we prove below.

  

- Proof of marginal flow lemma

We want to prove $f_\eta(\mu) = (\Gamma_{\eta\eta} - Q_{\eta\eta}) \nabla_\eta \ln p(\mu) - Q_{\eta\tilde{\eta}} \nabla_\eta \ln p(\mu)$.

We will start by obtaining an expression for $f_\eta(x) = f_\eta(\tilde{\mu} ,\mu)$ by [partitioning](https://en.wikipedia.org/wiki/Block_matrix) the Helmholtz decomposition $f(x) = (\Gamma - Q) \nabla_x \ln p(x)$ into a system of equations

$$

\begin{bmatrix}

f_\eta(x) \\

f_{\tilde{\eta}}(x)

\end{bmatrix}

=

\begin{bmatrix}

\Gamma_{\eta\eta} - Q_{\eta\eta} & - Q_{\eta\tilde\eta} \\

{Q_{\eta\tilde\eta}}^T & \Gamma_{\tilde\eta\tilde\eta} - Q_{\tilde\eta\tilde\eta}

\end{bmatrix}

\begin{bmatrix}

\nabla_\eta \ln p(x) \\

\nabla_{\tilde{\eta}} \ln p(x)

\end{bmatrix}

$$

- Notes

- $\Gamma_{\eta\tilde{\eta}}$ and $\Gamma_{\tilde\eta{\eta}}$ are matrices of all zeroes because $\Gamma$ is a scaled identity matrix

- $Q = -Q^T$ by definition so $-Q_{\tilde\eta\eta} = {Q_{\eta\tilde\eta}}^T$

Let $A = \int \frac{\nabla_\eta p(\mu, \tilde{\mu})}{p(\mu, \tilde{\mu})}$ for convenience and the sake of Ariel’s fingers.

Substituting the expression for $f_\eta(x)$ into the definition of marginal flow (line 3), we get

$$

\begin{align*}

f_\eta(\mu)&:= \mathbb{E}_{p(\tilde{\mu} \mid \mu)}[f_\eta(\mu, \tilde{\mu})]\\

&= \int f_\eta(\mu, \tilde{\mu}) p(\tilde{\mu} \mid \mu)d\tilde{\mu} \\

&= \int [(\Gamma_{\eta\eta} - Q_{\eta\eta}) \nabla_\eta \ln p(x) - Q_{\eta\tilde{\eta}} \nabla_{\tilde{\eta}} \ln p(x)] \cdot p(\tilde{\mu} \mid \mu) d\tilde{\mu} \\

&= \int [(\Gamma_{\eta\eta} - Q_{\eta\eta}) \frac{\nabla_\eta p(\mu, \tilde{\mu})}{p(\mu, \tilde{\mu})} - Q_{\eta\tilde{\eta}}\frac{\nabla_\eta p(\mu, \tilde{\mu})}{p(\mu, \tilde{\mu})}] \cdot p(\tilde{\mu} \mid \mu) d\tilde{\mu} \\

&= \int [(\Gamma_{\eta\eta} - Q_{\eta\eta}) \nabla_\eta p(\mu, \tilde{\mu}) - Q_{\eta\tilde{\eta}} \nabla_\eta p(\mu, \tilde{\mu})] \cdot \frac{p(\tilde{\mu} \mid \mu)}{p(\mu, \tilde{\mu})} d\tilde{\mu} \\

&= (\Gamma_{\eta\eta} - Q_{\eta\eta}) \int \nabla_\eta p(\mu, \tilde{\mu}) \cdot \frac{p(\tilde{\mu} \mid \mu)}{p(\mu, \tilde{\mu})} d\tilde{\mu} - Q_{\eta\tilde{\eta}} \int \nabla_\eta p(\mu, \tilde{\mu}) \cdot \frac{p(\tilde{\mu} \mid \mu)}{p(\mu, \tilde{\mu})} d\tilde{\mu} \\

&= (\Gamma_{\eta\eta} - Q_{\eta\eta}) \int \frac{\nabla_\eta p(\mu, \tilde{\mu})}{p(\mu)} d\tilde{\mu} - Q_{\eta\tilde{\eta}} \int \frac{\nabla_\eta p(\mu, \tilde{\mu})}{p(\mu)} d\tilde{\mu} \\

&= (\Gamma_{\eta\eta} - Q_{\eta\eta}) \cdot A - Q_{\eta\tilde{\eta}} \cdot A

\end{align*}

$$

- Notes

- Line 3: substitute expression for $f_\eta(x) = f_\eta(\mu, \tilde{\mu})$ from the partitioned matrix system of equations above

- Line 4: application of chain rule on $\nabla_\eta \ln p(x)$

We can simplify the integral $A = \int \frac{\nabla_\eta p(\mu, \tilde{\mu})}{p(\mu, \tilde{\mu})}$

$$

\begin{align*}

\int \frac{\nabla_\eta p(\mu, \tilde{\mu})}{p(\mu)} d\tilde{\mu} &= \int \frac{\nabla_\eta [p(\mu) \cdot p(\tilde{\mu} \mid \mu)]}{p(\mu)} d\tilde{\mu} \\

&= \int \frac{p(\mu) \nabla_\eta p(\tilde{\mu} \mid \mu) + p(\tilde{\mu} \mid \mu) \nabla_\eta p(\mu)}{p(\mu)} d\tilde{\mu} \\

&= \int \frac{p(\mu) \nabla_\eta p(\tilde{\mu} \mid \mu)}{p(\mu)} d\tilde{\mu} + \int \frac{p(\tilde{\mu} \mid \mu) \nabla_\eta p(\mu)}{p(\mu)} d\tilde{\mu} \\

&= \int \nabla_\eta p(\tilde{\mu} \mid \mu) d\tilde{\mu} + \frac{\nabla_\eta p(\mu)}{p(\mu)} \int p(\tilde{\mu} \mid \mu) d\tilde{\mu} \\

&= \int \nabla_\eta p(\tilde{\mu} \mid \mu) d\tilde{\mu} + \frac{\nabla_\eta p(\mu)}{p(\mu)} \\

&= \frac{\nabla_\eta p(\mu)}{p(\mu)}

\end{align*}

$$

- Notes

- Line 4: we can take $\frac{\nabla_\eta p(\mu)}{p(\mu)}$ out of the integral because it doesn’t depend on $\tilde{\mu}$ the variable we’re integrating over

- Line 5: the integral over the entire domain of any probability density is $1$

- Line 6: the average change of any probability density over the entire domain $\int \nabla_\eta p(\tilde{\mu} \mid \mu) d\tilde{\mu}$ is $0$.

- Intuitively, this is because the integral over the entire domain of any probability density is $1$.

- Thus if the density function increases in one region, it must decrease (on net) by the same amount in another region. Hence the average change is $0$ because these local changes “cancel each other out”

Substituting $I$ back into our expression for $f_\eta(\mu)$ we get

$$

\begin{align*}

f_\eta(\mu)

&= (\Gamma_{\eta\eta} - Q_{\eta\eta}) \frac{\nabla_\eta p(\mu)}{p(\mu)} - Q_{\eta\tilde{\eta}}\frac{\nabla_\eta p(\mu)}{p(\mu)} \\

&= (\Gamma_{\eta\eta} - Q_{\eta\eta}) \nabla_\eta \ln p(\mu) - Q_{\eta\tilde{\eta}} \nabla_\eta \ln p(\mu) \square

\end{align*}

$$

- Notes

- Line 3: $\nabla_\eta \ln p(\mu) = \frac{\nabla_\eta p(\mu)}{p(\mu)}$ because chain rule

  

If we further assume that the second solenoidal coupling term $Q_{\eta\tilde{\eta}} \nabla_\eta \ln p(\mu) = 0$, we can express the marginal flow of $\eta$ purely in terms of the gradient of $\eta$

  

$$

f_\eta(\mu) = (\Gamma_{\eta\eta} - Q_{\eta\eta}) \nabla_\eta \ln p(\mu)

$$

  

### Free energy lemma

  

We can apply the marginal flow lemma to finally answer our question.

  

To find the flow of autonomous states $f_\alpha$ given that we know the values of all the states that make up the system (internal states, active states, sensory states), we can apply the marginal flow lemma, setting $\eta = \alpha$ and $\mu = (a, i, s) = (\alpha, s)$ to get

  

$$

f_\alpha(i,s,a) = (\Gamma_{\alpha\alpha} - Q_{\alpha\alpha}) \nabla_\alpha \ln p(i,s,a)

$$

  

or equivalently

  

$$

f_\alpha(i,s,a) = (Q_{\alpha\alpha} - \Gamma_{\alpha\alpha}) \nabla_\alpha -\ln p(i,s,a)

$$

  

This expression means that at NESS, the flow of autonomous states given the values of the states that make up the system will *descend on*, or minimize $-\ln p(i,s,a)$.

  

Recall that $-\ln p(i, s, a)$ is the *lower bound* on VFE. This follows from our definition above of $F[q_\phi, p] = D_\text{KL}[q_\phi(u) \mid\mid p(u \mid v)] - \log p(v)$ if we set the hidden variable to $u = e$ and the observable variables to $v = i,s,a$.

  

Thus if we assume that $D_\text{KL} \approx 0$ which implies $F \approx - \ln p(i, s, a)$ then

  

$$

f_\alpha(i,s,a) \approx (Q_{\alpha\alpha} - \Gamma_{\alpha\alpha}) \nabla_\alpha F

$$

  

In other words, we can interpret the flow of autonomous states at NESS as descending on (or minimizing) variational free energy, i.e. approximating approximate Bayesian inference on the external states. This is the **free energy lemma**! Yay, we have finally arrived at what we’ve set out to show!

  

Let’s take a step back to see what we’ve actually done here. We’ve formalized the reason for **why things that maintain their thingness appear to model (or represent) their environments.** Our answer is: for a certain definition of thing, the FEP is true, which means that the flow on the autonomous states of the thing at NESS *approximate* approximate Bayesian inference on hidden (external) states. This is very much related to Ashby’s [good regulator theorem](https://en.wikipedia.org/wiki/Good_regulator).

  

We’ve also established what **things must do, by virtue of their thingness**: any thing which fits our definition of thing *must* minimize variational free energy at NESS. This tells us a surprising amount, because VFE can be decomposed in a surprisingly large number of (meaningful) ways:

  

![Source: [https://www.sciencedirect.com/science/article/pii/S037015732300203X](https://www.sciencedirect.com/science/article/pii/S037015732300203X)](Things!%20FEP%20Explained,%20Part%201%20118fcfd4925d8035ba35c1609bd81243/1-s2.0-S037015732300203X-gr7_lrg.jpg)

  

Source: [https://www.sciencedirect.com/science/article/pii/S037015732300203X](https://www.sciencedirect.com/science/article/pii/S037015732300203X)

  

There is a way in which we’ve looped back around to right where we started. We started by assuming that (1) things exist over time, and (2) asking ourselves what things must do given this. The conclusion we’ve obtained is essentially a (very precise) tautology: the free energy lemma formally states that “things which exist over time will continue existing over time” $\iff$”things will minimize VFE”.

But we have also, somewhat paradoxically, gained some new information from this tautology. We’ve obtained a general method for modeling what things must do falsifiably (which fall under the FEP definition of thingness): (1) specify the internal, external, sensory and active states of the thing of interest and (2) specify the probability distribution over them.

Finally, the FEP is also useful because it suggests that every behavior a “thing” exhibits (even behaviors conventionally thought of to have different objectives, such as action and perception) can be cast as some form of minimization of variational free energy. This has inspired various process theories that aim to make more concrete predictions such as active inference, predictive coding and even theories of autism.

Personally, I think that the FEP is interesting because it prompts us to zoom out drastically on the scale of abstraction and generality – and in doing so we now have a better idea of what, where, and how to zoom *in* when trying to predict how particular systems will behave.
