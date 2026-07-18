
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
$$= (2\sigma)^{-N} \cdot \exp\left(-\frac1\sigma\sum_{i=1}^N[(x_i - \mu)\cdot \mathbb 1_{x_i \gt \mu} - (x_i - \mu)\cdot \mathbb 1_{x_i \gt \mu}] \right)$$



## Question 5

### a)
### b)
### c) Find Lower bound of $Var(\hat\rho(\mathbf X))$

![[Pasted image 20260629153845.png]]



## Question 6

![[Pasted image 20260629154025.png]]
- We are given the conditional distribution of a single measurement $x_n$
$$f(x_n; \mu,\kappa) = \begin{cases} \frac1{2\pi I_0(\kappa)\exp \cos(x_n - \mu)} \quad:\quad -\pi \le x_n \le \pi \\  \quad\quad\quad\quad0\quad\quad\quad\quad :\quad else \quad \end{cases}$$
$$I_0(\kappa) := \int_{-\pi}^\pi e^{\kappa \cos(x)}dx$$
![[Pasted image 20260701151747.png]]

### a) von Mises distributed Random Vector

![[Pasted image 20260629154721.png]]

- Since the measurements $\mathbf x$ are i.i.d. the joint PDF of $\mathbf x$ is given by :
$$f(\mathbf x ; \mu,\kappa) = \prod_{i=1}^Nf(x_i ; \mu,\kappa) = (2\pi I_0(\kappa))^{-N}\prod_{i=1}^N \mathbb 1_{x_i \in[-\pi,\pi)}(x_i) \exp \left[\kappa\cos(x_i - \mu) \right]$$
$$f(\mathbf x ; \mu,\kappa) = (2\pi I_0(\kappa))^{-N}\cdot\mathbb 1_{\mathbf x \in[-\pi,\pi)}(\mathbf x) \cdot \exp \left[\kappa \sum_{i=1}^N \cos(x_i - \mu) \right]$$
- When, for convenience we denote :
$$1_{\mathbf x \in[-\pi,\pi)}(\mathbf x) = \begin{cases}1 \quad : \forall i \in \set{1,...,N} : x_i \in [-\pi,\pi) \\ 0 \quad :else  \end{cases}$$


- we can perform the following decomposition of the cosine to get :
$$\exp \left[\kappa \sum_{i=1}^N \cos(x_i - \mu) \right] = \exp \left[  \kappa \sum_{i=1}^N \cos(x_i)\cos(\mu)+\sin(x_i)\sin(\mu)   \right]$$
- Therefore, we can define the following statistics :
$$T_1(\mathbf x) = \sum_{i=1}^N\cos(x_i) \quad ;\quad  T_2(\mathbf x) = \sum_{i=1}^N\sin(x_i)$$

- We see that we can perform the following factorization :
$$g(T_1,T_2;\mu) = \exp[\cos(\mu)\cdot T_1(\mathbf x) + \sin(\mu)\cdot T_2(\mathbf x)] $$$$ h(\mathbf x) =  (2\pi I_0(\kappa))^{-N}\cdot\mathbb 1_{\mathbf x \in[-\pi,\pi)}(\mathbf x) $$
- Therefore, the statistics we defined for the estimation of the parameter $\mu$ from the measurements $\mathbf x$ are sufficient statistics.
### b) Find ML Estimator of $\mu$

![[Pasted image 20260629165716.png]]

- We take the log likelihood of the distribution of the measurement vector :

