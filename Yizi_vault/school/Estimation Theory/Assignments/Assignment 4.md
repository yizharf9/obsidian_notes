
## Question 1
![[Pasted image 20260618104715.png]]

### a) Finding Sufficient Statistics
![[Pasted image 20260625133849.png]]

To find a sufficient statistic of $\mathbf x$ for estimating $\lambda$ we will use the **Neyman-Fisher Factorization**.
We need to factorize the joint-PDF of the R.V.s $x_1,...,x_n$ the following way :
$$f_{\mathbf x | \lambda}(\mathbf x ; \lambda) = g(t(\mathbf x); \lambda) \cdot h(\mathbf x )$$
- The R.V.s are discrete so what we are actually looking for is :
$$\mathbb P (\mathbf x | \lambda ) = \mathbb P (x_1...,x_n|\lambda) = g(t(\mathbf x);\lambda) \cdot h(\mathbf x) $$
- We find the joint-PDF of the random vector $\mathbf x = (x_1,...,x_n)$ :
$$\mathbb P (\mathbf x | \lambda ) \underbrace{=}_{i.i.d.} \prod_{i=1}^n {e^{-\lambda} \cdot \frac{\lambda^{x_i}}{(x_i)!}} = {e^{-n\lambda} \cdot \lambda^{(\sum_{i=1}^n x_i)} \cdot \prod_{i=1}^n \frac{1}{(x_i)!}}$$
- We notice that when defining the statistics $t(\mathbf x) = \sum_{i=1}^n x_i$ we can perform the following factorization :

$$g(t(\mathbf x) ; \lambda) := e^{-n\lambda} \cdot \lambda^{(\sum_{i=1}^nx_i)} = e^{-n\lambda} \cdot \lambda^{t(\mathbf x)} \ , \ h(\mathbf x) := \prod_{i=1}^n \frac1{(x_i)!}$$
$$\implies \mathbb P (\mathbf x | \lambda) = g(t(\mathbf x) ; \lambda) \cdot h(\mathbf x)$$
- Invoking the **Neyman-Fisher Factorization**, we see that the statistics $t(\mathbf x)$ is a sufficient statistics.

- To Prove the minimality of $t(\mathbf x)$, we would like to show that it is a **complete** sufficient statistics of $\lambda$. For that, we want to show that for any function $g$, if $\forall \lambda \in \mathbb R : \mathbb E_{\lambda}\left[ g(t(\mathbf x))\right] = 0$, then it must imply that $g(t(\mathbf x)) \equiv 0$.

- For convenience, we will denote $t = t(\mathbf x)$ and We will find the function $g$ by expanding the expected value of $g$ :
$$\mathbb E_\lambda [g(t)] = \sum_{t =0}^{\infty}g(t)\cdot \mathbb P(t)$$
- We would like to substitute the probability function of $t$ to the term so we will derive the distribution of $t$.
- We will use the moment generating function of the random variable $t$ , $M_{t(\mathbf x)}(s)$ :
$$M_{t(\mathbf x)}(s) = \mathbb E[e^{s \cdot t(\mathbf x)}] = \mathbb E[e^{s \cdot \sum_{i=1}^n x_i}] \underbrace{=}_{x_i \underset{i.i.d}{\sim} Poi(\lambda)} \mathbb \prod_{i=1}^n \mathbb E[e^{s\cdot x_i}]  $$
- We will find the expression for the MGF of a single Poisson random variable $x$ :
$$M_{x}(s) = \mathbb E[e^{s\cdot x}] = \sum_{k=0}^\infty e^{sx}\cdot e^{-\lambda} \cdot \frac{\lambda^k}{k!} = e^{-\lambda} \cdot \sum_{k=0}^\infty \frac{(e^s \cdot \lambda)^k}{k!} = e^{-\lambda}\cdot e^{\lambda e^s} = \exp(\lambda (e^s - 1)) $$
- We substitute back to the MGF of the sufficient statistics :
$$\implies M_{t(\mathbf x)}(s) = \prod_{i=1}^n \exp(\lambda (e^s - 1)) = \exp(n\lambda (e^s - 1))$$
- We notice that the MGF of the sufficient statistics is an equivalent of an MGF of a Poisson random variable with mean $n\lambda$ and that is possible $\iff$ $t(\mathbf x) \sim Poi(n\lambda)$.

