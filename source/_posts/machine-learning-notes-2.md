---
title: Machine Learning Study Notes 2
mathjax: true
date: 2018-08-12 10:24:08
tags:
- 学习笔记
- tech
- Machine Learning
---

## 1. Environment Setup Instructions
### 1.1. Environment Setup Instructions
<!-- more -->

(Install Octave and use Matlab online version)

### 1.2. Multivariate Linear Regression
#### 1.2.1. Multiple Features

Linear regression with multiple variables is also known as "multivariate linear regression".

We now introduce notation for equations where we can have any number of input variables.

- $x_{j}^{i}$ = value of feature j in the $i^{th}$ training example
- $x^{i}$ = the input (features) of the $i^{th}$ training example
- m = the number of training examples
- n = the number of features

The multivariable form of the hypothesis function accommodating these multiple features is as follows:

$$h_{\theta}(x) = \theta_{0} + \theta_{1}x_{1} + \theta_{2}x_{2} + \theta_{3}x_{3} + ... + \theta_{n}x_{n}$$

In order to develop intuition about this function, we can think about $\theta_{0}$ as the basic price of a house, $\theta_{1}$ as the price per square meter, $\theta_{2}$ as the price per floor, etc. $x_{1}$ will be the number of square meters in the house, $x_{2}$ the number of floors, etc.

Using the definition of matrix multiplication, our multivariable hypothesis function can be concisely represented as:

$$h_{\theta}(x) = \begin{bmatrix}\theta_{0}&\theta_{1}&...&\theta_{n}\end{bmatrix}\begin{bmatrix}x_{0}\\x_{1}\\.\\.\\.\\x_{n}\end{bmatrix} = \theta^{T}x$$

This is a vectorization of our hypothesis function for one training example; see the lessons on vectorization to learn more.

Remark: Note that for convenience reasons in this course we assume $x_{0}^{i} = 1$ for $i∈1, ..., m)$. This allows us to do matrix operations with theta and x. Hence making the two vectors '$\theta$' and $x^{(i)}$ match each other element-wise (that is, have the same number of elements: n+1).]

#### 1.2.2. Gradient Descent For Multiple Variables

**Gradient Descent for Multiple Variables**

The gradient descent equation itself is generally the same form; we just have to repeat it for our 'n' features:
repeat until convergence: {
$$\theta_{0} := \theta_{0} - \alpha\frac{1}{m}\sum_{i=1}^{m}(h_{\theta}(x^{(i)}) - y^{(i)})*x_{0}^{(i)}$$
$$\theta_{1} := \theta_{1} - \alpha\frac{1}{m}\sum_{i=1}^{m}(h_{\theta}(x^{(i)}) - y^{(i)})*x_{1}^{(i)}$$
$$\theta_{2} := \theta_{2} - \alpha\frac{1}{m}\sum_{i=1}^{m}(h_{\theta}(x^{(i)}) - y^{(i)})*x_{2}^{(i)}$$
$$...$$

}

In other words, repeat until convergence: {
$$\theta_{j} := \theta_{j} - \alpha\frac{1}{m}\sum_{i=1}^{m}(h_{\theta}(x^{(i)}) - y^{(i)})*x_{j}^{(i)},    for j:= 0,...,m$$
$$...$$
}

The following image compares gradient descent with one variable to gradient descent with multiple variables:
![](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/MYm8uqafEeaZoQ7hPZtKqg_c974c2e2953662e9578b38c7b04591ed_Screenshot-2016-11-09-09.07.04.png?expiry=1534118400000&hmac=f1cD9W8Ddb6AwlqYpQ5kCSJS9hsgrjioIW0RMNRkfcU)

#### 1.2.3. Gradient Descent in Practice I - Feature Scaling

We can speed up gradient descent by having each of our input values in roughly the same range. This is because θ will descend quickly on small ranges and slowly on large ranges, and so will oscillate inefficiently down to the optimum when the variables are very uneven.

The way to prevent this is to modify the ranges of our input variables so that they are all roughly the same. Ideally:

$-1<= X_{i} <= 1$

or

$-0.5<= X_{i} <= 0.5$

These aren't exact requirements; we are only trying to speed things up. The goal is to get all input variables into roughly one of these ranges, give or take a few.

Two techniques to help with this are **feature scaling** and **mean normalization**. Feature scaling involves dividing the input values by the range (i.e. the maximum value minus the minimum value) of the input variable, resulting in a new range of just 1. Mean normalization involves subtracting the average value for an input variable from the values for that input variable resulting in a new average value for the input variable of just zero. To implement both of these techniques, adjust your input values as shown in this formula:

$x_{i} := \frac{x_{i} - u_{i}}{s_{i}}$

Where $u_{i}$ is the **average** of all the values for feature (i) and $s_{i}$ is the range of values (max - min), or $s_{i}$ is the standard deviation.

For example, if $x_{i}$ represents housing prices with a range of 100 to 2000 and a mean value of 1000, then, $x_{i} := \frac{price - 1000}{1900}$.

