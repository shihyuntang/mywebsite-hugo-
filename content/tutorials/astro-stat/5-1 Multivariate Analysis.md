---
title: Multivariate Analysis
linktitle: Multivariate Analysis
toc: true
type: docs
date: "2024-05-02T00:00:00+01:00"
draft: false
menu:
  astro-stat:
    parent: 5 Multivariate Analysis
    weight: 8

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 8
---
<!-- 
## Principle Component Analysis (PCA)

### Procedure

1. Make data matrix $\mathbf{d}$
2. Center data to form matrix $\mathbf{x}$
3. Construct covariance matrix $\mathbf{\Sigma_x}$ from $\mathbf{x}$
4. Find eigenvalues and eigenvectors of $\mathbf{\Sigma_x}$. The eigenvalues is are the variance and the eigenvectors is the PCA components.
5. Plot each data point in PCA space
6. Try to make sense to what each PCA vector physically means.

- **Step 1**
  The matrix $\mathbf{d}$ has it rows as attribute, like the properties of each targets, or people, etc. And in columns are for different targets or people for example. 
  $$
    \mathbf{d} = \begin{bmatrix}
    d_{11} & d_{21} & \cdots & d_{t1} \\\
    d_{12} & d_{22} & \cdots & d_{t2} \\\
    \vdots & \vdots & \ddots & \vdots \\\
    d_{1n} & d_{2n} & \cdots & d_{tn}
    \end{bmatrix}
  $$
- **Setp 2**
   Center data to form matrix $\mathbf{x}$ via 
   $$
    \mathbf{x} = \mathbf{d} - \mathbf{<\beta>}
   $$
   where $\mathbf{<\beta_j>} = \frac{1}{t} \sum_{j=1}^t d_{ji}$. This is basically means that for each attribute (each row) in $\mathbf{d}$, each values in it minus that attribute's mean value. So we have centered data 
  $$
    \mathbf{x} = \begin{bmatrix}
    x_{11} & x_{21} & \cdots & x_{t1} \\\
    x_{12} & x_{22} & \cdots & x_{t2} \\\
    \vdots & \vdots & \ddots & \vdots \\\
    x_{1n} & x_{2n} & \cdots & x_{tn}
    \end{bmatrix}
  $$
- **Setp 3**
  Construct covariance matrix $\mathbf{\Sigma_x}$ from $\mathbf{x}$. We have
  $$
    \frac{1}{t}E( \mathbf{x} \cdot \mathbf{x}^T) = E\begin{bmatrix}
    \frac{x_{11}^2+x_{21}^2+\cdots+x_{t1}^2}{t} & \frac{x_{11}x_{12}+x_{21}x_{22}+\cdots+x_{t1}x_{t2}}{t} & \cdots \\\
    \frac{x_{11}x_{12}+x_{21}x_{22}+\cdots+x_{t1}x_{t2}}{t} & \frac{x_{12}^2+x_{22}^2+\cdots+x_{t2}^2}{t} & \cdots \\\
    \vdots & \vdots & \ddots
    \end{bmatrix}
  $$
  Because $\mathbf{x}$ has been centered, meaning that $E(x_i)^2 = 0$, thus $\sigma_{x_i}^2 = E(x_i^2)$. And also that $\sigma_{x_i,x_j} = E(x_ix_j)$. We have $\frac{1}{t}E( \mathbf{x} \cdot \mathbf{x}^T)$ equals to the covariance matrix $\mathbf{\Sigma_x}$:
  $$
    \frac{1}{t}E( \mathbf{x} \cdot \mathbf{x}^T) = \mathbf{\Sigma_x} = \begin{bmatrix}
    \sigma_{1}^2 & \sigma_{12} & \cdots & \cdots \\\
    \sigma_{12} & \sigma_{2}^2 & \cdots & \cdots \\\
    \vdots & \vdots & \ddots & \vdots \\\
    \cdots & \cdots & \cdots & \sigma_{tn}^2
    \end{bmatrix}
  $$
