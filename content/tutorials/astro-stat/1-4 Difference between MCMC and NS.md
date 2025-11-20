---
title: Difference Between MCMC and NS
linktitle: MCMC vs. NS 
toc: true
type: docs
date: "2024-05-02T00:00:00+01:00"
draft: false
menu:
  astro-stat:
    parent: 1 Probability
    weight: 4

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 4
---

Both **Markov Chain Monte Carlo (MCMC)** and **Nested Sampling (NS)** are Bayesian inference techniques. They both rely on Bayes’ theorem, but they explore parameter space in fundamentally different ways. The biggest conceptual contrast is:

- **MCMC samples in the *posterior* space**.
- **NS samples in the *prior* space**, gradually restricting it to higher-likelihood regions.

Before digging into the differences, let’s recall Bayes’ theorem:
$$
  \text{Posterior}(\mathcal{P}) = \frac{
   \text{Likelihood}(\mathcal{L}) \times \text{Prior($\\pi$)}}{\text{Evidence($\mathcal{Z}$)}}
$$
$$
   \mathcal{P}(\theta|x) 
   = \frac{ 
      \mathcal{L}(x|\theta)\times \pi(\theta)
      }{\int \mathcal{L}(x|\theta) \pi(\theta) d\theta
      }
$$

--- 

## Markov Chain Monte Carlo (MCMC)

MCMC focuses directly on sampling from the **posterior distribution**. The idea is simple:

1. **Start with an initial guess** for the parameters ($\theta$) for each *walker*.
2. For each proposed step, compute  
   - the likelihood: $\mathcal{L}(\theta) = P(x|\theta)$
   - the prior: $\pi(\theta) = P(\theta)$
3. Combine them to get the **unnormalized posterior**:
   $$
      \mathcal{P}(\theta|x) \propto \mathcal{L}(\theta)\pi(\theta)
   $$
   (We ignore the evidence because it’s just a constant normalization factor.)
4. Use this posterior to decide whether the walker accepts or rejects the proposed move...

Over time, the chain spends more time in regions where the posterior is high. This produces samples distributed according to the true posterior — which is why we say that **MCMC samples from the posterior**.

MCMC is excellent for **parameter estimation**, but it does not naturally compute the **evidence**, which is required for comparing between different models.

---

## Nested Sampling (NS)

Nested Sampling takes a very different approach from MCMC.  
Instead of wandering around the posterior, NS **systematically explores the prior**, gradually shrinking it toward regions of higher likelihood.

The basic flow looks like this:

1. **Initialize a set of random parameters** (called *live points*)  
   These are drawn directly from the prior distribution $\pi(\theta)$.

2. For each live point, compute the likelihood:  
   $$
   \mathcal{L}(\theta) = P(x \mid \theta).
   $$

3. **Identify the live point with the lowest likelihood** and remove it.  
   This becomes a *dead point* (a point we won't revisit, but it *will* help build the posterior).

4. **Replace it** with a new sample drawn from the prior, **subject to a constraint:**  
   the new point must have a likelihood higher than the one just removed.  
   This gradually forces the live points into smaller and smaller regions of higher likelihood.

5. We repeat steps 3–4 many times. Eventually, the remaining prior volume becomes so small (or the change in the evidence becomes negligible) that continuing does not help, and we stop.

And this is why we say that **NS samples from the prior**!

---

## More About NS

At the stopping point (after step 5), what do we have?

- A list of **dead points** $\theta_i$ with likelihoods  
  $$
  \mathcal{L}_i = \mathcal{L}(\theta_i).
  $$
- An estimate of the **remaining prior volume** $X_i$ at each iteration,  
  which tells us how much of the prior space is left when that point is removed.

To compute the posterior, we first need the normalization factor: the **Evidence**.

### Evidence ($\mathcal{Z}$)

Recall that the evidence is:

$$
  \mathcal{Z} = \int P(x \mid \theta)\ \pi(\theta)\ d\theta,
$$

the **volume under the likelihood curve, weighted by the prior**.

Directly computing this in many dimensions is hard.  
But NS cleverly tracks how the prior volume shrinks as we move to higher likelihoods.

Define the remaining prior volume as:

$$
   X(\lambda) = \int_{\mathcal{L}(\theta) > \lambda} \pi(\theta) d\theta,
$$

the fraction of prior volume where $\mathcal{L} > \lambda$.

Skilling (2004) showed that the evidence ($\mathcal{Z}$) then becomes a **1D integral** over this volume:
$$
   \mathcal{Z} = \int_0^1 \mathcal{L}(X)\ dX.
$$

NS approximates this integral by a sum over the dead points:

$$
   Z \approx \sum_i L_i \ \Delta X_i
               = \sum_i L_i (X_{i-1} - X_i).
$$


### Unnormalized Posterior (the weight $w_i$)

Each dead point represents a slice of the shrinking prior volume. The **unnormalized posterior contribution** for each dead point is:

$$
  w_i = L_i\ (X_{i-1} - X_i),
$$
which reads as: **likelihood of that slice × size of that slice in prior volume**.

This automatically gives:
$$
   \mathcal{Z} \approx \sum_i w_i.
$$

### Posterior ($\mathcal{P}$)

Once we have the weights and the evidence, the posterior samples are simply:

$$
   \mathcal{P}(\theta_i \mid x) = \frac{w_i}{\mathcal{Z}} = \frac{w_i}{\sum_i w_i}.
$$

That’s it — the dead points (with the right weights) become your posterior samples.


--- 

## NS in the Python `dynesty` Package

Here we connect the quantities discussed above to the actual outputs of a Nested Sampling
run using the Python package **dynesty**:

```python
logl      = results.logl       # log-likelihoods of dead points
logwt     = results.logwt      # log-weights (unnormalized posterior weights)
logvol    = results.logvol     # log prior volumes of dead points
logz      = results.logz       # cumulative log-evidence estimates
```

All of these correspond directly to the core definitions of Nested Sampling.

Note, dynesty includes an extra final contribution from the last batch of
live points. That means:
* `logwt[:-1]`: weights from dead points only
* `logwt[-1]`: contribution from remaining live points at termination