#### 1.2.4. Gradient Descent in Practice II - Learning Rate

**Debugging gradient descent.** Make a plot with number of iterations on the x-axis. Now plot the cost function, J(θ) over the number of iterations of gradient descent. If J(θ) ever increases, then you probably need to decrease α.

**Automatic convergence test.** Declare convergence if J(θ) decreases by less than E in one iteration, where E is some small value such as 10−3. However in practice it's difficult to choose this threshold value.

![](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/FEfS3aajEea3qApInhZCFg_6be025f7ad145eb0974b244a7f5b3f59_Screenshot-2016-11-09-09.35.59.png?expiry=1534118400000&hmac=GqzeNeVN2C8hclqEIiTAXhx_JyT1_lvzYhnhg-j65Fo)

It has been proven that if learning rate α is sufficiently small, then J(θ) will decrease on every iteration.

![](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/rC2jGKgvEeamBAoLccicqA_ec9e40a58588382f5b6df60637b69470_Screenshot-2016-11-11-08.55.21.png?expiry=1534118400000&hmac=fBMhv7ZZB2PqC29TfdoC09YcDAW2qsvU_e5kUd8nAvI)

To summarize:

If $\alpha$ is too small: slow convergence.

If $\alpha$ is too large: ￼may not decrease on every iteration and thus may not converge.

#### 1.2.5. Features and Polynomial Regression

We can improve our features and the form of our hypothesis function in a couple different ways.

We can combine multiple features into one. For example, we can combine $x_{1}$ and $x_{2}$ into a new feature $x_{3}$ by taking $x_{1} * x_{2}$.

**Polynomial Regression**

Our hypothesis function need not be linear (a straight line) if that does not fit the data well.

We can **change the behavior or curve** of our hypothesis function by making it a quadratic, cubic or square root function (or any other form).

For example, if our hypothesis function is $h_{\theta}(x) = \theta_{0} + \theta_{1}x_{1}$ then we can create additional features based on $x_{1}$, to get the quadratic function $h_{\theta}(x) = \theta_{0} + \theta_{1}x_{1} + \theta_{2}x_{1}^{2}$ or the cubic function $h_{\theta}(x) = \theta_{0} + \theta_{1}x_{1} + \theta_{2}x_{1}^{2} + \theta_{3}x_{1}^{3}$
​	 
In the cubic version, we have created new features $x_{2}$ and $x_{3}$ where $x_{2} = x_{1}^{2}$ and $x_{3} = x_{1}^{3}$.

To make it a square root function, we could do: $h_{\theta}(x) = \theta_{0} + \theta_{1}x_{1} + \theta_{2}\sqrt{x_{1}}$

One important thing to keep in mind is, if you choose your features this way then feature scaling becomes very important.

eg. if $x_{1}$ has range 1 - 1000 then range of $x_{1}^{2}$ becomes 1 - 1000000 and that of $x_{1}^{3}$ becomes 1 - 1000000000

### 1.3. Computing Parameters Analytically

#### 1.3.1. Normal Equation

Gradient descent gives one way of minimizing J. Let’s discuss a second way of doing so, this time performing the minimization explicitly and without resorting to an iterative algorithm. In the "Normal Equation" method, we will minimize J by explicitly taking its derivatives with respect to the θj ’s, and setting them to zero. This allows us to find the optimum theta without iteration. The normal equation formula is given below:

$$\theta = (X^{T}X)^{-1}X^{T}y$$

![](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/dykma6dwEea3qApInhZCFg_333df5f11086fee19c4fb81bc34d5125_Screenshot-2016-11-10-10.06.16.png?expiry=1534204800000&hmac=okHO2ta10q-9e0Q-Nv-fFU5ukQF-pI1d_5w2AognaXg)

There is **no need** to do feature scaling with the normal equation.

The following is a comparison of gradient descent and the normal equation:

| Gradient Descent        | Normal Equation           |
|:------------ |:------------|
| Need to choose alpha      | No need to choose alpha |
| Needs many iterations      | No need to iterate      |
| $O(kn^{2})$ | $O(n^{3})$, need to calculate inverse of $X^{T}X$     |

With the normal equation, computing the inversion has complexity $O(n^{3})$. So if we have a very large number of features, the normal equation will be slow. In practice, when n exceeds 10,000 it might be a good time to go from a normal solution to an iterative process.

#### 1.3.2. Normal Equation Noninvertibility

When implementing the normal equation in octave we want to use the 'pinv' function rather than 'inv.' The 'pinv' function will give you a value of θ even if $X^{T}X$ is not invertible.

If $X^{T}X$ is **noninvertible**, the common causes might be having :

- Redundant features, where two features are very closely related (i.e. they are linearly dependent)
- Too many features (e.g. m ≤ n). In this case, delete some features or use "regularization" (to be explained in a later lesson).

Solutions to the above problems include deleting a feature that is linearly dependent with another or deleting one or more features when there are too many features.

(To Be Continued...)