$$\log L(\mu ; \mathbf x) = f(\mathbf x ; \mu,\kappa) = -N \log(2\pi I_0(\kappa)) + \kappa (\cos(\mu)\cdot T_1(\mathbf x) + \sin(\mu)\cdot T_2(\mathbf x))$$
- We take the derivative with respect to the parameter $\mu$ and equate to 0 :
$$\frac{\partial\log L(\mu ; \mathbf x)}{\partial\mu} = \kappa (\sin(\mu)\cdot T_1(\mathbf x) - \cos(\mu)\cdot T_2(\mathbf x)) = 0$$
$$\implies \sin(\mu)\cdot T_1(\mathbf x) = \cos(\mu)\cdot T_2(\mathbf x) \implies \tan(\mu) = \frac{T_2(\mathbf x)}{T_1(\mathbf x)}$$
$$\implies \hat\mu_{ML}(\mathbf x) = \arctan\left(\frac{T_2(\mathbf x)}{T_1(\mathbf x)}\right)$$
- We want to make sure that the estimator is indeed a local maximum of the log likelihood function (and therefore also the likelihood function...). For that we will show that the second derivative is always negative :
$$\frac{\partial^2\log L(\mu ; \mathbf x)}{\partial\mu^2} = -\kappa (\cos(\mu)\cdot T_1(\mathbf x) + \sin(\mu)\cdot T_2(\mathbf x)) : \kappa \gt 0$$
- To show that the expression within the parentheses is always positive we will convert the two dimensional sufficient statistics into polar coordinates. We will define the following sufficient statistics based of the ones we found :
$$R(\mathbf x) : = \sqrt{T_1^2(\mathbf x) + T_2^2(\mathbf x)} \quad ; \quad \phi(\mathbf x) := \hat\mu_{ML}(\mathbf x) = \arctan\left(\frac{T_2(\mathbf x)}{T_1(\mathbf x)}\right)$$
- Now we can define our original sufficient statistics as a function of the new one :
$$\implies T_1(\mathbf x) = R(\mathbf x)\cdot \cos(\hat\mu) \quad ; \quad T_2(\mathbf x) = R(\mathbf x)\cdot \sin(\hat\mu)$$
- We substitute back into the expression for the second partial derivative :
$$\implies \frac{\partial^2\log L(\hat\mu ; \mathbf x)}{\partial\mu^2} = -\kappa (R(\mathbf x)\cdot \cos^2(\hat\mu) + R(\mathbf x)\cdot \sin^2(\hat\mu)) = -\kappa \cdot R(\mathbf x) \lt 0$$
- We can see that the second derivative is always negative so the estimator that we have found indeed brings the likelihood function to a maximum!
### c) Find ML Estimator of $\kappa$

![[Pasted image 20260629181506.png]]

- We derive the expression for the log likelihood of the parameter $\kappa$ given the measurements $\mathbf x$ :
$$\log L(\kappa ; \mathbf x) = f(\mathbf x ; \mu,\kappa) = -N \log(2\pi) -N \log (I_0(\kappa)) + \kappa (\cos(\mu)\cdot T_1(\mathbf x) + \sin(\mu)\cdot T_2(\mathbf x))$$
- We take the derivative with respect to the parameter $\kappa$ and equate to 0 :
$$\frac{\partial\log L(\kappa ; \mathbf x)}{\partial\kappa} = -N \frac1{I_0(\kappa)}\cdot \frac{\partial I_0(\kappa)}{\partial\kappa} + \cos(\mu)\cdot T_1(\mathbf x) + \sin(\mu)\cdot T_2(\mathbf x)$$
- We take the derivative of $I_0(\kappa)$ according to its definition :
$$I_0(\kappa) := \int_{-\pi}^\pi e^{\kappa \cos(x)}dx \implies \frac{\partial I_0(\kappa)}{\partial\kappa} = \int_{-\pi}^\pi \frac{\partial}{\partial\kappa}e^{\kappa \cos(x)}dx = \int_{-\pi}^\pi \cos(x)e^{\kappa \cos(x)}dx $$
- We have no analytic solution for the equation but we know that the estimator of $\kappa$ must satisfy the following equation :
$$\frac1{I_0(\kappa)}\cdot \frac{\partial I_0(\kappa)}{\partial\kappa} = \frac1N [\cos(\mu)\cdot T_1(\mathbf x) + \sin(\mu)\cdot T_2(\mathbf x)]$$


## Question 7

![[Pasted image 20260629191118.png]]

### a) Find the Likelihood of $\theta$