- We conclude that the probability function of the sufficient statistics is :
$$P(t = k) = e^{-n\lambda}\cdot\frac{(n\lambda)^k}{k!} $$
- We substitute that back into the expected value of the function $g$ :
$$\implies \mathbb E_\lambda [g(t)] = \sum_{t =0}^{\infty}g(t)\cdot e^{-n\lambda}\frac{(n\lambda)^t}{t!} = e^{-n\lambda} \cdot \sum_{t =0}^{\infty} \left(\frac{g(t)\cdot n^t}{t!} \right) \cdot \lambda^t  $$
- We want to force the above expression to be 0 :
$$ e^{-n\lambda} \cdot \sum_{t =0}^{\infty} \left(\frac{g(t)\cdot n^t}{t!} \right) \cdot \lambda^t = 0 \implies \sum_{t =0}^{\infty} \left(\frac{g(t)\cdot n^t}{t!} \right) \cdot \lambda^t = 0 $$
- We notice that we get a power series with the argument $\lambda$. A power series can be the equivalent of the zero function $\iff$ all coefficients of the series must be equal to 0. This means that  $\frac{g(t)\cdot n^t}{t!} = 0$ which forces the function $g(t) \equiv 0$. 

- Therefore there exists a single function that sets the expected value to be 0 for every value of $\lambda$ which means that $t(\mathbf x)$ is a complete sufficient statistics for the estimation of $\lambda$ from the measurements $\mathbf x$. 
### b) Find ML estimator
![[Pasted image 20260625133047.png]]

By definition the ML function is defined as 
$$L(\lambda ; \mathbf x) = \prod_{i=1}^N\mathbb P(x_i|\lambda)$$
- We substitute the PDF we found previously:
$$L(\lambda ; \mathbf x) = \prod_{i=1}^N \frac{e^{-\lambda} \cdot \lambda^{x_i}}{x_i !} = \frac{e^{-N\lambda} \cdot \lambda^{\sum_{i=1}^Nx_i}}{\prod_{i=1}^Nx_i!}$$
- For convenience, we will take find the maximal argument of the logarithm of the likelihood function instead so first we will take the logarithm of the likelihood function :
$$\log L(\lambda ; \mathbf x)  = -N\lambda + \log(\lambda)\cdot\sum_{i=1}^N x_i - log(\prod_{i=1}^N x_i!)$$
- To find the minimum of the likelihood function we will take the derivative and equate to 0 :
$$\frac{\partial \log L(\lambda;\mathbf x)}{\partial \lambda} = -N + \frac1\lambda \sum_{i=1}^N x_i = 0 $$
$$\implies \lambda = \frac1N\sum_{i=1}^Nx_i $$
- We make sure it is indeed a maximum using the second derivative :
$$\frac{\partial^2 \log L(\lambda;\mathbf x)}{\partial \lambda^2} =  -\frac1{\lambda^2} \sum_{i=1}^N x_i \lt 0 : \forall \lambda \in \mathbb R \implies \lambda_{max} = t(\mathbf x)  :=  \frac1N\sum_{i=1}^Nx_i$$
- We have found the ML estimator of the and as expected we see that it is a function of the sufficient statistics we have found in previous subsection.
$$\hat\lambda_{ML}(\mathbf x) = \frac1N\sum_{i=1}^Nx_i$$

## Question 2

![[Pasted image 20260627001708.png]]

### a) + b) Find Sufficient Statistics of $\mu$

![[Pasted image 20260627001818.png]]

We will find the sufficient statistics for the estimation of $\mu$ from the measurements $\mathbf x$. We will perform the **Neyman-Fisher Factorization** of the joint-PDF of the measurements $\mathbf x$ :

$$f(\mathbf x ; \mu) = (2\sigma)^{-N} \cdot \prod_{i=1}^N \exp\left(-\frac{|x_i - \mu|}{\sigma}\right) = (2\sigma)^{-N} \cdot \exp\left(-\frac1\sigma\sum_{i=1}^N |x_i - \mu|\right)$$
- We notice that we can factorize the expression the following way :
$$g(t(\mathbf x),\mu) = (2\sigma)^{-N} \cdot \exp\left(-\frac1\sigma\sum_{i=1}^N |x_i - \mu|\right) \quad ; \quad h(\mathbf x) = 1 $$
- We can't factorize the original expression any further since the absolute value term $|x_i - \mu|$ is not factorable (it is a piecewise function that is constructed on $\mu$). That means that we cannot compress the original data $\mathbf x$, we must use all of it for a proper estimation of the parameter $\mu$.
$$\implies t(\mathbf x) = \mathbf x$$

