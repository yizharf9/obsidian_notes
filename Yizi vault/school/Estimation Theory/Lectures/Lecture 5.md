
## Properties of estimators 

- **Unbiased :**
	1. Bayesian estimation :
		1. Wide sense - $\mathbb{E}[\hat\theta - \theta] = 0$ 
		2. Strict sense -  $\mathbb{E}[\hat\theta - \theta | \theta ] = 0 : \forall \theta \in \Omega_\theta$  
	2. Non-Bayesian estimation :
		1. Point-wise Unbiased - $\left.\mathbb{E}[\hat\theta - \theta]\right|_{\theta_0} = 0$ 
		2. Locally Unbiased - $\left.\mathbb{E}[\hat\theta - \theta]\right|_{\theta_0} = 0_{_{M\times M}}$  ; $\left.\frac{d}{d\theta}\mathbb{E}[\hat\theta - \theta]\right|_{\theta_0} = 0_{_{M\times M}}$ 
		3. Uniformly Unbiased -  $\left.\mathbb{E}[\hat\theta - \theta]\right|_{\theta_0} = 0 : \forall \theta \in \Omega$ 

```desmos-graph
left = 0
bottom = -0.2
---
a = 5
z(x) = x - a
y = z(x)^2
y = z(x)^3 | red

(a,0) | label: theta 0
```

**Efficient :** Uniformly Minimum Variance Unbiased Estimator (UMVUE) 
an unbiased estimator that attains  the CRLB

1. Bayesian estimation :
	1. Wide sense - $\mathbb{E}[\hat\theta - \theta] = 0$ 
	2. Strict sense -  $\mathbb{E}[\hat\theta - \theta | \theta ] = 0 : \forall \theta \in \Omega_\theta$  
2. Non-Bayesian estimation :
	1. Point-wise Unbiased - $\left.\mathbb{E}[\hat\theta - \theta]\right|_{\theta_0} = 0$ 
	2. Locally Unbiased - $\left.\mathbb{E}[\hat\theta - \theta]\right|_{\theta_0} = 0_{_{M\times M}}$  ; $\left.\frac{d}{d\theta}\mathbb{E}[\hat\theta - \theta]\right|_{\theta_0} = 0_{_{M\times M}}$ 
	3. Uniformly Unbiased -  $\left.\mathbb{E}[\hat\theta - \theta]\right|_{\theta_0} = 0 : \forall \theta \in \Omega$ 

**Asymptotically Efficient :** 

We will denote $\hat\theta^{(N)}$ as the estimator of $\theta$ based on the first $N$ i.i.d. data samples.
We define such an estimator as one that satisfies :

1. $$\lim_{N \to \infty} \mathbb{E}[\hat\theta^{(N)} - \theta] = 0 : \forall \theta \in \Omega_\theta$$
2. $$\lim_{N \to \infty} \mathbb{E}[Cov(\hat\theta^{(N)}) \cdot  CRLB^{-1}] = \mathbb{I}_M $$

> [!Example]
> $x_n = \theta + v_n : v_n \sim^{i.i.d.}\mathcal{N}(0,\sigma^2)$
> 
>$\hat\theta_{eff} = \frac{1}{N}\sum_{n=1}^{N}x_n \implies Var(\hat\theta_{eff}) = CRB_N = \frac{\sigma^2}{N}$ 
>
>$\hat\theta_{1} = \frac{1}{N/2}\sum_{n=1}^{N/2}x_n \implies Var(\hat\theta_{1}) = \frac{2\cdot \sigma^2}{N}$ 
>
>$\hat\theta_{2} = \frac{1}{N+1}\sum_{n=1}^{N/2}x_n = \frac{N}{N+1} \hat \theta_{eff} \implies Var(\hat\theta^{(N)}_2) = (\frac{N}{N+1})^2 Var(\hat\theta_{eff}) = \frac{N}{(N+1)^2} \cdot \sigma^2$
>
>We will examine Asymp. efficiency :
>
>$\lim_{N \to \infty} \mathbb{E}[\hat\theta^{(N)}_{2} - \theta] = \lim_{N \to \infty} \mathbb{E}[\frac{N}{N+1}\theta_{eff} - \theta] = 0$
>
>We Notice that we were able to diminish the variance of the efficient estimator by relaxing the estimator to be Asymp. Unbiased by adding a Asymp. zero bias:
>$Var(\hat\theta_{2}) = \frac{N}{(N+1)^2} \cdot \sigma^2 \lt \frac{\sigma^2}{N} = Var(\hat\theta_{eff})$

**Consistency :**

A consistent estimator is one that satisfies :
$$\lim_{N \to \infty} Prob(|\hat\theta^{(N)} - \theta | \le \varepsilon) = 1 : \forall \varepsilon \gt 0 \ ; \ m = 1 \dots M$$

**Sufficient (Not necessary) condition for consistency :**

1. $\lim_{N \to \infty} \mathbb{E}[\hat\theta^{(N)} - \theta]=0$
2. $\lim_{N \to \infty} Cov(\hat\theta^{(N)}) = 0$

We can show that using **Chebyshev inequality**...

**Proof :**
Chebyshev inequality : $$\mathbb{P}(\left|\hat\theta^{(N)} - \mathbb{E}[\hat\theta^{(N)}]\right|) \le \frac{Var(\hat\theta^{(N)})}{\varepsilon^2}$$
$$\implies \lim_{N \to \infty} Prob(|\hat\theta^{(N)} - \theta | \le \varepsilon) \le
\frac{Var(\hat\theta^{(N)})}{\varepsilon^2} = 0$$
$$\implies \lim_{N \to \infty} Prob(|\hat\theta^{(N)} - \theta | \le \varepsilon) =
\lim_{N \to \infty} 1 - Prob(|\hat\theta^{(N)} - \theta | \gt \varepsilon) = 1$$


