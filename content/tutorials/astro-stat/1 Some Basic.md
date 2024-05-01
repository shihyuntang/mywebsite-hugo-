---
title: Probability Basic
linktitle: Probability Basic
toc: true
type: docs
date: "2024-04-29T00:00:00+01:00"
draft: false
menu:
  astro-stat:
    parent: 1 Probability
    weight: 1

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 1
---

## Some Terminology in Statistics

- **i.i.d. (Independent and Identically Distributed):**
  - **Definition:** This term refers to a set of random variables that are all independent of each other and share the same probability distribution. The assumption of i.i.d. is crucial in many statistical methods because it simplifies the mathematical analysis and inference processes.

- **Null Hypothesis:**
  - **Definition:** In hypothesis testing, the null hypothesis is a general statement or default position that there is no relationship between two measured phenomena or no association among groups tested.
  - 
- **P-value:**
  - **Definition:** The p-value is the probability of observing test results at least as extreme as the results actually observed, under the assumption that the null hypothesis is correct. A p-value less than a pre-determined significance level, often 0.05, leads to the rejection of the null hypothesis.
  
- **Confidence Interval (CI):**
  - **Definition:** A confidence interval is a range of values, derived from sample statistics, that is likely to contain the value of an unknown population parameter. The confidence level represents the probability that this interval will capture this parameter in repeated samples.
  
- **Type I and Type II Errors:**
  - **Type I Error (False Positive):** Occurs when the null hypothesis is incorrectly rejected when it is actually true.
  - **Type II Error (False Negative):** Occurs when the null hypothesis is not rejected when it is actually false.


---

## First and Second Moments

In probability and statistics, the concepts of first and second moments are central to understanding the distributions of random variables:

- **First Moment (Mean):**
  - **Definition:** The first moment is the expected value of a random variable $X$, denoted as $E(X)$.
  - **Formula:** 
    $$E(X) = \mu$$

- **Second Moment (Variance):**
  - **Definition:** The second moment about the mean is the variance of the random variable $X$, denoted as $\sigma^2$. It measures the spread of the data points around the mean.
  - **Formula:** The variance is calculated using the expectation of the *squared deviations from the mean*:
    $$
    \sigma^2 = E[(X-\mu)^2] = E[X^2] - E(X)^2
    $$
  > $$\begin{align}
      \sigma^2 &= E[(X-\mu)^2] \\\
              &= E[X^2 - 2X\mu + \mu^2] \\\
              &= E[X^2] - 2\mu E(X) + E(\mu^2) \\\
              &= E[X^2] - 2\mu^2 + \mu^2 \\\
              &= E[X^2] - \mu^2 \\\
              &= E[X^2] - E(X)^2
  \end{align}$$

- **Third Moment (Skewness):**
  - **Definition:** The third central moment describes the skewness of the distribution of a random variable, indicating the degree of asymmetry around the mean. Skewness can reveal whether the distribution tails off more on one side than the other.
  - **Formula:** The third moment is calculated using the expectation of the cubed deviations from the mean:
    $$
    E[(X - E(X))^3]
    $$
  - **Interpretation:** A positive skewness indicates that the distribution has a long tail to the right (more positive side), while a negative skewness indicates a long tail to the left (more negative side).

- **Covariance:**
  - **Definition:** Covariance measures the joint variability of two random variables, $X$ and $Y$. It assesses the degree to which two variables change together. If the greater values of one variable mainly correspond to the greater values of the other variable, and the same holds for the lesser values, the covariance is positive.
  - **Formula:** The covariance between two variables $X$ and $Y$ is given by:
    $$
    \text{Cov}(X, Y) = E[(X - E(X))(Y - E(Y))]
    $$
  - **Interpretation:** A positive covariance indicates that as $X$ increases, $Y$ tends to increase. A negative covariance suggests that as $X$ increases, $Y$ tends to decrease. Zero covariance indicates that the variables are independent, assuming they are also uncorrelated.


### Standardization

Transforming the random variable to with zero mean and unit variance. This tranasformation also removes the unit on the random variable.

$$
X_{std} = \frac{X - \mu}{\sigma}
$$

## z test vs. t test 
