# Portfolio Optimisation

Here in this project, I would like to shed some light over Portfolio Optimization and the foundations of Mathematical Optimization and Modern portfolio theory (or Mean-Variance Portfolio Theory). Based on the assumption  that returns are normally distributed and by looking at mean and variance, we can essentially describe the distribution of end-of-period wealth.
The basic idea of this theory is to achieve diversification by constructing a portfolio for a minimal portfolio risk or maximal portfolio returns. Accordingly, the Efficient Frontier is a set of optimal portfolios in the risk-return spectrum, and portfolios located under the Efficient Frontier curve are considered sub-optimal.

## Sections:

### 1.  A Quick Overview of Optimization

- The method of Lagrange
- Lagrange for Single Constraint

### 2. Portfolio Optimisation

- The Mean Variance Criterion
- Markowitz Criterion (continued)
- The Lagrangian Portfolio Optimisation
- Monte Carlo Approach

### 3. The Optimisation Class

### 4. Conclusions



## 1. A Quick Overview of Optimization

 An optimization problem is one in which you are trying to find the best possible value that a function, say $f$ , can take subject to a number of constraints. This generally involves finding the minimum or maximum of $f$ or
 of a function built around $f$.
 
Optimization problems can be divided into two categories, depending on whether the variables are continuous or discrete. In this context, we focused only on continuous optimisation. 
 
The standard form of a continuous optimization problem is:
 
${\displaystyle {\begin{aligned}&{\underset {x}{\operatorname {minimize} }}&&f(x)\\&\operatorname {subject\;to} &&g_{i}(x)\leq b_i,\quad i=1,\dots ,p\end{aligned}}}$

where the function f is called the objective function. It is the function we want to optimize (here minimize).  The variables $x_1, ....,x_n$ are the decision variables with respect to which we want to optimize the function. The functions $g_1,..,g_m$ are the m constraints faced in our optimization. These constraints can be equalities or inequalities


In the context of Portfolio Optimisation, the mean-variance optimisation criterion is quite popular. The 


###  The method of Lagrange

The basic idea of the Lagrangian method is to convert a constrained problem into a form such that the derivative test of an unconstrained problem can still be applied. The relationship between the gradient of the function and gradients of the constraints rather naturally leads to a reformulation of the original problem, known as the Lagrangian function or Lagrangian. In the general case, the Lagrangian is defined in the inner product fashion as:

${\displaystyle {\mathcal {L}}(x,\lambda )\equiv f(x)+\langle \lambda ,g(x)\rangle }$

In simple cases, it is defined as the dot product as:

${\displaystyle {\mathcal {L}}(x,\lambda )\equiv f(x)+\lambda \cdot g(x)}$

The method can be summarized as follows: in order to find the maximum or minimum of a function f ${\displaystyle g(x)=0}$, find the stationary points of L ${\displaystyle {\mathcal {L}}}$ considered as a function of  x ${\displaystyle x}$ and the Lagrange multiplier $λ$. This means that all partial derivatives should be zero, including the partial derivative with respect to $λ$, so:

${\displaystyle {\frac {\partial {\mathcal {L}}}{\partial x}}=0}$ 

${\displaystyle {\frac {\ \partial {\mathcal {L}}\ }{\partial \lambda }}=0\ ;}$


${\displaystyle {\frac {\partial f(x)}{\partial x}}+\lambda \cdot {\frac {\partial g(x)}{\partial x}}=0}$



In N-dimenions, the Lagrangian function reads as:


${\displaystyle {\mathcal {L}}\left(x_{1},\ldots ,x_{n},\lambda _{1},\ldots ,\lambda _{M}\right)=f\left(x_{1},\ldots ,x_{n}\right)-\sum \limits _{k=1}^{M}{\lambda _{k}g_{k}\left(x_{1},\ldots ,x_{n}\right)}\ }$


This involves solving:

$
{\displaystyle \nabla _{x_{1},\ldots ,x_{n},\lambda _{1},\ldots ,\lambda _{M}}{\mathcal {L}}(x_{1},\ldots ,x_{n},\lambda _{1},\ldots ,\lambda _{M})=0\iff {\begin{cases}\nabla f(\mathbf {x} )-\sum _{k=1}^{M}{\lambda _{k}\,\nabla g_{k}(\mathbf {x} )}=0\\g_{1}(\mathbf {x} )=\cdots =g_{M}(\mathbf {x} )=0\end{cases}}}$

### Lagrange for Single Constraint


$
\nabla_{x,y,\lambda} \mathcal{L}(x, y, \lambda) = 0 \iff 
\begin{cases} 
\nabla_{x,y} f(x, y) = -\lambda \nabla_{x,y} g(x, y), \\
g(x, y) = 0 
\end{cases}
$