- **Setp 4**
  Now, want to find a new axis that have a vectors which is at the direction that give is largest variance of the data. This new axis is then the PCA axes, or say the eigenvector of PC1. This new axis, is often made of linear combinations of wights $w_i$ $i = 1->n$ (where $n$ is the number of attributes). These weights will give a maximum $E(y_1^2)$ where 
  $$
    y_{1j} = w_{11}x_{j1} + w_{21}x_{j2} + \cdots + w_{n1}x_{jn}.
  $$
  where $j=1->t$, for data points. Note that $E(y_1)=0$, so $var(y_1)$ maximized. Now set:
  $$
    \vec{w_1} = \begin{bmatrix}
    w_{11}  \\\
    w_{21}  \\\
    \vdots  \\\
    w_{n1} 
    \end{bmatrix}
  $$ 
  and 
  $$
    \vec{w_1}^T = \begin{bmatrix}
    w_{11}  & w_{21} & \cdots & w_{n1} 
    \end{bmatrix}
  $$ 
  we get
  $$
    \vec{y_1}^T = \vec{w_1}^T \cdot \mathbf{x}
  $$
  Therefore, we get
  $$
    E(y_1^2) = \frac{1}{t}E(\vec{y_1}^T \cdot \vec{y_1}) 
              = \frac{1}{t}E(\vec{w_1}^T \cdot \mathbf{x} \cdot \mathbf{x}^T \cdot \vec{w_1} ) 
              = \vec{w_1}^T E\left( \frac{\mathbf{x} \cdot \mathbf{x}^T }{t} \right)  \vec{w_1}
              = \vec{w_1}^T \mathbf{\Sigma_x}  \vec{w_1}
  $$
  Then we just need to maximize $\vec{w_1}^T \mathbf{\Sigma_x}  \vec{w_1}$ with the constrain of $\vec{w_1}^T \cdot \vec{w_1} = 1$. This involves Lagrange multipliers which I will skip here (for now...). In the end one will get 
  $$
    (\Sigma_x - \lambda_1 I) \vec{w_1} = 0
  $$
  So, $w_1$ is an eigenvector of $\Sigma_x$, and that $\lambda_1$ is the eigenvalue. Want to maximize $\vec{w_1}^T \mathbf{\Sigma_x} \vec{w_1} = \vec{w_1}^T \lambda_1 \vec{w_1} = \lambda_1$. The first PCA component, PC1, is the one with the largest $\lambda$.

--- -->

## Principal Component Analysis (PCA)

### Procedure

PCA is a statistical technique used to emphasize variation and bring out strong patterns in a dataset. It's especially powerful when dealing with high-dimensional data. Here's how it works:

- **Step 1: Create the Data Matrix**:
  Construct matrix $\mathbf{d}$ where each row represents an attribute (like properties of each target or person), and each column corresponds to different subjects or observations (e.g., targets or person).
  $$
    \mathbf{d} = \begin{bmatrix}
    d_{11} & d_{21} & \cdots & d_{t1} \\\
    d_{12} & d_{22} & \cdots & d_{t2} \\\
    \vdots & \vdots & \ddots & \vdots \\\
    d_{1n} & d_{2n} & \cdots & d_{tn}
    \end{bmatrix}
  $$

- **Step 2: Center the Data**:
  Subtract the mean of each attribute from the corresponding values to center the data around the origin. This helps in aligning the PCA with the directions of maximum variance.
  $$
    \mathbf{x} = \mathbf{d} - \mathbf{\langle\beta\rangle}
  $$
  where $\mathbf{\langle\beta_j\rangle} = \frac{1}{t} \sum_{j=1}^t d_{ji}$ represents the mean of each attribute across all data points. The centered data matrix $\mathbf{x}$ looks like this:
  $$
    \mathbf{x} = \begin{bmatrix}
    x_{11} & x_{21} & \cdots & x_{t1} \\\
    x_{12} & x_{22} & \cdots & x_{t2} \\\
    \vdots & \vdots & \ddots & \vdots \\\
    x_{1n} & x_{2n} & \cdots & x_{tn}
    \end{bmatrix}
  $$

- **Step 3: Construct the Covariance Matrix**:
  The covariance matrix $\mathbf{\Sigma_x}$ is constructed from $\mathbf{x}$. Since $\mathbf{x}$ is centered, its expected value matrix $\mathbf{E(x)}$ is zero. The covariance matrix is then:
  
  $$
    \mathbf{\Sigma_x} = \frac{1}{t} \mathbf{x} \mathbf{x}^T
  $$

  This matrix captures the variance shared between the attributes, and its diagonal elements represent the variance of each attribute.