![[Pasted image 20260629191129.png]]
- For convenience, we denote the characteristic function of the interval $[\theta_1,\theta_2)$ as : 
$$\mathbb 1_{\mathbf x \in[\theta_1,\theta_2)}(\mathbf x) = \begin{cases}1 \quad : \forall i \in \set{1,...,N} : x_i \in [\theta_1,\theta_2) \\ 0 \quad :else  \end{cases}$$
- We derive the expression for the likelihood of the random vector $\mathbf \theta$ :
$$L(\theta ; \mathbf x) = f(\mathbf x ; \theta) \underbrace{=}_{x_i \overset{i.i.d}{\sim}U[\theta_1,\theta_2)} \prod_{i=1}^N\frac{1}{\theta_2 - \theta_1}\cdot \mathbb 1_{[-\pi,\pi)}(x_i) = \frac{1}{(\theta_2 - \theta_1)^N} \cdot \mathbb 1_{\mathbf x \in[\theta_1,\theta_2)}(\mathbf x)$$
- We can see that the value of the joint PDF is distributed uniformly in the domain $[\theta_1,\theta_2)^N$, so the maximum of the maximum of the joint PDF can be any point contained in the domain. That means that the only information we want about the measurements is what is the smallest interval that contains all measurements $\mathbf x$. We can define the following sufficient statistics :
$$T_1(\mathbf x) = \underset{i=1...N}{\min}\set{x_i} \quad ; \quad T_2(\mathbf x) = \underset{i=1...N}{\max}\set{x_i}$$
- We see that the original is actually a function of the new sufficient statistics. If the maximum and the minimum out of all measurements are contained in the interval then the rest and the measurements are contained in the interval of the sufficient statistics then that forces all measurements to be contained in the interval :
$$f(\mathbf x ; \theta) = \frac{1}{(\theta_2 - \theta_1)^N} \cdot \mathbb 1_{\mathbf x \in[\theta_1,\theta_2)}(\mathbf x) \equiv \mathbb 1_{ \mathbf [\theta_1,\infty)}(T_1(\mathbf x)) \cdot \mathbb 1_{ \mathbf (-\infty,\theta_2)}(T_2(\mathbf x)) \cdot \frac{1}{(\theta_2 - \theta_1)^N} $$

- Now, We can factorize the joint PDF as follows :
$$g(\mathbf T(\mathbf x); \theta) := \mathbb 1_{ \mathbf [\theta_1,\infty)}(T_1(\mathbf x)) \cdot \mathbb 1_{ \mathbf (-\infty,\theta_2)}(T_2(\mathbf x)) \cdot \frac{1}{(\theta_2 - \theta_1)^N} \quad ; \quad h(\mathbf x) := 1$$
- We can see that the defined statistics are indeed sufficient statistics for the estimation of the parameter vector $\theta$ from the measurements $\mathbf x$.

### b) Find ML Estimator 

![[Pasted image 20260629195512.png]]
- We look at expression for the likelihood function and see that we want to maximize the fraction term while satisfying the constraint that **all** measurements must be contained in the interval $[\theta_1,\theta_2)$. 
$$L(\theta ; \mathbf x ) = \underbrace{\frac{1}{(\theta_2 - \theta_1)^N}}_{maximize} \cdot \underbrace{\mathbb 1_{ \mathbf [\theta_1,\infty)}(T_1(\mathbf x)) \cdot \mathbb 1_{ \mathbf (-\infty,\theta_2)}(T_2(\mathbf x))}_{constraint}$$
- We see that to maximize the value of the expression we want to minimize the distance between the parameters $\theta_1, \theta_2$. The smallest possible interval that allows it the the interval between the sufficient statistics that we found, otherwise the entire expression goes to 0. Therefore the ML estimator is given by :
$$\hat\theta_{ML}(\mathbf x) = \begin{pmatrix}\hat\theta_{1,ML}(\mathbf x) \\ \hat\theta_{2,ML}(\mathbf x)\end{pmatrix} = \begin{pmatrix} T_1(\mathbf x) \\ T_2(\mathbf x) \end{pmatrix} $$
- As expected by theory, The ML estimator is a direct function of the sufficient statistics we defined.

### c) Estimators Bias

![[Pasted image 20260629195812.png]]