- We will now find the ML estimator for $\mu$ out of the measurement $\mathbf x$. We will find the log likelihood function and find its maximum :
$$\log L(\mathbf x ; \mu) =  -N\cdot \log(2\sigma) - \frac1\sigma\sum_{i=1}^N|x_i - \mu| \implies \frac{\partial\log L(\mathbf x ; \mu)}{\partial\mu} = - \frac1\sigma\sum_{i=1}^N sgn(x_i - \mu) = 0$$
- We notice that for the sum to be 0 we need to find a point in the middle of all samples such that all measurements that are smaller will yield $sgn(x-\mu) = -1$ and the larger will yield $sgn(x-\mu) = 1$ :
$$\sum_{i=1}^N sgn(x_i -\mu) = \sum_{i=1}^{\frac N2} sgn(x_i -\mu) + \sum_{i=\frac N2}^{N} sgn(x_i -\mu) = -\frac N2 + \frac N2  = 0$$
- Therefore, the value that maximizes the log likelihood and so the likelihood function is the median of all the measurements $\mathbf x$:
$$\implies \hat\mu_{ML}(\mathbf x ) = median\set{x_1,...,x_n}$$
### c) + d) Find Sufficient Statistics of $\sigma$

![[Pasted image 20260627224145.png]]

- Using the same joint PDF we have found before we find the **Neyman-Fisher Factorization** :

$$f(\mathbf x ; \mu) = (2\sigma)^{-N} \cdot \exp\left(-\frac1\sigma\sum_{i=1}^N |x_i - \mu|\right)$$
- Since the term in the exponent is not factorable we factor it the same way as for in the previous subsections :
$$g(t(\mathbf x),\sigma) = (2\sigma)^{-N} \cdot \exp\left(-\frac1\sigma\sum_{i=1}^N |x_i - \mu|\right) \quad ; \quad h(\mathbf x) = 1 $$
 - We find can see that the sufficient statistics for the estimation of $\sigma$ from the measurements $\mathbf x$ is given by :
$$\implies t(\mathbf x) = \sum_{i=1}^N |x_i - \mu|$$
- We will find the ML estimator by finding the maximal argument of the log likelihood function :
$$\log L(\mathbf x ; \mu) =  -N\cdot \log(2\sigma) - \frac1\sigma\sum_{i=1}^N|x_i - \mu| \implies \frac{\partial\log L(\mathbf x ; \mu)}{\partial\mu} = -\frac{N}{\sigma}+\frac1{\sigma^2}\sum_{i=1}^N |x_i - \mu| = 0$$
$$\implies -N\sigma + \sum_{i=1}^N|x_i - \mu| = 0 \implies \sigma = \frac1N\sum_{i=1}^N|x_i - \mu|$$
- We find that the ML estimator of $\sigma$ is a function of the sufficient statistics that we found :
$$\hat\sigma_{ML}(\mathbf x ) = \frac1N\sum_{i=1}^N|x_i - \mu| = \frac1N \cdot t(x)$$
## Question 3 

![[Pasted image 20260627230435.png]]

### a) Find ML estimator

![[Pasted image 20260627230451.png]]

- We derive the expression for the joint PDF of all measurements and take the log likelihood :
$$f(\mathbf x ;\theta) = \prod_{i=1}^Nf(x_i ;\theta) = \prod_{i=1}^N {L\choose x_i}\cdot \theta^{x_i}\cdot (1-\theta)^{L-x_i}$$
$$\log L(\mathbf x ; \theta) = \sum_{i=1}^N\left[ \log{L\choose x_i} + x_i \log\theta + (L-x_i)\log(1-\theta)\right]$$

$$\frac{\partial\log L(\mathbf x ; \theta)}{\partial\theta} =  \sum_{i=1}^N\left[ \frac1\theta x_i - \frac1{(1-\theta)}(L-x_i)\right] = 0 $$ 
$$ \frac1\theta\sum_{i=1}^N x_i - \frac1{1-\theta}\sum_{i=1}^N(L-x_i) = (1-\theta)\sum_{i=1}^N x_i - \theta\sum_{i=1}^N(L-x_i) $$
$$ = \sum_{i=1}^Nx_i \cancel{-\theta \sum_{i=1}^Nx_i} - \theta NL + \cancel{\theta\sum_{i=1}^Nx_i} = 0 \implies \theta = \frac1{NL}\sum_{i=1}^Nx_i$$
- We find that the ML estimator is given by :
$$\hat\theta_{ML}(\mathbf x) = \frac1{NL}\sum_{i=1}^Nx_i = \frac1L\bar x$$
### b) Efficiency

