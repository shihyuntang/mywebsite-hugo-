---
title: Bayes' theorem 
linktitle: Bayes' theorem 
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

Bayes Theorem is a fundamental principle in probability theory and statistics that describes how to update the probability of a hypothesis based on new evidence. It is particularly powerful in the context of predictive modeling and decision-making processes.

### Mathematical Formulation

If events $A$ and $B$ are independent, then the probability of $A$ given $B$ is simply the probability of $A$:
$$
  P(A|B) = P(A)
$$
However, when events $A$ and $B$ are not independent, the relationship changes as follows:
$$
  P(A|B) = \frac{P(A \cap B)}{P(B)} \quad \text{and} \quad P(B|A) = \frac{P(A \cap B)}{P(A)}
$$
From these relationships, we derive Bayes' Theorem:
$$
  P(B|A) = \frac{P(B) P(A|B)}{P(A)}
$$
Bayes' Theorem can be interpreted in terms of updating beliefs:
$$
  \text{Posterior} = \frac{\text{Prior} \times \text{Likelihood}}{\text{Evidence}}
$$

### Components of Bayes' Theorem

1. **Likelihood ( $ P(A|B) $ ):**
   The likelihood is a function that measures the plausibility of a model parameter value given specific observed data. In many applications, especially in statistical modeling, the likelihood is assumed to follow a normal distribution:
   $$
      L(\theta; x) = \frac{1}{\sqrt{2\pi\sigma^2}} e^{-\frac{(x-\theta)^2}{2\sigma^2}}
   $$
   where $\theta$ represents the parameter of interest, $x$ represents the data, and $\sigma^2$ is the variance.
2. **Prior ( $ P(B) $ ):**
   The prior represents the initial belief about the distribution of the parameter before considering the current data. Priors can be subjective or based on previous studies:
   $$
      P(\theta)
   $$
   It can be uniform (representing no initial preference) or follow a specific distribution that reflects prior knowledge about the parameter, e.g., a Gaussian prior, gamma and beta distribution.
3. **Evidence or Normalizing Constant ( $ P(A) $ ):**
   Often considered as a normalizing factor, the evidence ensures that the posterior probabilities sum to one. It is calculated as:
   $$
      P(A) = \int P(A|B) P(B) dB
   $$
   This factor is essential for the probabilistic model to be valid but is usually more relevant in analytical calculations than in practical applications.
4. **Posterior ( $ P(B|A) $ ):**
   The posterior probability reflects the updated belief about the parameter after considering the new evidence. It combines the prior and the likelihood given new data:
   $$
      P(\theta|x) = \frac{P(x|\theta)P(\theta)}{\int P(x|\theta)P(\theta) d\theta}
   $$


## Practical Applications

Bayes' Theorem is used extensively in various fields including exoplanet study, machine learning, medical testing, and any scenario requiring iterative updating of beliefs upon new evidence. Understanding how to apply the theorem allows for more informed decision-making processes and predictions.

---

## Relationship Between Likelihood and Chi-Squared Statistic

The likelihood function in statistical models often measures how well a set of parameters fits the data. When the data and the model predictions vary according to a normal distribution, the likelihood function can be directly linked to the chi-squared statistic.

### Chi-Squared Statistic:
The chi-squared statistic is a measure of how expectations compare to actual observed data. In the context of likelihood calculations, the chi-squared statistic quantifies the discrepancy between observed data and the data predicted by the model, under the assumption that the discrepancies are normally distributed.

### Calculation:
To calculate the chi-squared statistic as a measure of likelihood, you can use the following formula:
$$
   \chi^2 = \sum \frac{(O_i - E_i)^2}{\sigma_i^2}
$$
where $O_i$ are the observed values, $E_i$ are the expected values predicted by the model, and $\sigma_i^2$ is the variance associated with each observation.

### Using Chi-Squared to Calculate Likelihood:
The likelihood of observing the data given the model can be expressed as:
$$
   L = e^{-\chi^2/2}
$$
A more memorable form is:
$$
   \chi^2 = -2 \ln{L}
$$
> The $\chi^2$ is just -2 times the log-likelihood of a Gaussian model on observation.
This formulation arises from the exponential component of the PDF of the normal distribution, which is what a likelihood function usually take, thus, a easier way to remember how to calculate the likelihood. 