- We calculate the Bias of the proposed estimator :
$$Bias(\hat\theta(\mathbf x)) = \mathbb E[\hat\theta_{ML}(\mathbf x) - \theta]$$
- We will calculate the Bias of each component separately :
$$\mathbb E[\hat\theta_{1,ML}(\mathbf x)] = \mathbb E[\underset{i=1...N}{min}{\set{x_i}}] \quad , \quad \mathbb E[\hat\theta_{2,ML}(\mathbf x)] = \mathbb E[\underset{i=1...N}{max}{\set{x_i}}]$$
- To find the expected value we first need to find the distribution of the minimum and maximum of the random vector $\mathbf x$. We will do so by finding the derivative of the marginal CDF (cumulative distribution function) of the random variables $X_{min}:= \underset{i=1...N}{min} ,{\set{x_i}},X_{max} := \underset{i=1...N}{max}{\set{x_i}}$.
#### $X_{max}$ :
- We will first find the first term which is the CDF of the random variable $X_{max}$ :
$$F_{X_{max}}(t) = \mathbb P(X_{max} \le t) = \mathbb P\left(\bigcap_{i=1}^N \set{x_i \le t} \right) = \dots $$
- We know that the measurements are statistically independent :
$$\implies \prod_{i=1}^N \mathbb P(x_i \le t) = \prod_{i=1}^N \left[ \int_{-\infty}^{t}\frac{\mathbb 1_{[\theta_1,\theta_2)}(t)}{\theta_2 - \theta_1}dx \right] = \prod_{i=1}^N \left[ \frac{t - \theta_1}{\theta_2 - \theta_1} \cdot \mathbb 1_{[\theta_1,\theta_2)}(t) \right] = \left(\frac{t - \theta_1}{\theta_2 - \theta_1}\right)^N \cdot \mathbb 1_{[\theta_1,\theta_2)}(t)$$
- We get the joint CDF of the random variable $X_{max}$ :
$$F_{X_{max}}(t) = \left(\frac{t - \theta_1}{\theta_2 - \theta_1}\right)^N \cdot \mathbb 1_{[\theta_1,\theta_2)}(t) $$
- We take the derivative with respect to $t$ and find the PDF of $X_{max}$ :
$$f_{X_{max}}(t) = \frac{dF_{X_{max}}(t)}{dt} = \frac{d}{dt}\left(\frac{t - \theta_1}{\theta_2 - \theta_1}\right)^N \cdot \mathbb 1_{[\theta_1,\theta_2)}(t) $$$$ \implies f_{X_{max}}(t) = \frac{N}{\theta_2 - \theta_1}\left(\frac{t - \theta_1}{\theta_2 - \theta_1}\right)^{N-1} \cdot \mathbb 1_{[\theta_1,\theta_2)}(t)$$
#### $X_{min}$ :
- We will do the same for the second term which is the CDF of the random variable $X_{min}$ :
$$F_{X_{min}}(t) = \mathbb P(X_{min} \le t) = 1 - \mathbb P(X_{min} \ge t) = \mathbb P\left(\bigcap_{i=1}^N \set{x_i \ge t} \right) = \dots $$
- We know that the measurements are statistically independent :
$$\implies \prod_{i=1}^N \mathbb P(x_i \ge t) = \prod_{i=1}^N \left[ \int_{t}^{\infty}\frac{\mathbb 1_{[\theta_1,\theta_2)}(t)}{\theta_2 - \theta_1}dx \right] = \prod_{i=1}^N \left[ \frac{\theta_2 - t}{\theta_2 - \theta_1} \cdot \mathbb 1_{[\theta_1,\theta_2)}(t) \right] = \left(\frac{\theta_2 - t}{\theta_2 - \theta_1}\right)^N \cdot \mathbb 1_{[\theta_1,\theta_2)}(t)$$
- We get the joint CDF of the random variable $X_{min}$ :
$$F_{X_{min}}(t) = 1- \left(\frac{\theta_2 - t}{\theta_2 - \theta_1}\right)^N \cdot \mathbb 1_{[\theta_1,\theta_2)}(t) $$
- We will take the derivative with respect to $t$ :
$$f_{X_{min}}(t) = \frac{dF_{X_{min}}(t)}{dt} = \frac{d}{dt}\left( 1 - \left(\frac{\theta_2 - t}{\theta_2 - \theta_1}\right)^N \cdot \mathbb 1_{[\theta_1,\theta_2)}(t) \right)$$
$$\implies f_{X_{min}}(t) = \frac{N}{\theta_2 - \theta_1}\left(\frac{\theta_2 - t}{\theta_2 - \theta_1}\right)^{N-1} \cdot \mathbb 1_{[\theta_1,\theta_2)}(t)$$
- Now we will evaluate the expected values of each of the random variables :
#### $\mathbb E[X_{max}]$ :
$$\mathbb E[X_{max}] = \int_{\mathbb R} t\cdot f_{X_{max}}(t)dt = \int_{\mathbb R}t \cdot \frac{N}{\theta_2 - \theta_1}\left(\frac{t - \theta_1}{\theta_2 - \theta_1}\right)^{N-1} \cdot \mathbb 1_{[\theta_1,\theta_2)}(t)dt $$$$= \int_{\theta_1}^{\theta_2} \frac{Nt - N\theta_1 + N\theta_1}{\theta_2 - \theta_1}\left(\frac{t - \theta_1}{\theta_2 - \theta_1}\right)^{N-1} dt = \int_{\theta_1}^{\theta_2} N\left(\frac{t - \theta_1}{\theta_2 - \theta_1}\right)^{N} dt + \int_{\theta_1}^{\theta_2} \frac{N\theta_1}{\theta_2 - \theta_1}\left(\frac{t - \theta_1}{\theta_2 - \theta_1}\right)^{N-1} dt $$
- We perform a substitution in the integrals  $u = \frac{t-\theta_1}{\theta_2-\theta_1} , du = \frac1{\theta_2 - \theta_1}dt , 0 \le u \lt 1$ :
$$= (\theta_2 - \theta_1)\int_0^1Nu^Ndu + (\theta_2 - \theta_1)\int_0^1\frac{N\theta_1}{\theta_2 - \theta_1}u^{N-1}du = (\theta_2 - \theta_1) \left[ \left. \frac{N}{N+1}u^{N+1} + \frac{\theta_1}{\theta_2-\theta_1}u^N \right|_0^1 \right] $$$$ \dots = \frac{N}{N+1}(\theta_2 - \theta_1) + \theta_1 \implies \mathbb E[X_{max}] = \frac{N}{N+1}\theta_2 + \frac{1}{N+1}\theta_1 $$
#### $\mathbb E[X_{min}]$ :
$$\mathbb E[X_{min}] = \int_{\mathbb R} t\cdot f_{X_{min}}(t)dt = \int_{\mathbb R}t \cdot \frac{N}{\theta_2 - \theta_1}\left(\frac{\theta_2 - t}{\theta_2 - \theta_1}\right)^{N-1} \cdot \mathbb 1_{[\theta_1,\theta_2)}(t)dt $$$$= \int_{\theta_1}^{\theta_2} -\frac{ - N\theta_2 + N\theta_2 - Nt}{\theta_2 - \theta_1}\left(\frac{\theta_2 - t}{\theta_2 - \theta_1}\right)^{N-1} dt = $$$$ = -\int_{\theta_1}^{\theta_2} N\left(\frac{\theta_2-t}{\theta_2 - \theta_1}\right)^{N} dt + \int_{\theta_1}^{\theta_2} \frac{N\theta_2}{\theta_2 - \theta_1}\left(\frac{\theta_2-t}{\theta_2 - \theta_1}\right)^{N-1} dt $$
- We perform a substitution in the integrals  $u = \frac{\theta_2-t}{\theta_2-\theta_1} , du = -\frac1{\theta_2 - \theta_1}dt , 0 \le u \lt 1$ :
$$= -(\theta_2 - \theta_1)\int_0^1Nu^Ndu + {(\theta_2 - \theta_1)}\int_0^1\frac{N\theta_2}{\theta_2 - \theta_1}u^{N-1}du = (\theta_2 - \theta_1) \left[ \left. -\frac{N}{N+1}u^{N+1} + \frac{\theta_2}{\theta_2-\theta_1}u^N \right|_0^1 \right] $$$$ \dots = -\frac{N}{N+1}(\theta_2 - \theta_1) + \theta_2 \implies \mathbb E[X_{min}] = \frac{N}{N+1}\theta_1  - \frac{1}{N+1}\theta_2$$
#### $Bias(\hat\theta_1)$ :
- We substitute the term of the expected value that we calculated :
$$Bias(\hat\theta_1) = \mathbb E[X_{min}] - \theta_1 = \frac{N}{N+1}\theta_1  + \frac{1}{N+1}\theta_2 + \theta_1$$
$$\implies Bias(\hat\theta_1) = -\frac{1}{N+1}\theta_1 - \frac{1}{N+1}\theta_2 \underset{N \to \infty}{\longrightarrow} 0 $$
- We see that $\hat\theta_1$ is unbiased only asymptotically.

