
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
#### The results of said simulation are as follows

##### Plotted as a function of $N$ :
###### $Bias(N,\theta_i)$  :
![[Pasted image 20260601195400.png]]

###### $Var(N,\theta_i)$  :
![[Pasted image 20260601195727.png]]

###### $MSE(N,\theta_i)$  :
![[Pasted image 20260601195839.png]]

##### Plotted as a function of $\theta$ :
###### $Bias(N_i,\theta)$  :
![[Pasted image 20260601200407.png]]

###### $Var(N_i,\theta)$  :
![[Pasted image 20260601200534.png]]

###### $MSE(N_i,\theta)$  :
![[Pasted image 20260601200631.png]]


We will calculate the CRLB from the definition :
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

> [!Fail] Result
>  We notice that we are not able to bring the score of the conditional distribution to the desired form and therefore we conclude that the CRLB is **unattainable** for our problem and in particular, to our estimator.
>  $$\implies Var(\hat\theta) \gt \mathcal{I}(\theta)^{-1} = CRLB$$

### c) Efficiency
![[Pasted image 20260601192740.png]]

Since by definition an efficient estimator is an unbiased estimator (not asymptotically unbiased...) our proposed estimator is **not efficient**!
### d) Efficiency
![[Pasted image 20260601192954.png]]

...However, the estimator I proposed is only **Asymptotically Unbiased**. That means that for any finite sample vector, no matter how large it is, the estimator is biased and the attainability condition for the **CRLB** that was stated earlier does not apply to it. 

For analysis purposes, We will derive the distribution of the estimator theoretically :
- First we want to evaluate the mean and bias of the estimator
$$Bias(\hat\theta,\theta) = \mathbb{E}[\hat\theta-\theta] = \mathbb{E}_{\underline x}[\hat\theta]-\theta$$
- To evaluate the following expected value we will use the MGF of a GWN vector :
$$\implies \mathbb{E}[\hat\theta] = \mathbb{E}[e^{\frac1N\sum_{i=1}^N{x_i}}] = \prod_{i=1}^N {\mathbb{E}[e^{\frac{x_i}{N}}]} = \prod_{i=1}^N {\left.M_{x_i}(t)\right|_{t=\frac1N}} = \prod_{i=1}^N{\left.e^{(t \cdot \mu_i + \frac12t^2 \cdot \sigma_i^2)}\right|_{t=\frac1{N}}} = $$$$ = \prod_{i=1}^N{e^{(\frac1N \cdot \log\theta + \frac1{2N^2} \cdot 1)}} = e^{\log\theta}\cdot e^{\frac1{2N}} = \theta\cdot e^{\frac1{2N}}$$
- We plug it back in the expression for the bias :
$$\implies Bias(\hat\theta,\theta) = \theta \cdot e^{\frac1N} - \theta = \theta \cdot (e^{\frac1{2N}} - 1)$$

> [!Success] Result
> We get a final expression for the bias of the estimator and we notice that it is **Asymptotically Unbiased :**
> $$Bias(\hat\theta, \theta) = \theta \cdot (e^{\frac1{2N}} - 1) \overset{N\to \infty}{\longrightarrow} 0$$ 
- Now we want to find the variance of the estimator :
$$Var(\hat\theta) = \mathbb{E}[ \hat\theta ^2] -  \mathbb{E}[ \hat\theta ]^2 = \dots$$
- We want to evaluate the second moment of the estimator so we will use the same MGF as before :
$$\mathbb{E}[\hat\theta^2] = \mathbb{E}[(e^{\frac1N \sum_{i=1}^N x_i})^2] = \mathbb{E}[e^{\frac2N \sum_{i=1}^N x_i}] = \prod_{i=1}^N {\left.M_{x_i}(t)\right|_{t=\frac2N}} = \prod_{i=1}^N{\left.e^{(t \cdot \mu_i + \frac12t^2 \cdot \sigma_i^2)}\right|_{t=\frac2N}} = $$
$$ = \prod_{i=1}^N{e^{(\frac2N \cdot \log\theta + \frac4{2N^2} \cdot 1)}} = e^{2\log\theta}\cdot e^{\frac4N} = \theta^2\cdot e^{\frac2N}$$
- Since we've previously calculated the mean, we plug in all terms to get the expression variance of the estimator :
$$\implies Var(\hat\theta) = \theta^2\cdot e^{\frac2N} - \left(\theta\cdot e^{\frac1{2N}}\right)^2 = \theta^2 \cdot (e^{\frac2N} - e^{\frac1N})$$

> [!Success] Result
> We get the expression variance of the estimator : 
> $$Var(\hat\theta) = \theta^2 \cdot (e^{\frac2N} - e^{\frac1N})$$

- We will use the **Talyor series of the exponent function** to evaluate the limit as the number of data samples goes to infinity :
$$e^x = 1 + x + \mathcal{o}(x^2) \implies Var(\hat\theta)\overset{a}{\approx} \theta^2 \cdot \left(1+\frac2N - (1+\frac1N)\right) = \frac{1}{N}\cdot \theta^2$$

> [!success] Result
> We can see that our estimator **attains the CRLB asymptotically :**
> $$Var(\hat\theta)\overset{a}{\approx} \frac{\theta^2}{N} $$
> $\implies$From this we can also conclude that the estimator is **asymptotically efficient** !

