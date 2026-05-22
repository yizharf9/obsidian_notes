
## Question 7

![[Pasted image 20260521195742.png]]
![[Pasted image 20260521195754.png]]

### a) Find optimal estimator

We want to find the optimal estimator in the sense of the cost function defined as :
$$
C(\hat\theta, \theta) =  e^{\alpha(\hat\theta - \theta)} - \alpha(\hat\theta - \theta) - 1
: \alpha \in \mathbb{R}
$$
Which is called the **LINEX** cost function (linear exponential cost function).

- We will find the estimator based on the definition :
$$
\hat\theta_{opt}(\underline x) = 
\underset{\theta\in \mathbb{R}}{argmin}
\left\{
\mathbb{E}[C(\theta,\hat\theta) | \underline x]
\right\}
$$
- We expand the expected cost and evaluate each term separately :
$$
\mathbb{E}[C(\theta,\hat\theta) | \underline x] = 
\mathbb{E}[e^{\alpha \hat\theta}| \underline x]\cdot 
\mathbb{E}[e^{-\alpha\theta}| \underline x] -
\alpha\ \cdot \mathbb{E}[\hat\theta| \underline x] +
\alpha\ \cdot \mathbb{E}[\theta| \underline x] - 1 = 
$$
- $\hat \theta | \underline{x}$ is deterministic so we plug that in :
$$
\mathbb{E}[C(\theta,\hat\theta) | \underline x] = 
e^{\alpha \hat\theta} \cdot 
\mathbb{E}[e^{-\alpha\theta}| \underline x] -
\alpha\ \cdot \hat\theta + 
\alpha\ \cdot \mathbb{E}[\theta| \underline x] - 1
$$
- To find the argument that minimizes the cost we differentiate :
$$
\overset{\frac{d}{d\hat\theta}}{\longrightarrow} 
\alpha \cdot e^{\alpha \hat\theta} \cdot 
\mathbb{E}[e^{-\alpha\theta}| \underline x] -
\alpha\ + 
\cancel{\alpha\ \cdot \mathbb{E}[\theta| \underline x]} - \cancel{1} = 
\alpha \cdot e^{\alpha \hat\theta} - \alpha\
$$
- We equate to 0 and find the argument :
$$
\alpha \cdot e^{\alpha \hat\theta} \cdot \mathbb{E}[e^{-\alpha\theta}| \underline x] - \alpha = 0
\implies 
e^{\alpha \hat\theta} = \frac{1}{\mathbb{E}[e^{-\alpha\theta}| \underline x]}
$$
$$\implies 
\hat\theta \cdot \alpha  = \ln
\left(
\frac{1}{\mathbb{E}[e^{-\alpha\theta}| \underline x]}
\right)
= -\ln
\left(
\mathbb{E}[e^{-\alpha\theta}| \underline x]
\right)$$

> [!success] Result
> We get the final expression for the optimal estimator
> $$ \hat \theta_{opt}(\underline x) = - \frac{1}{\alpha}\ln\left(\mathbb{E}[e^{-\alpha\theta}| \underline x]\right)$$

### b) Find MMSE estimator for a single data sample 

We are given the posterior distribution of the parameter given a data sample :
$$
\theta | x \sim \mathcal{N}(x,1)
$$
We will derive both the MMSE estimator and the optimal estimator and compare the 2.

#### MMSE Estimator

- We will find the MMSE estimator according to definition :
$$
\hat \theta_{MMSE}(x) = \mathbb{E}[\theta|x]
$$
 - Since we know the posterior distribution, this is pretty straight forward :
$$
\theta | x \sim \mathcal{N}(x,1) \implies 
\hat \theta_{MMSE}(x) = x
$$

#### Optimal Estimator

- We will use the former expression derived for the optimal estimator in the LINEX sense :
$$ 
\hat \theta_{opt}(x) = - \frac{1}{\alpha}\ln\left(\mathbb{E}[e^{-\alpha\theta}| x]\right)
$$
- We will first find the target expected value term to later substitute it back into the expression for the estimator.
- To evaluate this term we will use the moment generating function of the posterior distribution defined as :
$$
M_X(t) = \mathbb{E}[e^{Xt}]
$$
- We will use the derivation for the moment generating function of a gaussian R.V. :
$$
X \sim \mathcal{N}(\mu,\sigma^2) \implies M_X(t) = 
\mathbb{E}[e^{Xt}] = 
\exp({\mu \cdot t + \frac{1}{2} \sigma^2\cdot t^2})
$$
- Since the posterior distribution of the parameter is gaussian, we can safely state that the target expected value is equivalent to evaluating the moment generating function of the posterior  at $t = -\alpha$ : 
$$
\left. M_{\theta|x}(t) \right|_{t = -\alpha} = 
\mathbb{E}[e^{-\alpha\theta}| x] = 
\exp({x \cdot (-\alpha) + \frac{1}{2} \cdot 1 \cdot (-\alpha)^2})
$$
- We substitute this expression back in the optimal LINEX estimator expression :
$$
\hat\theta_{opt}(x) = -\frac{1}{\alpha} \cdot \ln(\exp({-\alpha x + \frac{1}{2} \alpha^2})) =
-\frac{1}{\alpha} \cdot [-\alpha x + \frac{1}{2}\alpha^2] =
x - \frac{\alpha}{2}
$$