![[Pasted image 20260627235025.png]]

To see if the estimator is efficient we will check if it is unbiased, if it is then we will check if it achieves the CRB for estimation of $\theta$ from the measurements $\mathbf x$.

- First, we will check if the estimator is unbiased :
$$Bias(\hat\theta_{ML}) = \mathbb E[\hat\theta_{ML} - \theta]$$
$$\mathbb E[\hat\theta_{ML}(\mathbf x)] = \frac1{NL}\sum_{i=1}^N\mathbb E [x_i] \underbrace{=}_{x_i\perp \! \perp x_j \sim Bin(L,\theta)} \frac1{NL}\sum_{i=1}^N L\theta = \theta $$
- We find that the estimator is indeed unbiased :
$$\implies Bias(\hat\theta_{ML}) = \theta-\theta = 0$$
- We will find the variance of the estimator :
$$Var(\hat\theta_{ML}(\mathbf x)) = \mathbb E \left[\left( \frac1{NL}\sum_{i=1}^Nx_i  \right)^2\right] = \frac1{(NL)^2}\sum_{i=1}^N\sum_{k=1}^N\mathbb E [x_ix_k] $$
$$\implies Var(\hat\theta_{ML}(\mathbf x)) = \frac1{(NL)^{\cancel{2}}}[\cancel{N \cdot L}\theta(1-\theta)] = \frac{\theta(1-\theta)}{NL}$$
- We calculate the CRB for estimation of $\theta$ from $\mathbf x$ :
$$\mathcal I(\theta) = -\mathbb E\left[\frac{\partial^2\log f(\mathbf x ; \theta)}{\partial\theta^2}\right]$$
$$\implies \log f(\mathbf x ; \theta) = \sum_{i=1}^N\left[ \log{L\choose x_i} + x_i \log\theta + (L-x_i)\log(1-\theta)\right]$$
$$\implies \frac{\partial\log f(\mathbf x ; \theta)}{\partial\theta} = \sum_{i=1}^N\left[ \frac1\theta x_i - \frac1{(1-\theta)}(L-x_i)\right]$$
$$\implies \frac{\partial^2\log f(\mathbf x ; \theta)}{\partial\theta^2} = \sum_{i=1}^N\left[ -\frac1{\theta^2} x_i - \frac1{(1-\theta)^2}(L-x_i)\right]$$
$$\implies \mathbb E \left[\frac{\partial^2\log f(\mathbf x ; \theta)}{\partial\theta^2}\right] = \sum_{i=1}^N\left[ -\frac1{\theta^2} \mathbb E [x_i] - \frac1{(1-\theta)^2}(L-\mathbb E [x_i])\right] $$$$ = \sum_{i=1}^N\left[ -\frac1{\theta^2} L\theta - \frac1{(1-\theta)^2}(L-L\theta)\right] = N\left[ -\frac L{\theta}  - \frac L{(1-\theta)}\right] = NL\left[ - \frac {1-\theta + \theta}{(1-\theta)}\right] = -\frac{NL}{\theta(1-\theta)}$$
$$\implies \mathcal I(\theta) = \frac{NL}{\theta(1-\theta)}$$
- We see that the CRB matches the variance of the ML estimator :
$$\implies CRB = \frac{\theta(1-\theta)}{NL} = Var(\hat\theta_{ML}(\mathbf x))$$

## Question 4 

![[Pasted image 20260628011738.png]]

### a) Prove Sufficient statistics

![[Pasted image 20260628011801.png]]

- We will derive the expression of the joint PDF of the measurement vector :
$$f(\mathbf x ; \theta) = \prod_{i=1}^N \theta^{x_i} \cdot (1-\theta)^{1-x_i} = \theta^{\sum_{i=1}^Nx_i}\cdot (1-\theta)^{N - \sum_{i=1}^Nx_i} = \theta^{t(\mathbf x)} \cdot (1- \theta)^{N - t(\mathbf x)}$$
- We can see that the exponent cannot be factorized out from the base and therefore we can factorize the joint PDF as follows : 
$$g(t(\mathbf x); \theta) := \theta^{t(\mathbf x)} \cdot (1- \theta)^{N - t(\mathbf x)} \quad ; \quad h(\mathbf x) = 1$$
- Since we found a factorization $g$ that is a function of the statistics that we previously defined, we can now say that $t(\mathbf x)$ is a sufficient statistics for the estimation of $\theta$ from $\mathbf x$.