It is visible from our plots that this projection holds since the bias always exist even though it is asymp. zero. The variance attains the CRB for each plot, matching our earlier projections. The MSE follows the same trend as the variance since the bias squared term goes to zero and the MSE and the variance align with each other.
## Question 2

![[Pasted image 20260531110249.png]]

We are given the statistical model of the data samples :
$$\underline x := \begin{pmatrix} x_1 \\ \vdots \\ x_n \end{pmatrix} : \ \forall i \ne j \in \{1,...,n\} x_i \perp \! \perp x_j $$$$\implies \underline x \sim \mathcal{N}(\mathbb{1} \cdot\mu \ , \ \sigma^2 \cdot \mathbb{I}_n)$$
## a) Find CRB

![[Pasted image 20260531110313.png]]

We want to find the CRLB for the case of a GWN vector.

- We will find it based on the definition :
$$\underline \theta := [\mu,\sigma]^T \implies\left[ \underline {\underline{\mathcal{I}}}(\underline \theta) \right]_{i,j}= \mathbb{E}\left[ \frac{\partial\log f_{\underline x|\underline \theta}(\underline x)}{\partial\theta_i} \cdot \frac{\partial\log f_{\underline x|\underline \theta}(\underline x)}{\partial\theta_j} \right]$$
$$\log f_{\underline x | \underline \theta}(\underline x) = -\frac n2 (\log(2\pi)+\log(\sigma^2)) - \sum_{i=1}^{n}\frac{(x_i-\mu)^2}{2\sigma^2}$$
$$\overset{\frac{d}{d\mu}}{\longrightarrow} \quad \sum_{i=1}^{n}\frac{(x_i-\mu)}{\sigma^2} $$
$$\overset{\frac{d}{d\sigma^2}}{\longrightarrow} \quad -\frac n{2\sigma^2} + \frac 1{2\sigma^4}\sum_{i=1}^n {(x_i-\mu)^2}$$
- Calculating the off-diagonal terms :
$$[\mathcal{I}(\underline \theta)]_{1,2} = [\mathcal{I}(\underline \theta)]_{2,1} = \mathbb{E}\left[\left[ -\frac n{2\sigma^2} + \frac 1{2\sigma^4}\sum_{i=1}^n{(x_i-\mu)^2}\right] \cdot \sum_{i=1}^n(x_i -\mu) \right] = $$$$ = \frac1{2\sigma^2}\mathbb{E}\left[n\sum_{i=1}^n\underbrace{\cancel{(x_i -\mu)}}_{x_i \sim \mathcal{N}(\mu,\sigma^2)} + \sum_{i=1}^n \frac{(x_i -\mu)^3 }{\sigma^2} \right] = \frac1{2\sigma^4}\sum_{i=1}^n {\mathbb{E}\left[(x_i -\mu)^3\right]} =  $$
- To evaluate the expected value in question we will use the MGF of a joint-gaussian random vector :
$$\underline z := (\underline x - \mathbb{1}\cdot \mu) \sim \mathcal{N}(\underline 0 \ , \ \sigma^2 \cdot \mathbb{I}_n) \implies \mathbb{E}[z_i^n] = \begin{cases} 0 \quad\quad\quad\quad\quad : even \\ \sigma^{n}\cdot (n-1)!! : odd \end{cases} $$
$$\implies \mathbb{E}[(x_i - \mu)^3] = 0 = [\mathcal{I}(\underline \theta)]_{1,2} = [\mathcal{I}(\underline \theta)]_{2,1} $$

- Calculating the diagonal terms :
$$[\mathcal{I}(\underline \theta)]_{1,1} = -\mathbb{E}\left[ \frac{d}{d\mu}\left(\sum_{i=1}^{n}\frac{(x_i-\mu)}{\sigma^2}\right) \right] = \sum_{i=1}^n\frac{1}{\sigma^2} = \frac{n}{\sigma^2}$$

$$[\mathcal{I}(\underline \theta)]_{2,2} = -\mathbb{E}\left[ \frac{d}{d(\sigma^2)}\left(-\frac n{2\sigma^2} + \frac 1{2\sigma^4}\sum_{i=1}^n{(x_i-\mu)^2}\right) \right] = -\mathbb{E}\left[ \frac n{2\sigma^4} - \frac1{\sigma^6}\sum_{i=1}^n{(x_i-\mu)^2} \right] = $$$$ = -\frac n{2\sigma^4} + \frac1{\sigma^6}\sum_{i=1}^n\mathbb{E}\left[ {(x_i-\mu)^2} \right] = - \frac n{2\sigma^4} + \frac{n \cdot Var(x_i)}{\sigma^6} = -\frac n{2\sigma^4} + \frac{n \cdot \sigma^2}{\sigma^6} = \frac n{2\sigma^4}$$
- We get the FIM of the data samples :
$$\mathcal{I}(\underline\theta) = \begin{bmatrix} \frac n{\sigma^2} \quad 0 \\ 0 \quad \frac n{2\sigma^4} \end{bmatrix}$$

> [!success] Result
> We get the final expression for the CRB matrix :
>$$\mathcal{I}(\underline\theta)^{-1} = \begin{bmatrix} \frac {\sigma^2}{n} \quad 0\\ 0 \quad \frac {2\sigma^4}{n} \end{bmatrix}$$ 

