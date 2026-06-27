
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
