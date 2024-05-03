---
title: Timeseries Analysis
linktitle: Timeseries Analysis
toc: true
type: docs
date: "2024-05-03T00:00:00+01:00"
draft: false
menu:
  astro-stat:
    parent: 8 Timeseries Analysis
    weight: 11

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 11
---

## Evenly Spaced Time Series Data

### Autocorrelation Function (ACF)

The Autocorrelation Function (ACF) measures the correlation between a time series and a lagged version of itself over various time intervals. It's akin to performing a Pearson correlation test between the original time series data and the same data shifted by a lag time $k$. Notably, ACF(k=0) always equals 1, reflecting perfect self-correlation at zero lag.

### Partial Autocorrelation Function (PACF)

The Partial Autocorrelation Function (PACF) quantifies the correlation between observations in a time series separated by $k$ time units, specifically adjusting for the correlations at shorter lags. This adjustment helps isolate the direct influence of past data points on the current observation:
- At lag 1, PACF equals ACF as there are no previous terms to adjust for.
- At lag 2, PACF assesses the correlation between points two units apart (e.g., $X_i$ - $X_{i+2}$), adjusting for the influence of the intervening lag (e.g., corelation between $X_i$ - $X_{i+1}$ and $X_{i+1}$ - $X_{i+2}$).

PACF is crucial for model building, especially in autoregressive models, as it helps identify the effective number of past observations (lags) that significantly influence future values.

### Autoregressive (AR) Model

In an AR model, each point in the series is modeled as a linear combination of its previous values:
$$
X_t = \alpha_1 X_{t-1} + \alpha_2 X_{t-2} + \cdots + \alpha_p X_{t-p} + \varepsilon_t
$$
where $\alpha_i$ are coefficients to be estimated and $\varepsilon_t$ is white noise.

### Moving Average (MA) Model

An MA model expresses each point in the series as a linear combination of past noise terms:
$$
X_t = \varepsilon_t + \beta_1 \varepsilon_{t-1} + \beta_2 \varepsilon_{t-2} + \cdots + \beta_q \varepsilon_{t-q}
$$
where $\varepsilon_t = N(0, \sigma^2)$ and $\beta_i$ are coefficients to be estimated.

### Autoregressive Moving Average (ARMA) Model

The ARMA $(p,q)$ model effectively combines autoregressive (AR) and moving average (MA) components:
$$
X_t = \alpha_1 X_{t-1} + \cdots + \alpha_p X_{t-p} + \varepsilon_t + \beta_1 \varepsilon_{t-1} + \cdots + \beta_q \varepsilon_{t-q}
$$
In this model, the parameters $p$ and $q$ denote the orders of the AR and MA components, respectively. These parameters are crucial as they determine the "memory" length of the model, indicating how far back in time the data's dependencies and shocks influence the current observation.

### Autoregressive Integrated Moving Average (ARIMA) Model

Building on the ARMA model, the ARIMA $(p,d,q)$ model incorporates an additional differencing component to render non-stationary time series data stationary. This adjustment is necessary for dealing with underlying trends or seasonality:
<!-- $$
\text{Differenced Series: } Y_t = (1 - B)^d X_t
$$
$$
Y_t = \alpha_1 Y_{t-1} + \cdots + \alpha_p Y_{t-p} + \varepsilon_t + \beta_1 \varepsilon_{t-1} + \cdots + \beta_q \varepsilon_{t-q}
$$ -->
In ARIMA, $d$ represents the degree of differencing required to flatten trends in the data, addressing long-term drift and ensuring stationarity. The parameters $p$ and $q$ continue to represent the AR and MA orders, respectively. ARIMA models are extensively used not only in modeling but also in forecasting scenarios, such as predicting financial market trends or stock prices.


### Fourier Power Spectrum

Fourier analysis converts time series data into the frequency domain, providing insights into periodicity and cyclic patterns within the series.

## Unevenly Spaced Time Series Data

### Lomb-Scargle Periodogram (LSP)

