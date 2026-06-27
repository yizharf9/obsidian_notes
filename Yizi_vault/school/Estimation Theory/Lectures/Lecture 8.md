
## Sufficient statistic

$$f(\mathbf x, \mathbf \theta) , t(\mathbf x)$$
**Definition :**
$t(\mathbf x)$ is a sufficient statistic of estimation of $\mathbf \theta$ based on the measurements $\mathbf x$ if 
the distribution $f_{\mathbf x | \mathbf t}(\underline \alpha | \mathbf t = \tau ; \theta) \perp \! \perp \underline \theta$ 

$$\log f_{\mathbf x | \mathbf t}(\underline \alpha ;\tau ; \theta) = \underbrace{\log f_{\mathbf x | \mathbf t}(\underline \alpha | \tau ; \theta)}_{\text{we want this term to be 0}} + \underbrace{\log f_{\mathbf t}(\tau ; \theta)}_{\text{then this term will hold all the information}}$$

> [!Example]

$$x_n = \theta + v_n : n \in \{1...N\}$$
$$v_n \sim \mathcal{N}(0,\sigma^2)$$
$$t(\mathbf x) := \sum_{n=1}^{N}x_n$$
Is $t(\mathbf x)$ a sufficient statistic of estimating $\theta$?


> [!Note] Observation 
> 
>We consider the expansion of the PDF of the joint distribution $f_{\mathbf x, \mathbf t}$:
$$f_{\mathbf x , \mathbf t}(\underline \alpha ;\tau ; \theta) = \underbrace{f_{\mathbf t | \mathbf x}(\underline \alpha | \tau ; \theta)}_{\dots = \delta(\tau - t(\alpha))} \cdot f_{\mathbf t}(\tau ; \theta)$$
> we notice that $f_{\mathbf t | \mathbf x}$ is a deterministic function/curve in the $\alpha,\tau$ plane.
>$$f_{\mathbf x , \mathbf t}(\underline \alpha ;\tau ; \theta) = f_{\mathbf x | \mathbf t}(\mathbf\alpha|\mathbf \tau;\theta)\cdot f_\mathbf{t}(\tau;\theta)$$
>$$f_{\mathbf x , \mathbf t}(\underline \alpha ;\tau ; \theta) = \frac{f_{\mathbf x | \mathbf t}(\mathbf\alpha|\theta)}{f_\mathbf{t}(\tau;\theta)} \cdot \delta(\tau - \mathbf t (\alpha))$$

^75aa63


- Back to our problem:
$$
f_{\mathbf x , \mathbf t}(\underline \alpha ;\tau ; \theta) =
\frac{
	(2\pi\sigma^2)^{-\frac N2} \cdot \exp\left[-\frac{1}{2\sigma^2}(\sum_{n=1}^N\alpha_n^2 - 2\theta\sum_{n=1}^N\alpha_n^2 + N\theta^2) \right]
}{
	(2\pi\sigma^2)^{-\frac 12} \cdot \exp\left[-\frac{1}{2\sigma^2}\tau^2 - 2\tau +N\theta^2\right]
}
$$
- After canceling out all terms we get :
$$
f_{\mathbf x , \mathbf t}(\underline \alpha ;\tau ; \theta) = 
const. \cdot 
\exp\left[
	-\frac{1}{2\sigma^2} \sum_{n=1}^N \alpha_n^2
\right]
\exp\left[
	-\frac{1}{2\sigma^2}\frac{\tau^2}{N}
\right] \implies f_{\mathbf x , \mathbf t}(\underline \alpha ;\tau ; \theta) = f_{\mathbf x , \mathbf t}(\underline \alpha ;\tau)
$$
- We see that it is not a function of $\theta$!

### #Theorem Neyman-Fisher Factorization

$\mathbf t (\mathbf x)$ is a sufficient statistic for the estimation of $\theta$ from the measurements $\mathbf x$ $\iff$ $f(\mathbf x ; \theta ) = g(\mathbf t(\mathbf x) ; \theta) \cdot h(\mathbf x)$ 