- We get the final term for the optimal estimator in the sense of the LINEX cost :
$$
\implies \hat \theta_{opt}(x) = x - \frac{\alpha}{2}
$$

> [!abstract] Comparison
> We notice that the LINEX optimal estimator has a linear relationship with the MMSE estimator:
> $$\implies \hat \theta_{opt}(x) = \hat\theta_{MMSE}(x) - \frac{\alpha}{2}$$
> The LINEX estimator has a relative bias with respect to the MMSE estimator.
> 
> That makes sense since the LINEX cost punishes over estimation more than under estimation do to the exponential term in the cost function !

### c) Repeating a) for new cost function

We are presented with a new cost function :
$$
C(\hat\theta, \theta) =  e^{\alpha|\hat\theta - \theta|} - \alpha|\hat\theta - \theta| - 1
: \alpha \in \mathbb{R}
$$
We cannot use the moment generating function for this part since it does not answer the definition. We will have to define the optimal estimator by explicitly stating the integral accordingly.
- We first write the expression for the expected cost :
$$
\mathbb{E}[C(\hat\theta,\theta)] = 
\int_{\mathbb{R}} \left( e^{\alpha|\hat{\theta} - \theta|} - \alpha|\hat{\theta} - \theta| - 1 \right) f(\theta | \mathbf{x}) \, d\theta
$$
- We separate the integral to greater than and lower than $\hat\theta$ values to handle the absolute value :
$$
\dots = \int_{-\infty}^{\hat{\theta}} \left( e^{\alpha(\hat{\theta} - \theta)} - \alpha(\hat{\theta} - \theta) - 1 \right) f(\theta | \mathbf{x}) \, d\theta \quad + \int_{\hat{\theta}}^{\infty} \left( e^{\alpha(\theta - \hat{\theta})} - \alpha(\theta - \hat{\theta}) - 1 \right) f(\theta | \mathbf{x}) \, d\theta
$$
- As of before, we take the derivative with respect to $\hat\theta$  and evaluate the integral at the boundries according to the **leibniz's rule of integration**:
$$
\overset{\frac{d}{d\hat\theta}}{\longrightarrow} 
\int_{-\infty}^{\hat{\theta}} \frac{d}{d\hat\theta}\left( e^{\alpha(\hat{\theta} - \theta)} - \alpha(\hat{\theta} - \theta) - 1 \right) f(\theta | \mathbf{x}) \, d\theta \quad + 
\int_{\hat{\theta}}^{\infty} \frac{d}{d\hat\theta}\left( e^{\alpha(\theta - \hat{\theta})} - \alpha(\theta - \hat{\theta}) - 1 \right) f(\theta | \mathbf{x}) \, d\theta =
$$
$$
\dots = \int_{-\infty}^{\hat{\theta}} \alpha\left( e^{\alpha(\hat{\theta} - \theta)} - 1 \right) f(\theta | \mathbf{x}) \, d\theta + 
\int_{\hat{\theta}}^{\infty} \alpha\left( -e^{\alpha(\theta - \hat{\theta})} + 1 \right) f(\theta | \mathbf{x}) \, d\theta = 0 
$$
- We compare to 0 to find the minimum argument. We notice that we can't find a closed form for that argument without previously knowing the distribution of the posterior :
$$
\implies 
\hat\theta_{opt}(x) = \hat\theta : 
\int_{-\infty}^{\hat{\theta}} \alpha\left( e^{\alpha(\hat{\theta} - \theta)} - 1 \right) f(\theta | \mathbf{x}) \, d\theta =
\int_{\hat{\theta}}^{\infty} \alpha\left( -e^{\alpha(\theta - \hat{\theta})} + 1 \right) f(\theta | \mathbf{x}) \, d\theta
$$
> [!info] Comment 
> We can define a function of the difference between the 2 integrals.
> Suppose that the expected value in question converges, we can define a function of the difference between the integrals.
> Such a function will be valued some constant at infinity and minus that constant at -infinity so we can assume that it is zero somewhere on the real number line. 
> That value will be our estimator!

### d) Finding optimal estimator for new cost function 

In contrast to previous subsection, this cost function is **Symmetric**! 
For a gaussian posterior, this gives us the advantage to use a theorem we proved in class.

- We want to use the following Theorem we proved in class :
	_If the posterior PDF is symmetric around the conditional expected value 
	$\implies \hat{\theta}_{MMSE}$  minimizes every expected value of a symmetric and convex cost function._