The LSP method extends Fourier analysis to unevenly spaced time series data, facilitating the detection of periodic signals. It also has another form that use leat-squares regression of the dataset to sine and cosine waves in a range of frequencies. A common form is:
$$
  P_{LS}(\nu) = \frac{1}{2\sigma^2} \left[ \frac{\left(\sum_{i=1}^n X_i \cos(2\pi \nu t_i)\right)^2}{\sum_{i=1}^n \cos^2(2\pi \nu (t_i - \tau(\nu)))} + \frac{\left(\sum_{i=1}^n X_i \sin(2\pi \nu t_i)\right)^2}{\sum_{i=1}^n \sin^2(2\pi \nu (t_i - \tau(\nu)))} \right]
$$
where $\tau$ is defined as
$$
  \tan(4\pi \nu \tau) = \frac{\sum_{i=1}^n \sin(4\pi \nu t_i)}{\sum_{i=1}^n \cos(4\pi \nu t_i)}
$$


## Other Analysis Techniques

### Wavelet Analysis

Fourier Transform (FT) is a powerful tool for analyzing frequency components within a time series. However, a key limitation of a single FT is its lack of temporal resolution: it provides frequency information ($\nu$) but no insight into when these frequencies occur, especially if the data is non-stationary—meaning the frequency content changes over time.

#### Problem with Standard Fourier Transform

For instance, if a time series exhibits seasonal variations, the frequency of these variations might change over different time intervals. A simple FT would average these changes across the entire dataset, potentially obscuring meaningful patterns.

#### Solution via Wavelet Analysis

Wavelet analysis addresses this limitation by allowing the examination of different frequencies at different times. This is achieved by dividing the time series into segments and analyzing each segment separately—a process that optimizes the extraction of temporal information at various frequencies.

#### Visualizing Wavelet Transforms

A wavelet plot typically displays frequency space ($\nu$) versus time ($t$). It offers a detailed view where, at shorter periods on the y-axis, there is higher time resolution, and conversely, longer periods offer broader frequency insights but lower time specificity. The parabolic shapes in the plot, often shaded, mark the boundary edge effects, indicating where data becomes less reliable due to edge artifacts.

![Wavelet Transform Analysis Example](https://www.researchgate.net/profile/Victor-Manuel-Velasco-Herrera/publication/261322980/figure/fig2/AS:296841208975361@1447783867682/Wavelet-transform-analysis-of-the-newly-proposed-solar-activity-proxy-nitrate.png)
(Credit: [ResearchGate](https://www.researchgate.net/figure/Wavelet-transform-analysis-of-the-newly-proposed-solar-activity-proxy-nitrate_fig2_261322980))

#### Wavelets Versus Fourier Transforms

Instead of using Fourier transforms, wavelet analysis involves convoluting the time-sliced data with a wavelet function. This method is more effective because it adjusts to the localized variations in the time series through the use of variable-sized 'windows'—smaller windows for higher frequencies and larger ones for lower frequencies.

#### Common Wavelets

Commonly used wavelet functions include the Morlet and Daubechies wavelets, each with specific characteristics that make them suitable for different types of data analysis tasks.

![Types of Mother Wavelet Functions](https://www.researchgate.net/profile/Steven-Vandeput/publication/267403305/figure/fig15/AS:654064610197505@1532952563244/Illustration-of-several-types-of-mother-wavelet-functions-Morlet-wavelet-top-left.png)
(Credit: [ResearchGate](https://www.researchgate.net/figure/Illustration-of-several-types-of-mother-wavelet-functions-Morlet-wavelet-top-left_fig15_267403305))

#### Mathematical Expression

The mathematical expression for a wavelet transform is given by:
$$
W[f(\lambda,t)] = \int_{-\infty}^{\infty} f(\nu) \frac{1}{\sqrt{\lambda}} \overline{\phi}\left(\frac{u-t}{\lambda}\right) du
$$
where $\lambda$ is the scaling factor that stretches or compresses the wavelet, adapting it to the signal's local characteristics.

Wavelet analysis thus provides a more flexible and nuanced approach to understanding time series data, especially when the signal contains non-stationary or frequency-varying components.


### Nyquist Frequency

The Nyquist frequency $\nu_N = 1/(2 \Delta t)$ is the maximum frequency that can be effectively captured by the data, where $\Delta t$ is the sampling interval. It represents the boundary beyond which the sampling rate is insufficient to capture detailed variations in the data.