#### $Bias(\hat\theta_2)$ :
- We substitute the term of the expected value that we calculated :
$$Bias(\hat\theta_2) = \mathbb E[X_{max}] - \theta_2 = \frac{N}{N+1}\theta_2  + \frac{1}{N+1}\theta_1 - \theta_2$$
$$\implies Bias(\hat\theta_2) = \frac{1}{N+1}\theta_1 - \frac{1}{N+1}\theta_2 \underset{N \to \infty}{\longrightarrow} 0 $$
- We see that $\hat\theta_2$ is unbiased only asymptotically as well.
#### Bias Correction :
- We want to add a correction term for the original estimator that is a function of the sufficient statistic that we have found earlier. For that we want to estimate the distance between the parameters :
$$Bias(\hat\theta_1) = \frac{1}{N+1}(\theta_2 - \theta_1) \quad ; \quad Bias(\hat\theta_2) = -\frac{1}{N+1}(\theta_1 - \theta_2) $$
- We want to express the distance between the parameters as the expected value of a function of the sufficient statistics :
$$\mathbb E[T_2 - T_1] = \mathbb E[X_{max}] - \mathbb E[X_{min}] = \frac{N}{N+1}\theta_2 + \frac{1}{N+1}\theta_1 - \left[ \frac{N}{N+1}\theta_1  - \frac{1}{N+1}\theta_2\right]$$
$$\mathbb E[T_2 - T_1] = \frac{N-1}{N+1}(\theta_2 - \theta_1) \implies \frac{1}{N-1}\mathbb E[T_2-T_1] = \frac1{N+1}(\theta_2 - \theta_1)  $$
- We can see that by adding the following terms to the original ML estimators we correct their bias, we denote the new unbiased estimators $\tilde\theta_1, \tilde\theta_2$ respectively: 
$$\tilde\theta_1 = \hat\theta_{1,ML} - \frac1{N-1}[T_2 - T1] \implies \mathbb E [\tilde\theta_1] = \theta_1  $$
$$\tilde\theta_2 = \hat\theta_{2,ML} - \frac1{N-1}[T_2 - T1] \implies \mathbb E [\tilde\theta_2] = \theta_2 $$
- We get that our new corrected estimator is unbiased :
$$\tilde\theta(\mathbf x) = \begin{pmatrix}\tilde\theta_{1,ML}(\mathbf x) \\ \tilde\theta_{2,ML}(\mathbf x)\end{pmatrix} = \begin{pmatrix} T_1(\mathbf x) \\ T_2(\mathbf x) \end{pmatrix} +\begin{pmatrix} -1 \\ 1 \end{pmatrix} \cdot  \frac{1}{N-1}(T_2(\mathbf x)-T_1(\mathbf x)) $$
### d) Find MVU estimator :

