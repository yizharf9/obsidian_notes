
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
$$L(\lambda ; \mathbf x) = \prod_{i=1}^N \frac{e^{-\lambda} \cdot \lambda^{x_i}}{x_i !} = \frac{e^{-\lambda} \cdot \lambda^{\sum_{i=1}^Nx_i}}{\prod_{i=1}^Nx_i!}$$
- For convenience, we will take find the maximal argument of the logarithm of the likelihood function instead so first we will take the logarithm of the likelihood function :
$$\log L(\lambda ; \mathbf x)  = -\lambda + \log(\lambda)\cdot\sum_{i=1}^N x_i - log(\prod_{i=1}^N x_i!)$$
- To find the minimum of the likelihood function we will take the derivative and equate to 0 :
$$\frac{\partial \log L(\lambda;\mathbf x)}{\partial \lambda} = -1 + \frac1\lambda \sum_{i=1}^N x_i = 0 $$
$$\implies \lambda = \sum_{i=1}^Nx_i $$
$$\frac{\partial^2 \log L(\lambda;\mathbf x)}{\partial \lambda^2} =  -\frac1{\lambda^2} \sum_{i=1}^N x_i \lt 0 : \forall \lambda \in \mathbb R \implies \lambda_{max} = t(\mathbf x)  :=  \sum_{i=1}^Nx_i$$
- We have found the ML estimator of the and as expected we see that it is a function of the sufficient statistics we have found in previous subsection.

## Question 2

![[Pasted image 20260627001708.png]]

### a) + b) Find Sufficient Statistics of $\mu$

![[Pasted image 20260627001818.png]]

We will find the sufficient statistics for the estimation of $\mu$ from the measurements $\mathbf x$. We will perform the Neyman-Fisher Factorization of the joint-PDF of the measurements $\mathbf x$ :

$$f(\mathbf x ; \mu) = (2\sigma)^{-N} \cdot \prod_{i=1}^N \exp\left(-\frac{|x_i - \mu|}{\sigma}\right) = (2\sigma)^{-N} \cdot \exp\left(-\frac1\sigma\sum_{i=1}^N |x_i - \mu|\right)$$
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
```desmos-graph
bottom = -0.2
top = 1
left = -pi - 0.2
right = pi + 0.2
---
x = -\pi | dashed | red
x = \pi  | dashed | red

m=0
k= 10^{-1}
B=\sum_{n=0}^{15}\frac{\left(\frac{k^2}{4}\right)^n}{\left(n!\right)^2}

y=\frac{1}{2\pi B}e^{k\cos\left(x-m\right)}  \left\{-\pi\le x\le\pi\right\}


l=3
A=\sum_{n=0}^{15}\frac{\left(\frac{l^2}{4}\right)^n}{\left(n!\right)^2}

y=\frac{1}{2\pi A}e^{l\cos\left(x-m\right)}  \left\{-\pi\le x\le\pi\right\}
```

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
$$Bias(\hat\theta(\mathbf x)) = \mathbb E[\theta - \hat\theta_{ML}(\mathbf x)]$$
- We will calculate the Bias of each component separately :
$$\mathbb E[\hat\theta_{1,ML}(\mathbf x)] = \mathbb E[\underset{i=1...N}{min}{\set{x_i}}]$$
- To find the expected value we first need to find the distribution of the minimum of the random vector $\mathbf x$. We will do so by finding the joint CDF (cumulative distribution function) of the random variable $X_{min} := \underset{i=1...N}{min}{\set{x_i}}$ :
$$F_{X_{min}}(t) = \mathbb P(X_{min} \le t) = 1 - \mathbb P(X_{min} \ge t) =  1- \mathbb P\left(\bigcap_{i=1}^N \set{x_i \ge t} \right) = \dots $$
- We know that the measurements are statistically independent :
$$\implies \prod_{i=1}^N \mathbb P(x_i \ge t) = \prod_{i=1}^N \left[ \int_{\theta_1}^{t}\frac{dx}{\theta_2 - \theta_1} \right] = \prod_{i=1}^N \left[ \frac{t - \theta_1}{\theta_2 - \theta_1} \cdot \mathbb 1_{[\theta_1,\infty)}(t) \right] = \left(\frac{t - \theta_1}{\theta_2 - \theta_1}\right)^N \cdot \mathbb 1_{[\theta_1,\infty)}(t) $$
- We get the joint CDF of the random variable $X_{min}$ :
$$F_{X_{min}}(t) = 1 - \left(\frac{t - \theta_1}{\theta_2 - \theta_1}\right)^N \cdot \mathbb 1_{[\theta_1,\infty)}(t) $$
- To calculate the expected value of the random value we need the PDF. We will extract it by differentiating the CDF with respect to $t$ :
$$f_{X_{min}}(t) = \frac{d}{dt}F_{X_{min}}(t) = \frac{d}{dt}\left( 1 - \left(\frac{t - \theta_1}{\theta_2 - \theta_1}\right)^N \cdot \mathbb 1_{[\theta_1,\infty)}(t)  \right) = -\frac{d}{dt}\left(\left(\frac{t - \theta_1}{\theta_2 - \theta_1}\right)^N \cdot \mathbb 1_{[\theta_1,\infty)}(t)  \right)$$
- We differentiate the expression as a multiplication of functions :
$$\dots = $$
