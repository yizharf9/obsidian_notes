
## Question 1
![[Pasted image 20260529171128.png]]
### a) Find Estimator
![[Pasted image 20260529171139.png]]

Since $\theta$ is a deterministic parameter we will prefer using ML estimator.

- We will derive the expression of the ML estimator by definition :
$$\hat\theta_{ML}(\underline x) = \underset{\theta\in\Omega_\theta}{argmax}\left\{f_{\underline x | \theta}(\underline x | \theta)\right\}$$
- For that purpose, we will find the conditional distribution of $\underline x | \theta$ :
$$x_n = \log\theta + w_n : w_n \overset{i.i.d}{\sim} \mathcal{N}(0,1)$$
$$\underline x^{(N)} {\sim} \mathcal{N}(\mathbb{1}_N\cdot \log\theta,I_N) \ : \ \mathbb{1}_N = \begin{pmatrix}1 \\ 1 \\ \vdots \\ 1\end{pmatrix} \in \mathbb{R}^N$$
- We can derive the conditional joint PDF of the samples :
$$f_{\underline x | \theta}(\underline \alpha ; \theta) = \prod_{i=1}^N {f_{x_i | \theta}(\alpha_i ; \theta)} = \prod_{i=1}^N {\frac{1}{\sqrt{2\pi}} \cdot e^{-\frac{(x_i - \log\theta)^2}{2}}} = (2\pi)^{-\frac{N}{2}}\cdot \exp\left[ -\frac{1}{2}\sum_{i=1}^{N}(x_i - \log\theta)^2 \right] $$
- We notice that for convenience, we can find the max argument of the $\ln$ of the conditional joint distribution without changing our goal :
$$\hat\theta_{ML}(\underline x) = \underset{\theta\in\Omega_\theta}{argmax}\left\{f_{\underline x | \theta}(\underline x | \theta)\right\} =  \underset{\theta\in\Omega_\theta}{argmax}\left\{\ln f_{\underline x | \theta}(\underline x | \theta)\right\}$$
$$\dots = \ln\left[(2\pi)^{-\frac{N}{2}}\cdot \exp\left[ -\frac{1}{2}\sum_{i=1}^{N}(x_i - \log\theta)^2 \right]\right] = -\frac{N}{2}\ln(2\pi) + \left[-\frac{1}{2}\sum_{i=1}^{N}(x_i - \log\theta)^2\right]$$
- We will find the max argument by taking the derivative and comparing to 0 :
$$\overset{\frac{d}{d\theta}}{\longrightarrow} -\cancel{\frac{1}{2}}\sum_{i=1}^N{\cancel{2}\cdot(x_i - \log\theta)\cdot (-\frac1\theta)} = \cancel{-\frac1\theta} \left[N\cdot \log\theta - \sum_{i=1}^{N} x_i\right] = 0 $$
 $$\theta \gt 0 \implies N\log \hat\theta = \sum_{i=1}^N x_i \implies \hat\theta = \exp\left[{\frac1N \cdot \sum _{i=1}^N}\right]$$
 
> [!success] Result
> We get the final derivation of the MLE :
> 
> $$\hat\theta_{ML}\left(\underline x^{(N)}\right) = \exp\left[{\frac1N \cdot \sum _{i=1}^N}\right] = \exp(\bar x)$$


### b) Analyzing The Results
![[Pasted image 20260529192232.png]]

For analysis purposes, we want to check if our estimator is unbiased and therefore to know if the CRLB would even possibly apply to our problem.

- We will calculate the CRLB from the definition :
$$Var(\hat \theta) \ge \mathcal{I}(\theta)^{-1} = CRLB$$
- We will derive the Fisher-Information from the definition. Since there are $N$ i.id. samples, we can take the Fisher-Information of a single sample and multiply it by $N$ :
$$\forall n,m \in \{1\dots N\} \ : \ x_n \perp \!\perp x_m \implies \mathcal{I}(\theta) = N \cdot \mathbb{E}\left[\left(\frac{\partial\log f_{x_n | \theta}(x_n ; \theta)}{\partial\theta}\right)^2\right]$$
$$\log f_{x_n | \theta}(x_n ; \theta) = \log\left[ (2\pi)^{-\frac12} \cdot \exp\left(-\frac{(x_n - \log\theta)^2}{2}\right) \right] = -\frac 12 \log(2\pi) -\frac{(x_n - \log\theta)^2}{2}$$
$$\overset{\frac \partial {\partial\theta}}{\longrightarrow} \cancel{-}\cancel{\frac12}(x_n - \log\theta) \cdot \cancel{2} \cdot (\cancel{-}\frac1\theta) =  (x_n - \log\theta)\cdot \frac1\theta$$
$$N \cdot \mathbb{E}\left[\left(\frac{\partial\log f_{x_n | \theta}(x_n ; \theta)}{\partial\theta}\right)^2\right] = N \cdot \mathbb{E}\left[\left.(x_n - \log\theta)^2\cdot \frac1{\theta^2}\right| \theta\right] = N \cdot \frac1{\theta^2} \cdot \mathbb{E}[(x_n - \log\theta)^2]$$
- We can notice that by definition, the expected value in question is the Variance of the conditional distribution $x_n | \theta$ which is given to be 1 :
$$\dots = N \cdot \frac1{\theta^2} Var(x_n|\theta) = N\cdot \frac1{\theta^2}$$
- We get the final expression for the Fisher-Information :
$$\implies \mathcal{I}(\theta) = \frac{N}{\theta^2}$$

> [!success] Result
> And finally, we get the final expression for the CRLB :
>$$CRLB = \mathcal{I}(\theta)^{-1} = \frac{\theta^2}{N}$$

Next, we want to check the condition for which the CRLB can be attained. As we proved in class, the conditional PDF must satisfy :
$$\frac{\partial\log f_{\underline x | \theta}(\underline x ; \theta)}{\partial\theta} = c(\theta)\cdot (\varphi(x)- \theta)$$
- We will expand the terms for our problem (relying on earlier derivation...) to check if the condition holds :
$$\frac{\partial\log f_{\underline x | \theta}(\underline x ; \theta)}{\partial\theta} = \dots = \underbrace{\frac N\theta}_{:=c(\theta)} \cdot \left[\underbrace{\frac1N\sum_{i=1}^Nx_i}_{:=\varphi(x)} -\underbrace{\log\theta}_{\ne\theta}\right] $$
- There is no possible way to bring the $\log\theta$ term to the form of $\theta$ without breaking the definition for the rest of the terms...

> [!success] Result
>  We notice that we are not able to bring the score of the conditional distribution to the desired form and therefore we conclude that the CRLB is **unattainable** for our problem and in particular, to our estimator.
>  $$\implies Var(\hat\theta) \gt \mathcal{I}(\theta)^{-1} = CRLB$$