## 2. Portfolio Optimisation

In this section, we will focus on how to efficiently optimize portfolio weights in order to reach better allocation both in a risk-return framework but also with a given return constraint (i.e. a return mandate to achieve over time).

### The Mean Variance Criterion

Let us consider the following,  each asset $i$ is entirely characterized by its expected return $\mu_{i}$ and expected standard deviation $\sigma_{i}$. In addition, assets $i$ and $j$ are correlated with correlation $\rho_{ij}$. The proportion of the portfolio invested in asset i is $w_i$.

The vector of asset expected returns is defined as the following column vector:


$\mu =
\begin{bmatrix}
\mu_1 \\
.\\
. \\
\mu_i \\
 \\
.\\
. \\
\mu_n \\
\end{bmatrix}
$

and the covariance matrix $\Sigma$, which by definition is:

${\displaystyle \operatorname {\Sigma} =\operatorname {cov} [X_{i},X_{j}]=\operatorname {E} [(X_{i}-\operatorname {E} [X_{i}])(X_{j}-\operatorname {E} [X_{j}])]}$



Given our settings, the covariance matrix can be written as:

$
\Sigma =
\begin{bmatrix}
\sigma^2_{1} & \rho_{12}\sigma_1\sigma_2 & \cdots & \rho_{1n}\sigma_1\sigma_n \\
\rho_{21}\sigma_2\sigma_1 & \sigma_2^2 & \cdots &\rho_{2n}\sigma_2\sigma_n \\
\cdots & \cdots & \cdots & \cdots \\
\vdots & \vdots & \vdots & \ddots  \\
\rho_{n1}\sigma_2\sigma_1 & \cdots & \cdots & \sigma^2_n 
\end{bmatrix}
$

Let us consider the correlation matrix:

${\displaystyle \operatorname {corr} (\mathbf {X} )={\begin{bmatrix}1&{\frac {\operatorname {E} [(X_{1}-\mu _{1})(X_{2}-\mu _{2})]}{\sigma (X_{1})\sigma (X_{2})}}&\cdots &{\frac {\operatorname {E} [(X_{1}-\mu _{1})(X_{n}-\mu _{n})]}{\sigma (X_{1})\sigma (X_{n})}}\\\\{\frac {\operatorname {E} [(X_{2}-\mu _{2})(X_{1}-\mu _{1})]}{\sigma (X_{2})\sigma (X_{1})}}&1&\cdots &{\frac {\operatorname {E} [(X_{2}-\mu _{2})(X_{n}-\mu _{n})]}{\sigma (X_{2})\sigma (X_{n})}}\\\\\vdots &\vdots &\ddots &\vdots \\\\{\frac {\operatorname {E} [(X_{n}-\mu _{n})(X_{1}-\mu _{1})]}{\sigma (X_{n})\sigma (X_{1})}}&{\frac {\operatorname {E} [(X_{n}-\mu _{n})(X_{2}-\mu _{2})]}{\sigma (X_{n})\sigma (X_{2})}}&\cdots &1\end{bmatrix}}}$


Then the covariance matrix can also be factorised in the following way, (i.e. $\Sigma = DCD$) where D is a diagonal matrix and C is the correlation matrix $C = corr(X)$:

${\displaystyle \operatorname {\Sigma} ={\begin{bmatrix}\sigma _{1}&&&0\\&\sigma _{2}\\&&\ddots \\0&&&\sigma _{n}\end{bmatrix}}{\begin{bmatrix}1&\rho _{12}&\cdots &\rho _{1n}\\\rho _{21}&1&\cdots &\rho _{2n}\\\vdots &\vdots &\ddots &\vdots \\\rho _{n1}&\rho _{n2}&\cdots &1\\\end{bmatrix}}{\begin{bmatrix}\sigma_{1}&&&0\\&\sigma_{2}\\&&\ddots \\0&&&\sigma_{n}\end{bmatrix}}}$





The weights vector $w$ is given by:


$w =
\begin{bmatrix}
\ w_1 \\
.\\
. \\
\ w_i \\
 \\
.\\
. \\
\ w_n \\
\end{bmatrix}
$

Considering a risk-free asset,  with a certain return r, variance equal to 0 and correlation with the other (risky) assets equal to 0. The weight $w_0$ of the risk-free asset is de ned as the weight of the portfolio that remains once the allocation to risky assets is complete.

Mathematically,
$w_0 = \mathbf{1}  - w_1$ where $\mathbf{1}$ is a vector of 1's.


The return of the portfolio is given by:


### Markowitz Criterion (continued)

The mean-variance optimisation criterion, which was first proposed by Markowitz, corresponds to nding the asset allocation w that maximizes the expected return of the portfolio subject to a penalty related to the variance of portfolio returns:


$
\max_{w} \mu_P - \frac{\lambda}{2} \sigma^2_P 
$

and $\lambda > 0 $ represents the degree of risk aversion.

To solve the optimisation problem, we need to express the previous equation as an explicit function of w. In a market with N risky assets and a risk-free asset, we get:


$\max_{w} V(w) = [r + w(\mu - r\mathbf{1})] - \frac{\lambda}{2}w^T \Sigma w$


The first order condition gives:


$\nabla V(w^*) = \displaystyle{\frac{\partial{V}}{\partial{w}}(w^*) = (\mu - r\mathbf{1}) - \lambda \Sigma w^* = 0 }$

which gives the solution:

$w^* = \frac{1}{\lambda} \Sigma ^-1 (\mu - r\mathbf{1})$

We can confirm that by checking the second order condition that our Hessian matrix is negative, therefore $w^*$ is a maximum (i.e.):

$\mathbf{H} (w^*) = - \lambda \Sigma < 0$



### The Lagrangian Portfolio Optimisation

The portfolio selection problem is generally de ned as a minimization of risk subject to a return constraint. Here it comes the Lagrangian method that we have highlighted above.

The Lagrangian optimisation problem in the context of Portfolio Construction starts with:

$\displaystyle{\min_{w} \frac{1}{2} \sigma_P^2 = \frac{1}{2} w^T \Sigma w}$

We already have one constraint: the portfolio return must be equal to a specified level $m$. In mathematical terms:

- $ \mu_P = \mu ^T w = m$

This combines with the second usual constraint (the sum of weights being equal to 1):

- $ \mathbf{1}^Tw = 1$


To resolve the Lagrangian problem, let us set the Lagrangian function with two Lagrange multipliers $\lambda $ and $\gamma$ as:

$\displaystyle{\mathbf{L}(w, \lambda, \gamma) = \frac{1}{2} w^T \Sigma w + \lambda (m - w^T \mu) + \gamma (1 - w^T \mathbf{1})}$


The first order condition gives:

$\displaystyle{\frac{\partial L}{\partial w}} = \Sigma w - \lambda \mu - \gamma \mathbf{1} = 0 $

Checking the second order condition, the Hessian of the objective function is equal to the covariance matrix $\Sigma$, which is positive definite. Therefore, we have
reached the optimal weight vector $w^*$:

- $ w^* = \Sigma ^{-1} (\lambda \mu + \gamma \mathbf{1} $


Remembering the constraints are:

- $ \mu^T w = m$
- $ \mathbf{1}^T w = 1$

Substituting winto these two equations, we get:

$ \mu^T \Sigma ^{-1} (\lambda \mu + \gamma \mathbf{1}) = \lambda \mu ^T \Sigma ^{-1} \mu + \gamma \mu ^T \Sigma ^{-1} \mathbf{1} = m$

and:

$ \mathbf{1}^T \Sigma ^{-1} (\lambda \mu + \gamma \mathbf{1}) = \lambda \mathbf{1}^T \Sigma ^{-1} \mu + \gamma \mathbf{1}^T \Sigma ^{-1} \mathbf{1} = 1$ 


For convenience, we define the following scalars:

- $ A = \mathbf{1}^T \Sigma ^{-1} \mathbf{1} $

- $ B = \mu ^T \Sigma ^{-1} \mathbf{1}$

- $ C = \mu ^T \Sigma ^{-1} \mu $


Note that $ AC - B^2>0$ and therefore the system of Lagrange multipliers becomes:

- $ C\lambda + B\gamma = m$
- $ B\lambda + A\gamma + 1$

which yields:

- $ \lambda = \frac{Am - B}{AC - B^2} $
- $ \gamma = \frac{C - Bm}{AC - B^2}$


Substituting into the solution for $w^*$, we obtain:

- $ w^* = \frac{1}{AC- B^2} \Sigma ^{-1} [(A\mu - B\mathbf{1})m + (C\mathbf{1} - B\mu)]$


We will utilise the Lagrangian method to obtain the optimal weight vector for our portfolio.

### Monte Carlo Approach


In a Monte Carlo context, we generate N 0-1 distributed pseudo-random numbers using $random.random$ to generate weights vector and then we perform simulations, by calculating the relevant covariance matrices to generate the portfolio returns. We therefore perform some Monte Carlo simulations, by calculating the covariance matrix and use the quadratic form expression, highlighted above to achieve our portfolio standard deviation. This does not involve covariance matrix inversion, which is computationally heavy.

## 3. The Optimisation Class

In this class, we included all the methods that we are going to deploy in our analysis, to first obtain FTSE MIB data and then computes all the risk returns analytics to then be applied to our Optimisers.
To check the full code, please visit the ipynb file!