- **Step 4: Eigenvalue Decomposition**:
  Eigenvalues and eigenvectors of the covariance matrix $\mathbf{\Sigma_x}$ are computed. The eigenvectors represent the directions of maximum variance (principal components), and the eigenvalues represent the magnitude of the variance along each principal component.
  
  To find the principal components:
  
  1. Maximize $\vec{w}^T \mathbf{\Sigma_x} \vec{w}$ subject to $\vec{w}^T \vec{w} = 1$.
  2. This leads to solving $(\mathbf{\Sigma_x} - \lambda I) \vec{w} = 0$, where $\lambda$ is the eigenvalue.
  
  The principal component associated with the largest eigenvalue ($\lambda_1$) captures the most variance.

- **Step 5: Transform Data to PCA Space**
  Each data point is then projected onto the PCA space using the eigenvectors, effectively reducing dimensionality while retaining the most significant variance features.

- **Step 6: Interpretation**
  Interpret the physical meaning of each principal component, which might involve understanding how original attributes combine to form the component.


---
## Independent Component Analysis (ICA)

Independent Component Analysis (ICA) is a computational method for separating a multivariate signal into additive subcomponents that are maximally independent. This technique is particularly useful in the field of blind source separation, where the goal is to separate a mixture of signals (like audio tracks) into their individual, independent components without prior knowledge about the source signals.

### Understanding the Context

In applications like audio processing, ICA can be used to separate different speaking voices from a single audio track recorded with multiple voices overlapping. Each recording may capture the same set of voices but with varying amplitudes depending on the distance and orientation of each voice relative to the microphone. Unlike Principal Component Analysis (PCA), which seeks directions of maximum variance and might mix sources further, ICA focuses on maximizing statistical independence between the components. This characteristic makes ICA suitable for tasks where the *underlying sources are non-Gaussian and independent.*

### Procedure for Applying ICA

1. **Preprocessing with PCA**: 
   - **Dimensionality Reduction**: Initially, PCA is applied to reduce the dimensionality of the data. This step is crucial because it removes noise and reduces the complexity of the data, which simplifies the subsequent ICA.
   - **Whitening**: The data is transformed into components that are uncorrelated and have unit variance. This transformation, often performed as part of PCA, is also known as "whitening". It ensures that the ICA algorithm focuses only on finding the independent sources without being misled by possible correlations in the data.
2. **Applying ICA**:
   - **Identify Independent Components (ICs)**: After whitening, the ICA algorithm seeks to rotate the whitened data to a new coordinate system where the statistical independence of the resulting signals is maximized. This involves optimizing an objective function that measures non-Gaussianity (since independence implies non-Gaussianity under certain conditions, see below section on Non-Gaussianity).
   - **Extraction of Sources**: The independent components correspond to the original signals/sources that were mixed in the observed data. Each component should represent one source, such as a single voice in the context of audio processing.

### Example Application

For instance, if you have a recording from a busy restaurant, ICA can help isolate single voices from the background noise and other voices. This technique is invaluable in environments where multiple sources overlap significantly but retain their independence in terms of their statistical signatures.

---
## Understanding Independence, Non-Gaussianity, and the Central Limit Theorem

The Central Limit Theorem (CLT) states that the sum of a large number of independent random variables, each with finite mean and variance, tends toward a Gaussian distribution, regardless of the original distributions of the variables. This principle is critical in the context of Independent Component Analysis (ICA), which is used to separate mixed signals into their original, independent components.

### Implications for ICA

- **Role of the CLT**: The CLT implies that a mixture of multiple independent, non-Gaussian signals tends to be *more Gaussian-like* than any of the individual signals. ICA utilizes this property by assuming that the original sources are non-Gaussian. The mixed signal, being more Gaussian, provides a clue that separation is possible by identifying and maximizing the non-Gaussian aspects of its components.
- **Non-Gaussianity as a Tool**: ICA algorithms focus on maximizing non-Gaussianity to separate the independent components. This is because non-Gaussian signals, when summed, lose some of their distinct statistical features, making the mixture more Gaussian. By finding projections of the data that are maximally non-Gaussian, ICA can effectively identify and separate the original independent sources.
- **Challenge with Gaussian Sources**: If the original sources were Gaussian, their sum would also be Gaussian, offering no statistical advantage for separation. This is why ICA is particularly powerful for non-Gaussian data sources, where it can exploit statistical differences to distinguish between the sources.

### Practical Considerations

ICA is particularly effective in scenarios where the underlying sources of a signal are known to be non-Gaussian, such as in audio signal processing or in biomedical signal analysis. The ability to reverse the effects of the CLT and uncover the original signals from a complex mixture is what makes ICA a valuable tool in modern data analysis.