> [!Example] 
> Given a R.V $\varphi$ with the following PDF :
> ```desmos-graph
> top = 0.5 
> bottom = -0.2 
> left = -5
> right = 5
> ---
> s = 0.5
> d = 4
> c = 1/(\pi)^0.5
> 
> y = 3/4 * c * e^{-x^2 / s^2} | blue
> y = 1/8 * c * e^{-(x-d)^2 / s^2} | red 
> y = 1/8 * c * e^{-(x+d)^2 / s^2} | red
> 
> x = s | dashed |  black
> x = -s | dashed | black
> 
>(d,0) | label: `\theta + \delta \cdot \theta \cdot N`
>(-d,0) | label: `\theta - \delta \cdot \theta \cdot N`
>
> ```
> 
> We notice that our condition does not hold yet :
> 1. The side lobes shrink in size so the probability of leaving the interval is 0 Asymp.
> 2. The variance of $\varphi$ grows to $\infty$ since the side lobes travel far away from the main lobe of the distribution ($\propto N^2$) faster than they shrink ($\propto N$).
> 
> $Var(\hat\theta^{(N)}) = Var(\hat\theta^{(N)} |\text{Main lobe})\cdot(1-\frac{\delta}{N}) + \underbrace{Var(\hat\theta^{(N)} |\text{Side lobe})\frac{\delta}{N}}_{\propto N^2} \underset{N \to \infty}{\longrightarrow} \infty$
> 

## Properties of the Cramer-Rao Lower Bound

We denote $I_{M}^{k}(\theta)$ the **fisher information Matrix** of the estimation of the parameter $\theta$ from the data samples $\underline{x}_k$. Assuming that $\left\{\underline{x}_k\right\}_{k=1}^{K}$ is a series of statistically independent vectors (not necessarily iid or of the same dimensions), 
therefore the FIM for estimating $\theta$ from the samples $\left\{ \underline{x}_k \right\}_{k=1^K}$ is given by :
$$I(\theta) = \sum_{k=1}^K{I^{(k)}(\theta)}$$
**Derivation :**
$$
\implies I(\theta) = 
-\mathbb{E} \left[
	\frac{\partial^2 \log f_\underline{x}(\underline{x} ; \theta)}
	{\partial \theta ^2}
\right] =
-\mathbb{E} \left[
	\frac{\partial^2 \log \prod_{k=1}^K f_{\underline{x}_k}(\underline{x}_k ; \theta)}
	{\partial \theta ^2}
\right] = $$$$
= \sum_{k=1}^K -\mathbb{E} 
\underbrace{\left[
	\frac{\partial^2 \log f_\underline{x}(\underline{x} ; \theta)}
	{\partial \theta ^2}
\right]}_{\text{FIM for estimation of $\theta$ from $\underline{x}_k$ }} =
\sum_{k=1}^K I^{(k)}(\theta)
$$
For the case where the samples $\{x_k\}_{k=1}^K$ are iid, under the same logical process as before we can derive the FIM as :

$$
I(\underline{\theta}) = \dots = K \cdot I(\theta_1)
$$


## Bayesian Cramer-Rao Lower Bound

This is an extension for the former definition of the CRLB for the Bayesian case.

$$\mathbb{E}\left[(\hat\theta-\theta) \cdot (\hat\theta-\theta) ^T \right] \succeq BCRB$$
The parameter is a R.V. : ${\theta \sim P_\theta}$ :

- We will use the **CS inequality** for the case of R.V.'s :
$$
\mathbb{E}[\underline z \cdot \underline z^T] \succeq 
\mathbb{E}[\underline z \cdot \underline y^T] \cdot 
\mathbb{E}[\underline y \cdot \underline y^T] \cdot 
\mathbb{E}[\underline y \cdot \underline z^T] 
$$
- Where we get equality :
$$\iff \underline z = c \cdot \underline y  \ : \ c \perp \underline y , x , \theta$$

- We denote :
$$\underline z := \underline{\hat\theta} - \theta $$
$$\implies \mathbb{E}[(\hat\theta - \theta) \cdot y ^T] 
$$$$\implies \mathbb{E}[\hat\theta \cdot y ^T] = \mathbb{E}_x\left[\mathbb{E}[\hat\theta \cdot y^T\ | \ x] \right]  = \mathbb{E}_x\left[\hat\theta \cdot\mathbb{E}[y^T\ | \ x] \right]  = \dots $$
$$
\mathbb{E}[y\ | \ x] = \mathbb{E}\left[\left.\frac{\partial^T\log f_{\underline x, \underline \theta }(\underline x , \underline\theta)}{\partial \underline\theta} \right|x\right] = \mathbb{E}\left[\left.\frac{\partial^T\log f_{\underline \theta | \underline x }(\underline \theta | \underline x )}{\partial \underline\theta} \right|x\right] + \underbrace{\cancel{\mathbb{E}\left[\left.\frac{\partial^T\log f_{\underline x}(\underline x)}{\partial \underline\theta} \right|x\right]}}_{...\perp \!\perp \theta} = 
$$
$$
\dots = \int_{\Omega_\theta}\frac{1}{f_{\underline \theta | \underline x}(\underline \theta | \underline x)} \cdot \frac{df_{\underline \theta | \underline x}(\underline \theta | \underline x)}{d\theta} \cdot f_{\underline \theta | \underline x}(\underline \theta | \underline x) \ d\theta
$$