**Proof :**
- $\implies$ :
	We use the [[school/Estimation Theory/Lectures/Lecture 8#^75aa63|Observation]] we performed earlier and substitute the factorization we assumed :
	$$f_{\mathbf x , \mathbf t}(\underline \alpha ;\tau ; \theta) = \frac{g(\mathbf t (\alpha);\theta) \cdot h(\alpha)}{\int_{\Omega_{\mathbf x}} f_\mathbf{x}(\alpha,\tau;\theta)d\alpha  } \cdot \delta(\tau - \mathbf t (\alpha))$$
$$f_{\mathbf x , \mathbf t}(\underline \alpha ;\tau ; \theta) = \frac{g(\mathbf t (\alpha);\theta) \cdot h(\alpha)}{\int_{\Omega_{\mathbf x}} \delta(\tau - \mathbf t (\alpha')) \cdot g(\mathbf t (\alpha');\theta) \cdot h(\alpha')d\alpha'  } \cdot \delta(\tau - \mathbf t (\alpha))$$
$$f_{\mathbf x , \mathbf t}(\underline \alpha ;\tau ; \theta) = 
\frac{\cancel{g(\tau;\theta)} \cdot h(\alpha)}
{\cancel{g(\tau;\theta)} \cdot \int_{\Omega_{\mathbf x}} \delta(\tau - \mathbf t (\alpha')) \cdot  h(\alpha')d\alpha'  } 
\cdot \delta(\tau - \mathbf t (\alpha)) \ne \text{function of }\theta$$


- $\impliedby$ 



### #Lemma 
If there exists an efficient estimator then it is a function of the sufficient statistics.

$$\hat\theta_{eff} = \theta + \mathcal {I}^{-1}(\theta) \cdot \left[
\frac{\partial^T\log g(\mathbf t (\mathbf x);\theta)}
{\partial \theta} +
\underbrace{\cancel{\frac{\partial^T\log h(\mathbf x)}
{\partial \theta}}}_{}
\right] = func(\mathbf t(\mathbf x) )
$$

### #Theorem Rao-Blackwell-Lehmann-Scheffe (RBLS)

If :
- $\tilde \theta(x)$ is an **unbiased estimator** of $\theta$ from the measurements $x$ 
- $t(x)$ is a sufficient statistics of $x$

Then the estimator $\hat\theta = \mathbb E(\tilde\theta(x) | t(x))$ is
- A **legit estimator** of $\theta$ - independent of $\theta$
- An **unbiased estimator** of $\theta$
- $Cov(\hat\theta(x)) \le Cov(\tilde\theta(x))$

**Proof :**

We want to show that :
$$\tilde \theta(t(x)) = \int_{\Omega_x} \tilde\theta(\alpha) \cdot f_{x|t}(\alpha|t \cancel{;\theta})d\alpha \ne func(\theta)$$
1. We show that it is unbiased :
$$\mathbb E [\hat \theta] = 
\int_{\Omega_x} \int_{\Omega_\tau} \tilde\theta(\alpha) \cdot f_{x|t}(\alpha|\tau)d\alpha \cdot f_{t}(\tau;\theta)d\tau =
\int_{\Omega_x}\tilde\theta(\alpha)  \underbrace{\int_{\Omega_\tau} f_{x|t}(\alpha|\tau)d\tau}_{= f_x(\alpha;\theta)} \cdot f_{t}(\tau;\theta)d\alpha =
\mathbb E [\tilde \theta(\alpha)]
$$
$$\mathbb E [\hat\theta(\alpha) - \theta] = \mathbb E [\tilde\theta(\alpha) - \theta] $$

2. We show the property of the covariance :
$$
Cov(\tilde\theta) - Cov(\hat\theta) = 
\mathbb E\left[(\tilde\theta - \mathbb E[\tilde \theta] + \hat\theta - \hat\theta )^2\right] - Cov(\hat \theta) = $$$$
= \mathbb E\left[(\tilde\theta - \hat\theta )^2\right] + 
2\mathbb E\left[(\hat\theta - \mathbb E [\tilde\theta] )^2\right] +
\mathbb E [\hat\theta] 
- Cov(\hat \theta) = 
$$


### Complete Sufficient statistics

**Definition :**
A sufficient statistics is called complete if there exists only a single function $g$ for which :
$$\mathbb E [g(t)] = \theta \ : \ \forall \theta \in \Omega_\theta$$
We would like to use a complete sufficient statistics to find a Uniform Minimum Variance Unbiased Estimator (UMVUE).