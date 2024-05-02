---
title: Distributions
linktitle: Distributions
toc: true
type: docs
date: "2024-04-29T00:00:00+01:00"
draft: false
menu:
  astro-stat:
    parent: 1 Probability
    weight: 3

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 3
---

## Probability Distributions

Probability distributions describe how the probabilities of a **random variable** are distributed. Here are the two main types of probability functions associated with these distributions:

1. **Probability Density Function (PDF, continuous):**
   - **Description:** The PDF is used to specify the probability of a random variable falling within a particular range of values, rather than taking any one specific value. This function is applicable only to continuous variables.
   - **Key Characteristic:** The area under the PDF curve between two points represents the probability of the variable falling within that range.
   - **Example:** The normal distribution.

2. **Probability Mass Function (PMF, discrete):**
   - **Description:** The PMF is used for discrete random variables and specifies the probability that a random variable is exactly equal to some value.
   - **Key Characteristic:** The sum of all the probabilities represented by the PMF must equal 1, as it accounts for every possible discrete value the variable can take.
   - **Example:** The binomial distribution, and the Poisson distribution.

**Cumulative Distribution Function (CDF):**
   - **Description:** The CDF is used to determine the probability that a random variable \(X\) is $\lesssim$ to a certain value. CDF can be applied to both discrete and continuous random variables.
   - **Key Characteristic:** The CDF is a non-decreasing function that ranges from 0 to 1. For continuous variables, it is obtained by integrating the PDF over the range of possible values. For discrete variables, it is the cumulative sum of the PMF.
   - **Example:** For normal distribution, the CDF is used to calculate the probability that the variable is less than a specific threshold, which is central to hypothesis testing and confidence interval estimation.

---
## Chebyshev's Theorem

Chebyshev's Theorem, also known as Chebyshev's Inequality, is a fundamental result in probability theory that provides a way **to estimate the probability that a random variable differs from its mean**. This theorem is not restricted to normally distributed data, making it very versatile.

**Theorem Statement:**
$$
P(|X-\mu| < k\sigma) \geq 1 - \frac{1}{k^2}
$$
where:
- ($\mu$) is the mean of the random variable \( X \),
- ($\sigma$) is the standard deviation of \( X \),
- ($k$) is a positive number greater than 1.

**Key Points:**
- **Generality:** Chebyshev's theorem applies to any probability distribution where the mean and variance are defined.
- **Implication:** The inequality tells us that no matter the shape of the distribution, the proportion of values that fall within ($k$) standard deviations of the mean is at least $( 1 - \frac{1}{k^2})$. For example, at least (75\%) of the values lie within 2 standard deviations of the mean (since ($k=2$) gives $( 1-\frac{1}{4} = 0.75)$).
- **Limitations:** While the theorem provides a lower bound, it does not give exact probabilities, and the bounds can be quite loose, especially for distributions that tightly clustered around the mean.

Chebyshev's Theorem is particularly useful for analysts and statisticians dealing with samples from unknown distributions, as it provides a safe, conservative estimate of the spread of data around the mean.



---
## Discrete Distributions

### Binomial Distribution

The Binomial distribution is a discrete probability distribution that models the number of successes in a fixed number of independent trials, with each trial having two possible outcomes, typically labeled as "success" and "failure".

**Key Points:**
- There are only two possible outcomes for each trial: success (1) and failure (0).
- The trials are independent, meaning the outcome of one trial does not affect the outcomes of other trials.

The probability mass function (PMF) for the Binomial distribution is expressed as:
$$
P(X=x) = C^{n}_{x} \theta^x (1-\theta)^{n-x}
$$
where $\theta$ is the probability of success on a single trial, $x$ is the number of successes, and $n$ is the total number of trials.

**Example:**
Consider flipping a fair coin five times. What is the probability of getting exactly two heads?

The calculation is as follows:
$$
P(X=2) = C^{5}_{2} 0.5^2 (1-0.5)^3 = \frac{5!}{2!3!} \times 0.25 \times 0.125 = 31.25\%
$$


### Geometric Distribution

The Geometric distribution describes the probability of observing the first success on the $x$-th trial in a sequence of Bernoulli trials.

**PMF:**
$$
g(x; \theta) = \theta(1-\theta)^{x-1}
$$
where, $\theta$ is the probability of success on each trial, and $x$ is the trial number of the first success.

**Key Properties:**
- **Mean ($\mu$):** The expected number of trials to get the first success is given by:
  $$
  \mu = \frac{1}{\theta}
  $$
- **Variance ($\sigma^2$):** The variance of the number of trials to get the first success is:
  $$
  \sigma^2 = \frac{1-\theta}{\theta^2}
  $$

**Interpretation:**
- The mean and variance provide insights into the "spread" or variability of trials needed to achieve the first success, with higher values of $\theta$ leading to fewer expected trials.

This distribution is commonly used in *quality control*, *reliability testing*, and other areas where the "time" or number of trials until the first success is of interest.


### Poisson Distribution 

The Poisson distribution is a discrete probability distribution that expresses the probability of a given number of events occurring within a fixed interval of time or space. It assumes these events occur with a known constant mean rate and independently of the time since the last event.

A practical example is photometry using a Charge-Coupled Device (CCD), where light—specifically, the number of photons—hits the CCD at a constant rate. Importantly, the arrival of photons is assumed to be independent of previous arrivals, provided the CCD is not saturated.

> **Note:** Independence of events holds only if the CCD is not saturated.

**Assumptions:**
1. The rate of event occurrence, $\lambda$, is constant over time. For example, the number of events occurring between $t$ and $t + \Delta t$ is $\lambda \Delta t$.
2. The probability of an event in the interval $\{t, t+\Delta t\}$ is independent of previous events.

The probability mass function (PMF) of the Poisson distribution is defined as:
$$
P(x; \lambda) = \frac{\lambda^x e^{-\lambda}}{x!}
$$
where $\lambda$ is the expected number of events in a given interval, and $x$ is the observed number of events.

For the Poisson distribution, the expected value (mean) is $\mu = \lambda$, and the variance is $\sigma^2 = \lambda$.

#### Poisson Noise (Shot Noise)

Since $\sigma^2 = \lambda$, the standard deviation (Poisson noise) is $\sigma = \sqrt{\lambda}$. In photometry, where $N$ represents the number of photons hitting the CCD, this implies $\sigma = \sqrt{N}$.

Due to the characteristics of the Poisson distribution, the signal-to-noise ratio (SNR) is calculated as follows:
$$
SNR = \frac{\mu}{\sigma} = \frac{\mu}{\sqrt{\mu}} = \sqrt{\mu}
$$
This relationship highlights the inherent noise properties in photon-counting measurements like those in CCD photometry.

---