![[Pasted image 20260701135919.png]]

 We will use the **Lehmann - Scheffe Theorem** that states that : "if $T$ is a sufficient statistics for the estimation of the parameters $\theta$ out of the measurements $\mathbf x$ and it is **complete** then any unbiased estimator that is solely a function of $T$ is uniquely the MVU estimator".

- We have already shown that $\tilde \theta(\mathbf x)$ is an unbiased estimator and we built it strictly as solely a function of the sufficient statistics $\mathbf T = (T_1,T_2)^T$.

- What is left to do is show that the sufficient statistics is **complete**. For that we will use the definition of completeness by showing that there exist only one function $g(T_1,T_2)$ such that :
$$\mathbb E[g(T_1,T_2)] = 0 : \forall \theta \in \mathbb R^2 : \theta_1 \le \theta_2$$
- We will expand the term for the expected value of $g$ as follows :
$$\mathbb E[g(T_1,T_2)] = \int_{\theta_1}^{\theta_2}\int_{t1}^{\theta_2} g(t_1,t_2)\cdot f_{T_1,T_2}(t_1,t_2)dt_2dt_1$$
- We want to find the joint PDF of the sufficient statistics that we found. For that we use the hint given in the question to find the joint CDF and take the partial derivatives :
![[Pasted image 20260701143806.png]]