### b) Prove Minimality

![[Pasted image 20260628013445.png]]

 We will show that the sufficient statistics for $\theta$ is complete and therefore minimal.

- By definition, we want to show that there exists **only a single function** $s(t)$ of the sufficient statistics such that :
$$\forall \theta\in [0,1] : \mathbb E[g(t)|\theta] = 0 $$
- We will expand the expected value term accordingly :
$$\mathbb E [g(t)] = \sum_{t}g(t) \cdot \mathbb P(t)$$
- Since $t$ is a sum of bernoulli distributed discrete random variables, is follows a Binomial distribution :
$$\implies t \sim Bin(N,\theta) \quad ; \quad \mathbb P(t) = {N\choose t} \cdot \theta^t \cdot (1-\theta)^{N-t} \quad ; \quad t \in \set{0,\dots,N}$$
- We plug it back into the expected value :
$$\mathbb E [g(t)] = \sum_{t=0}^N g(t) \cdot {N\choose t} \cdot \theta^t \cdot (1-\theta)^{N-t} \ge 0$$
- Since all terms inside the sum but $g(t)$ are strictly greater of equal to 0 we know for sure that the only function that will bring the whole term to 0 is the zero function :

$$\forall \theta\in [0,1] : \mathbb E[g(t)|\theta] = 0  \iff g(t)\equiv 0 $$
- This proves that the sufficient statistics $t(\mathbf x)$ is a complete sufficient statistics and therefore minimal.

### c) Prove Completeness
![[Pasted image 20260628020142.png]]
See subsection b).

## Question 5

![[Pasted image 20260628132353.png]]

### a) ML estimator

![[Pasted image 20260628132412.png]]
$$f(\mathbf x_n;\rho) = \frac{1}{2\pi\sqrt{1-\rho^2}} \exp\left[ -\frac{x_{1,n}^2 - 2\rho x_{1,n}x_{2,n} + x_{2,n}^2}{2(1-\rho^2)} \right]$$
To find the likelihood function we will use the fact that the pairs of samples $\mathbf x_n = [x_{1,n},x_{2,n}]$ are independent of each other. Therefore, the Likelihood function of $\rho$ from the measurements $\mathbf X = [\mathbf x_1...\mathbf x_N]^T$ is given by : 
$$L(\rho ; \mathbf X) = \prod_{n=1}^N f(\mathbf x_n;\rho) = \prod_{n=1}^N\frac{1}{2\pi\sqrt{1-\rho^2}} \exp\left[ -\frac{x_{1,n}^2 - 2\rho x_{1,n}x_{2,n} + x_{2,n}^2}{2(1-\rho^2)} \right] = $$$$\implies L(\rho ; \mathbf X) = \frac{1}{(2\pi\sqrt{1-\rho^2})^N} \exp\left[ -\frac1{2(1-\rho^2)}\sum_{n=1}^N (x_{1,n}^2 - 2\rho x_{1,n}x_{2,n} + x_{2,n}^2) \right] $$
### b) Find Min Sufficient statistics of $\rho$

![[Pasted image 20260628150415.png]]

- We reorganize the likelihood function we derived earlier as follows :
$$L(\rho ; \mathbf X) = \frac{1}{(2\pi\sqrt{1-\rho^2})^N} \exp\left[ -\frac1{2(1-\rho^2)}\sum_{n=1}^N (x_{1,n}^2  + x_{2,n}^2) \right] \exp\left[ \frac{\rho}{2(1-\rho^2)} \sum_{n=1}^N  x_{1,n}x_{2,n} \right] $$
- We define the following statistics $\mathbf T_1 ,\mathbf T_2$ :
$$\mathbf T_1(\mathbf X) = \sum_{n=1}^N (x_{1,n}^2  + x_{2,n}^2) \quad ; \quad \mathbf T_2(\mathbf X) = \sum_{n=1}^N  x_{1,n}x_{2,n}$$
- We notice that we can factorize the likelihood function to 2 functions of each of the statistics we defined :
$$L(\rho ; \mathbf X) = \frac{1}{(2\pi\sqrt{1-\rho^2})^N} \exp\left[ -\frac{1}{2(1-\rho^2)}\mathbf T_1(\mathbf X) \right] \exp\left[ -\frac\rho{1-\rho^2}\mathbf T_2(\mathbf X) \right] $$
- We can see that the statistics
