---
title: Regression
linktitle: Regression
toc: true
type: docs
date: "2024-05-02T00:00:00+01:00"
draft: false
menu:
  astro-stat:
    parent: 4 Regression
    weight: 7

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 7
---


Regression analysis is fundamental in statistical modeling, used for predicting and forecasting, and understanding relationships between variables. Below are various regression methods:

### Least-Square Linear Regression (without Uncertainty)

- **Ordinary Least Squares (OLS)**: This method minimizes the residual sum of squares (RSS) between the observed values in the dataset and the values predicted by the linear model.
  $$
    \text{min RSS} = \text{min} \sum_{i=1}^n (Y_i - \beta_0 - \beta_1 X_i)^2
  $$
  where $X_i$ and $Y_i$ are the observed values, and $\beta_0$ and $\beta_1$ are the intercept and slope of the linear model, respectively.

- **Symmetric Least Squares-Orthogonal Regression**: This method minimizes the summed squares of the residuals orthogonal to the regression line, providing a more general approach than OLS when errors in both variables need to be considered.

- **Robust Regression - Thiel-Sen Estimator**: This technique uses the median of the slopes between pairs of points as the estimator, providing robustness against outliers.

- **Quantile Regression**: Focuses on estimating either the conditional median or other quantiles of the response variable, providing a more comprehensive view of the possible outcome distribution than mean regression.

- **Maximum Likelihood Estimation**: Assumes a probability distribution model for the data, often a normal distribution, and finds the parameter values that maximize the likelihood of observing the data.

### Weighted Least Squares (with Uncertainty)

In scenarios with heteroscedastic errors (errors that varies), weighted least squares (WLS) is more appropriate:

$$
  S_{r,wt} = \sum_{i=1}^n \frac{(Y_i - \beta_0 - \beta_1 X_i)^2}{\sigma_{Y,i}^2}
$$
where $\sigma_{Y,i}^2$ is the variance associated with each observation, weighting the residuals accordingly. This is related to the $\chi^2$ statistic used in minimum $\chi^2$ regression:

$$
  \chi^2_{me} = \sum_{i=1}^n (O_i - M_i)^2 / \sigma_{i,me}^2
$$

### Logistic Regression

Logistic regression is used for modeling binary outcome variables by using the logistic function to estimate probabilities that can be transformed into binary values.

---
### Model Validation and Selection

- **Coefficient of Determination (R²)**: Measures the proportion of variability in a dataset that is explained by the regression model.
$$
  R^2 = 1 - \frac{ \sum_{i=1}^n (Y_i - \hat{Y_i})^2 }{ \sum_{i=1}^n (Y_i - \bar{Y})^2 }
$$
where 
  - $\hat{Y_i}$ is the predicted value of the dependent variable for the $i$-th observation from the model
  - $\bar{Y}$ is the mean of the observed data $Y_i$. 

  An $R^2$ value of 1 implies a perfect fit, meaning that the model explains all the variability of the response data around its mean. Conversely, an $R^2$ value of 0 indicates at bad fit.

- **Adjusted $R^2$**: Adjusts $R²$ for the number of predictors in the model, preventing overfitting by penalizing excessive use of parameters.
  $$
  R_a^2 = 1 - \frac{(1-R^2)(n-1)}{n-p-1}
  $$
  where $p$ is the number of parameters, and $n$ is the number of data points.

- **Normal quantile-quantile plot (Q-Q Plot)**: Used to check the normality of residuals. If the points lie along a straight line, the residuals are normally distributed, an assumption in many regression models.

---

- **Akaike Information Criterion (AIC)**: The AIC estimates the relative amount of information lost by a given model: the less information a model loses, the higher the quality of that model.
  $$
    \text{AIC} = 2k - 2\ln(\hat{L})
  $$
  where $k$ is the number of parameters in the model, and $\hat{L}$ is the maximum likelihood value.
  
  The model with the lowest AIC among a set of models is typically chosen. The AIC is particularly useful when a model is being fit to data: minimizing the AIC maximizes the likelihood function given the data while penalizing for increasing numbers of parameters.

- **Bayesian Information Criterion (BIC)**: The BIC is similar to the AIC but introduces *a stronger penalty for including additional variables to the model*. It is derived from Bayesian probability.
  $$
  \text{BIC} = \ln(n)k - 2\ln(\hat{L})
  $$
  where $n$ is the number of observations, $k$ is the number of parameters in the model, and $\hat{L}$ is the maximum likelihood of the model.

  The BIC is generally stricter than the AIC and can be preferable for models with large $n$, penalizing free parameters more heavily. Like the AIC, **the model with the lowest BIC is generally preferred**.

<!-- ## When to Use AIC vs. BIC

| **Criterion** | **When to Use**                                                                                               |
|---------------|---------------------------------------------------------------------------------------------------------------|
| **AIC**       | More appropriate when the focus is on goodness of fit. Suitable for models where the sample size \( n \) is much larger than the number of parameters \( k \). Less strict about adding parameters. |
| **BIC**       | Used when model parsimony is important. Especially useful in models with a large number of observations \( n \) and relatively less concern about capturing every parameter influence. More stringent in penalizing free parameters. | -->

<!-- ## Summary Table for Regression Methods

| **Method**                      | **Best Use**                                           | **Assumptions/Features**                                   |
|---------------------------------|--------------------------------------------------------|------------------------------------------------------------|
| **OLS Regression**              | Linear relationships with constant variance            | Assumes normality and linearity                            |
| **Orthogonal Regression**       | Errors in both variables                               | Minimizes perpendicular distances                          |
| **Robust Regression**           | Outlier-heavy data                                     | Resistant to outliers in data                              |
| **Quantile Regression**         | Non-normal data; interested in other quantiles         | Does not assume a specific distribution for residuals      |
| **Weighted Least Squares**      | Varied error size across data range                    | Weights observations by the inverse of their variance      |
| **Logistic Regression**         | Binary outcome data                                    | Estimates probability of occurrence                        |
 -->