- We can write out the expression for the joint CDF :
$$F_{T_1,T_2}(t_1,t_2) = \dots = \mathbb P(X_{max}\le t_2) - P(t_1 \le X_{min} ,X_{max} \le t_2) $$
- The first term has already been calculated before :
$$\mathbb P(X_{max}\le t_2) = F_{X_{max}}(t_2) = \left(\frac{t_2 - \theta_1}{\theta_2 - \theta_1}\right)^N$$
- The second term can be expressed as follows :
$$\mathbb P(t_1 \le X_{min} ,X_{max} \le t_2) = \mathbb P \left( \bigcap_{i=1}^N\set{t_1 \le x_i \le t_2} \right) = \prod_{i=1}^N(F_{x_i}(t_2) - F_{x_i}(t_1)) = (F_{x_i}(t_2) - F_{x_i}(t_1))^N$$
$$\implies \mathbb P(t_1 \le X_{min} ,X_{max} \le t_2)  = \left(\frac{t_2 - t1}{\theta_2 - \theta_1}\right)^N$$
- We get the joint CDF of the sufficient statistics to be :
$$F_{T_1,T_2}(t_1,t_2) = \left(\frac{t_2 - \theta_1}{\theta_2 - \theta_1}\right)^N -  \left(\frac{t_2 - t1}{\theta_2 - \theta_1}\right)^N$$
- To find the joint PDF we take partial derivatives with respect to each of the parameters $t_1,t_2$ : 
$$f_{T_1,T_2}(t_1,t_2) = \frac{\partial^2}{\partial t_1 \partial t_2}F_{T_1,T_2}(t_1,t_2)$$
$$\implies \frac{\partial}{\partial t_1}F_{T_1,T_2}(t_1,t_2) = \frac{\partial}{\partial t_1}\cancel{\left(\frac{t_2 - \theta_1}{\theta_2 - \theta_1}\right)^N} -  \frac{\partial}{\partial t_1}\left(\frac{t_2 - t1}{\theta_2 - \theta_1}\right)^N = \cancel{-}\left( \frac{\cancel{-}N}{\theta_2-\theta_1}\left(\frac{t_2 - t1}{\theta_2 - \theta_1}\right)^{N-1} \right) $$
$$\implies \frac{\partial^2}{\partial t_1\partial t_2}F_{T_1,T_2}(t_1,t_2) = \frac{\partial}{\partial t_2}\left( \frac{N}{\theta_2-\theta_1}\left(\frac{t_2 - t1}{\theta_2 - \theta_1}\right)^{N-1} \right) = \frac{N(N-1)}{(\theta_2-\theta_1)^2}\left(\frac{t_2 - t1}{\theta_2 - \theta_1}\right)^{N-2}  $$
$$f_{T_1,T_2}(t_1,t_2) = \frac{N(N-1)}{(\theta_2-\theta_1)^2}\left(\frac{t_2 - t1}{\theta_2 - \theta_1}\right)^{N-2}$$
- We plug that back into the expected value :
$$\mathbb E[g(T_1,T_2)] = \int_{\theta_1}^{\theta_2}\int_{t_1}^{\theta_2} g(t_1,t_2)\cdot \frac{N(N-1)}{(\theta_2-\theta_1)^2}\left(\frac{t_2 - t1}{\theta_2 - \theta_1}\right)^{N-2}dt_2dt_1$$
- We see that the integrand is always positive since $t_2 \ge t_1$ within all the domain of the integration when equality is satisfied at the lower bound of integration of $t_2$. Therefore the integral itself can be 0 if and only if the the integrand is equinely 0. These solely happens for the case where $g(t_1,t_2) \equiv 0$.
- $\implies$ This means that the third condition for completeness is satisfied and the sufficient statistics we found are complete sufficient statistics
- $\implies$ Finally, This means that our unbiased estimator $\tilde\theta(\mathbf x)$ is uniquely the MVU!