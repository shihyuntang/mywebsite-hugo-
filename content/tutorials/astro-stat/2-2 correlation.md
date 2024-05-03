---
title: Correlation
linktitle: Correlation
toc: true
type: docs
date: "2024-05-1T00:00:00+01:00"
draft: false
menu:
  astro-stat:
    parent: 2 Nonparametric
    weight: 6

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 5
---

Nonparametric correlation tests are essential tools for assessing the strength and direction of a relationship between two datasets, especially when the underlying distributions are unknown or non-normal. These tests are robust alternatives to the Pearson correlation coefficient, suitable for various types of relationships. The null hypothesis for these tests is that there is no correlation between the datasets.

### *Pearson Correlation Coefficient

> Pearson correlation test is a **parametric test**, but I put it here for completeness and for comparison.

The Pearson correlation coefficient measures the linear relationship between two continuous variables. It is a parametric test and assumes that the data is normally distributed. The coefficient varies between -1 and +1, where +1 indicates a perfect positive linear relationship, -1 indicates a perfect negative linear relationship, and 0 indicates no linear relationship.

### Spearman's Rank Correlation Coefficient ($\rho$)

Spearman's correlation assesses how well the relationship between two variables can be described using a monotonic function. It does not require the data to be normally distributed, as it uses the rank of the data rather than the actual values.

**Statistic:**
$$
  \rho = 1 - \frac{6 \sum d_i^2 + T}{n(n^2 - 1)}
$$
where $d_i$ is the difference between the ranks of corresponding variables and $n$ is the number of observations. For handling ties, the correction term $T$ is applied:
$$
  T = \sum t_x \left[ \frac{x^3 - x}{12} \right]
$$
where $t_x$ is the number of ties involving $x$ elements. To further estimate the $p$-value, the $z$ score can be calculated by:
$$
  z = \sqrt{n-1} \rho
$$
which approximates a normal distribution under the null hypothesis. One can use the $\rho$ statistic and compare to the critical values [here](https://www.york.ac.uk/depts/maths/tables/spearman.pdf).

### Kendall's Tau ($\tau$)

Kendall's Tau measures the ordinal association between two variables by considering the number of concordant and discordant pairs. It is less sensitive to outliers than Pearson and can be more interpretable in terms of the proportion of concordant pairs.

**Statistic:**
$$
\tau = \frac{N_c - N_d}{\sqrt{(N_c + N_d + T)(N_c + N_d + U)}}
$$
where $N_c$ is the number of concordant pairs, $N_d$ is the number of discordant pairs, $T$ is the number of ties on one variable, and $U$ is the number of ties on the other variable. 

The critical values for $\tau$ can be find [here](https://www.york.ac.uk/depts/maths/tables/kendall.pdf).


### Comparison of Correlation Tests

| **Test**           | **Best Use Case**                           | **Sensitivity**                                 | **Data Requirements**          |
|--------------------|---------------------------------------------|-------------------------------------------------|--------------------------------|
| **Pearson**        | Linear relationships                        | Highly sensitive to linear trends               | Normal distribution, continuous data |
| **Spearman's rho** | Monotonic relationships, not necessarily linear | Sensitive to monotonic trends, not affected by outliers | Ordinal data or non-normal distributions |
| **Kendall's tau**  | General increasing or decreasing trends, less intensive computation | Less sensitive to errors in data, good for small samples or data with many ties | Ordinal data, robust against outliers |