- To use it we need to meet the following requirements : 
	1. Symmetric posterior : $f_{\underline{\theta}|\underline{x}}(\underline{\varphi}|\underline{x}) = f_{\underline{\theta}|\underline{x}}(\underline{-\varphi}|\underline{x})$ $\implies$ gaussian
	2. Symmetric cost function :  $\bar{C}(\underline{\varepsilon}) = \bar{C}(-\underline{\varepsilon})$ $\implies$ contains absolute value
	3. Convex Cost function : $\bar{C}(\cdot) -$ convex $\implies$ sum of a exp. , linear and constant terms is a convex term

- Since we meet all the requirements, we can safely claim that the MMSE estimator is the estimator that minimizes the new cost function.


> [!success] Result
> We get the final expression for the optimal estimator :
> $$\hat \theta_{MMSE}(x) = x$$


## Question 9

![[Pasted image 20260521220634.png]]

### a) Find MAP Estimator 

We will find that MAP estimator by definition :

$$
\hat a_{MAP}(x) = \underset{a\in \mathbb{R}}{argmax}
\left\{
f_{a | x} (a | x)
\right\} =
\underset{a\in \mathbb{R}}{argmax}
\left\{
f_{x | a} (x | a) \cdot f_{a} (a)
\right\} 
$$
- We can instead look at an equivalent statement :
$$
\hat a_{MAP}(x) = 
\underset{a\in \mathbb{R}}{argmin}
\left\{
-\ln(f_{x | a} (x | a) \cdot f_{a} (a))
\right\} 
$$
- We can derive the distribution of $x|a$ under the assumption of independent gaussian distributions of all R.V. .
- Since that for a fixed value of a, $x$ is a linear combination of independent gaussian R.V. s it is a gaussian R.V. We will find it's first and second moments :
$$
\mathbb{E}[x|a] = 
\mathbb{E}[ab+n|a] = 
a \cdot \mathbb{E}[b|a] + \mathbb{E}[n|a] = 0
$$
$$
Var(x|a) = 
\mathbb{E}[x^2|a] = 
\mathbb{E}[(ab+n)^2|a] = 
a^2 + \mathbb{E}[(b)^2|a] +
\cancel{2 a \mathbb{E}[abn|a]} +
\mathbb{E}[n^2|a] =
a^2 \cdot \sigma_b^2 + \sigma^2_n
$$
$$\implies x|a \sim \mathcal{N}(0, a^2\sigma_b^2 + \sigma_n^2)$$
- We will can  use bayes theorem to justify the following relationship :
$$f(a|x) \propto f_{x | a} (x | a) \cdot f_{a} (a) = \left[ 
\frac{1}{\sqrt{2\pi(a^2\sigma_b^2 + \sigma_n^2)}} 
\exp\left(-\frac{x^2}{2(a^2\sigma_b^2 + \sigma_n^2)}\right) 
\right] 
\left[ 
\frac{1}{\sqrt{2\pi\sigma_a^2}} 
\exp\left(-\frac{a^2}{2\sigma_a^2}\right) 
\right]$$$$\implies f(a|x) \propto \left[ 
\exp\left(-\frac{x^2}{2(a^2\sigma_b^2 + \sigma_n^2)}\right) 
\right] 
\left[ 
\exp\left(-\frac{a^2}{2\sigma_a^2}\right) 
\right]$$
- We take the minus of the logarithm to find the argument that minimizes both sides :
$$
\overset{-\ln(\cdot)}{\longrightarrow} \quad \frac{1}{2}\ln(a^2\sigma_b^2 + \sigma_n^2) + \frac{x^2}{2(a^2\sigma_b^2 + \sigma_n^2)} + \frac{a^2}{2\sigma_a^2}$$
- We take the derivative with respect to the parameter $a$ and compare to 0 :
$$
\overset{\frac{d}{da}}{\longrightarrow} \quad 
\frac{a\sigma_b^2}{a^2\sigma_b^2 + 
\sigma_n^2} - \frac{x^2 a\sigma_b^2}{(a^2\sigma_b^2 + \sigma_n^2)^2} + \frac{a}{\sigma_a^2} = 0
$$
$$\implies 
a \left[
\frac{\sigma_b^2}{a^2\sigma_b^2 + 
\sigma_n^2} - \frac{x^2 \sigma_b^2}{(a^2\sigma_b^2 + \sigma_n^2)^2} + \frac{1}{\sigma_a^2} 
\right]
= 0 \implies 
\begin{cases}
a = 0 \\
a = \pm \sqrt{ \frac{\sigma_a^2}{2} \left[ -1 + \sqrt{1 + \frac{4x^2}{\sigma_a^2\sigma_b^2}} \right] - \frac{\sigma_n^2}{\sigma_b^2} } \\
\end{cases}$$

