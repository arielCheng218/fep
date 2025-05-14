---
title: II. Paths!
draft: false
tags: 
date: "{{date}}"
aliases:
  - II. Paths!
description: This post explains the path integral formulation of the Free Energy Principle.
---
*Meta*: This article is an opinionated distillation of [Friston et al., 2022](https://arxiv.org/pdf/2205.11543).

---

In the previous post, we started out by asking:

> If **things exist**, **what must they do**?

Phrased more clearly:

> If the same thing exists over some timescale, what must the dynamics of that thing look like?

We operationalized "same thing exists over some timescale" as:
* A Markov blanket exists over that timescale
* The non-equilibrium steady state (NESS) condition is met, i.e. $\frac{dp}{dt} = 0$. 

I will define any thing that meets these two conditions as a **strongly-thing** thing, and any thing that meets the Markov blanket condition but not the NESS condition as a **weakly-thing** thing.

In this post, we will drop the NESS condition and show that weakly-thing things also minimize  free energy. More specifically, we will show that the trajectories, or paths, of weakly-thing things over time minimize variational free energy. [^1]

[^1]: We are talking about paths and trajectories, not points, because it simplifies the math.

Why are we doing this? Because we want to be able to describe weakly-thing things, because weakly-thing things are still interesting. 

Consider two examples:
- If I join a cult, my phenotype--$p(x)$--will be different before I join the cult and after I join the cult.
	- Thus I do not count as a strongly-thing thing because $\frac{dp}{dt} \neq 0$, so the Free Energy Lemma we proved last time doesn't hold.
	- But this case is still pretty interesting, and we want to be able to make statements about the dynamics of this kind of thing!
	- Also, notice that depending on the scale at which you're modeling, and the kind of thing you're modeling, the change will not necessarily sound as drastic as "join a cult".
- If I hurl myself into the sun--
	- then my Markov blanket would say bye-bye. This case and similar cases are not particularly interesting and we don't care about them, which is why we're not dropping the Markov blanket assumption.

The other reason we care about weakly-thing things is that the equations look much friendlier, and we like friendly equations! What we proved last time turns out to be a messy special case. An interesting and important special case, to be sure, but a messy one nonetheless.

# I. From paths to surprisal

## Setup

We will start in the same place we did last time: by assuming that our system can be modeled with our old friend the Langevin equation
$$ \frac{dx}{dt} = f(x) + \omega(t)$$
where
- $x \in \mathbb{R}^n$ is our vector of states
- $f \in \mathbb{R}^n$ is the deterministic component of the flow
- $\omega \in \mathbb{R}^n$ is the noise component of the flow that's normally distributed with mean $0$ and covariance $2\Gamma$[^2].

[^2]: This assumption is justified by [the central limit theorem](https://youtu.be/zeJD6dqJ5lo?si=xh1ZPMHvEjS7NVJO).

Now we're going to do something different. We're going to talk about the *paths* our system will take (the trajectory of $x$ over time); *not* the states of our system themselves, $x$; and *not* the probability distributions of those states, which would be $p(x)$.

We do this by defining a new quantity called a generalized coordinate: $\vec{x} = \left < x, x', \dots x^{(m)}\right > \in \mathbb{R}^{n \times m}$. If we let the components of this vector represent the [coefficients of a Taylor series](https://youtu.be/3d6DsjIBzJ4?si=S_gv6UnvEZMgZVmG), we will have a one-to-one correspondence between paths and generalized coordinates and $\vec{x}$ now represents a path[^3].

[^3]: Note that $\vec{x}$ only represents the trajectory of $x$ on a short timescale. The more components we add to $\vec{x}$, i.e. the larger $m$ is, the better the approximation, and the longer $\vec{x}$ actually corresponds to the real path of the system. 

Now we will rewrite the Langevin equation in terms of $\vec{x}$. First