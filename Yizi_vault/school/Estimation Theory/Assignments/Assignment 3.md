
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
$$\underline x := \begin{pmatrix} x_1 \\ \vdots \\ x_n \end{pmatrix} : \ \forall i \ne j \in \{1,...,n\}  : x_i \perp \! \perp x_j $$$$\implies \underline x \sim \mathcal{N}(\mathbb{1} \cdot\mu \ , \ \sigma^2 \cdot \mathbb{I}_n)$$
### a) + b) Find CRB and 

![[Pasted image 20260602194129.png]]

We want to find the CRLB for the case of a GWN vector.

- We will find it based on the definition :
$$\underline \theta := [\mu,\sigma^2]^T \implies\left[ \underline {\underline{\mathcal{I}}}(\underline \theta) \right]_{i,j}= \mathbb{E}\left[ \frac{\partial\log f_{\underline x|\underline \theta}(\underline x)}{\partial\theta_i} \cdot \frac{\partial\log f_{\underline x|\underline \theta}(\underline x)}{\partial\theta_j} \right]$$
$$\log f_{\underline x | \underline \theta}(\underline x) = -\frac n2 (\log(2\pi)+\log(\sigma^2)) - \sum_{i=1}^{n}\frac{(x_i-\mu)^2}{2\sigma^2}$$
$$\overset{\frac{d}{d\mu}}{\longrightarrow} \quad \sum_{i=1}^{n}\frac{(x_i-\mu)}{\sigma^2} $$
$$\overset{\frac{d}{d\sigma^2}}{\longrightarrow} \quad -\frac n{2\sigma^2} + \frac 1{2\sigma^4}\sum_{i=1}^n {(x_i-\mu)^2}$$
- Calculating the off-diagonal terms :
$$[\mathcal{I}(\underline \theta)]_{1,2} = [\mathcal{I}(\underline \theta)]_{2,1} = \mathbb{E}\left[\left[ -\frac n{2\sigma^2} + \frac 1{2\sigma^4}\sum_{i=1}^n{(x_i-\mu)^2}\right] \cdot \sum_{i=1}^n(x_i -\mu) \right] = $$$$ = \frac1{2\sigma^2}\mathbb{E}\left[n\sum_{i=1}^n\underbrace{\cancel{(x_i -\mu)}}_{x_i \sim \mathcal{N}(\mu,\sigma^2)} + \sum_{i=1}^n \frac{(x_i -\mu)^3 }{\sigma^2} \right] = \frac1{2\sigma^4}\sum_{i=1}^n {\mathbb{E}\left[(x_i -\mu)^3\right]} =  $$
- To evaluate the expected value in question we will use the MGF of a joint-gaussian random vector :
$$\underline z := (\underline x - \mathbb{1}\cdot \mu) \sim \mathcal{N}(\underline 0 \ , \ \sigma^2 \cdot \mathbb{I}_n) \implies \mathbb{E}[z_i^n] = \begin{cases} 0 \quad\quad\quad\quad\quad : odd \\ \sigma^{n}\cdot (n-1)!! : even \end{cases} $$
$$\implies \mathbb{E}[(x_i - \mu)^3] = 0 = [\mathcal{I}(\underline \theta)]_{1,2} = [\mathcal{I}(\underline \theta)]_{2,1} $$

- Calculating the diagonal terms :
$$[\mathcal{I}(\underline \theta)]_{1,1} = -\mathbb{E}\left[ \frac{d}{d\mu}\left(\sum_{i=1}^{n}\frac{(x_i-\mu)}{\sigma^2}\right) \right] = \sum_{i=1}^n\frac{1}{\sigma^2} = \frac{n}{\sigma^2}$$

$$[\mathcal{I}(\underline \theta)]_{2,2} = -\mathbb{E}\left[ \frac{d}{d(\sigma^2)}\left(-\frac n{2\sigma^2} + \frac 1{2\sigma^4}\sum_{i=1}^n{(x_i-\mu)^2}\right) \right] = -\mathbb{E}\left[ \frac n{2\sigma^4} - \frac1{\sigma^6}\sum_{i=1}^n{(x_i-\mu)^2} \right] = $$$$ = -\frac n{2\sigma^4} + \frac1{\sigma^6}\sum_{i=1}^n\mathbb{E}\left[ {(x_i-\mu)^2} \right] = - \frac n{2\sigma^4} + \frac{n \cdot Var(x_i)}{\sigma^6} = -\frac n{2\sigma^4} + \frac{n \cdot \sigma^2}{\sigma^6} = \frac n{2\sigma^4}$$
- We get the FIM of the data samples :
$$\mathcal{I}(\underline\theta) = \begin{bmatrix} \frac n{\sigma^2} \quad 0 \\ 0 \quad \frac n{2\sigma^4} \end{bmatrix}$$

> [!success] Result
> We get the final expression for the CRB matrix :
>$$\mathcal{I}(\underline\theta)^{-1} = \begin{bmatrix} \frac {\sigma^2}{n} \quad 0\\ 0 \quad \frac {2\sigma^4}{n} \end{bmatrix}$$ 
>We can see that the off-diagonal terms are 0, then there is no coupling between the 2 which makes sense since the first and second moments of a distribution are independent of each other.

### c) Variance Estimators bias :

![[Pasted image 20260602154241.png]]

- We will calculate the bias of the estimator :
$$\mathbb{E}[\hat \sigma^2] = \mathbb{E}\left[ \frac1N\sum_{i=1}^N (x_i-\bar x)^2 \right] =  \sum_{i=1}^N \mathbb{E}\left[(x_i-\bar x)^2 \right] $$
$$\implies \mathbb{E}\left[ (x_i - \bar x)^2\right] = \mathbb{E}\left[ x_i^2 \right] - 2 \cdot \mathbb{E}[x_i \cdot \bar x] + \mathbb{E}[\bar x^2] $$

- We take advantage of the fact that : $\mathbb{E}[x^2] = Var(x) + \mathbb{E}[x]^2$ 
$$  \forall k \ne i : \mathbb{E}[x_k \cdot x_i] = \begin{cases} \mu^2 \quad\quad\quad : i\ne k \\ \sigma^2 +\mu^2 \quad :i=k \end{cases} $$
$$\mathbb{E}[x_i^2] = \sigma^2 + \mu^2$$
$$\mathbb{E}[x_i \cdot \bar x] = \frac1N \sum_{k=1}^N \mathbb{E}[x_i x_k] = \frac1N (\sigma^2 + \mu^2 + (N-1)\cdot \mu^2) = \frac1N \sigma^2 + \mu^2 $$
$$\mathbb{E}[\bar x ^2] = \frac1{N^2} \sum_{k=1}^N \sum_{m=1}^N \mathbb{E}[x_k x_m]  = \frac{1}{N^2} \cdot \left[ N\cdot (\sigma^2 + \mu^2) + N(N-1)\cdot\mu^2 \right] = \frac1N \cdot \sigma^2 + \mu^2 $$
$$\implies \mathbb{E}[(x_i-\bar x)^2] = \sigma^2 + \mu^2 - 2(\frac1N \cdot \sigma^2 + \mu^2) + \frac1N \cdot \sigma^2 + \mu^2 = \sigma^2 (1- \frac1N)$$
$$\implies \mathbb{E}[\hat\sigma^2] = \frac1N \sum_{i=1}^N\sigma^2 (1- \frac1N) = \frac1N \cdot N \cdot \sigma^2 (1- \frac1N) = \sigma^2 (1- \frac1N)$$

> [!success] Result
> We see that the bias of the estimator is 0 only asymptotically, meaning that it is not unbiased:
>$$Bias(\hat\sigma^2,\sigma^2) = \mathbb{E}[\hat\sigma^2 - \sigma^2] = \sigma^2(1-\frac1N) - \sigma^2 = -\frac{\sigma^2}{N} \overset{N \to \infty}{\longrightarrow} 0$$ 

We want to find the correction term make the estimator unbiased. We notice that we can multiply the original estimator by a function of the number of samples and remove the bias :

- We propose the following estimator $\tilde\sigma^2$ :
$$\tilde\sigma^2 : = \frac{1}{1-\frac1N} \hat\sigma^2 = \frac{1}{1-\frac1N} \frac1N \sum_{i=1}^N(x_i - \bar x)^2 = \frac{1}{N-1}\sum_{i=1}^N(x_i - \bar x)^2$$
- We notice that the expected value of the estimator comes out to be the target parameter :
$$\implies \mathbb{E}[\tilde\sigma^2] = \frac{1}{1-\frac1N}\mathbb{E}[\hat\sigma^2] = \cancel{\frac{1}{1-\frac1N}} \cdot \sigma^2\cancel{(1 - \frac1N)} = \sigma^2$$

> [!success] Result
> We see that the new estimator we propose is unbiased :
> $$\tilde\sigma^2 = \frac{1}{N-1}\sum_{i=1}^N(x_i - \bar x)^2 \implies \mathbb{E}[\tilde\sigma^2] = \sigma^2$$

### d) Variance of Proposed Estimator
![[Pasted image 20260602162006.png]]

We will calculate the variance of the estimator and check if it achieves the CRB.
$$Var(\tilde\sigma^2) = \mathbb{E}[(\tilde \sigma^2)^2] - \mathbb{E}[\tilde \sigma^2]^2$$
$$\mathbb{E}[(\tilde\sigma^2)^2] = \mathbb{E}\left[ \frac1{(N-1)^2}\sum_{i=1}^N \sum_{k=1}^N (x_i - \bar x)^2 \cdot (x_k - \bar x)^2 \right] = \frac1{(N-1)^2}\sum_{i=1}^N \sum_{k=1}^N \mathbb{E} \left[(x_i - \bar x)^2 \cdot (x_k - \bar x)^2 \right]$$
- We would like to evaluate the expected value $\mathbb{E} \left[(x_i - \bar x)^2 \cdot (x_k - \bar x)^2 \right]$ inside the sum. For that we will use the fact that the R.V.s $\left\{x_i - \bar x\right\}_{i=1}^N$ are jointly Gaussian with zero mean. Therefore, we can denote $z_k := x_k - \bar x$  and expand the expected value term as follows :
$$\mathbb{E} \left[(x_i - \bar x)^2 \cdot (x_k - \bar x)^2 \right] = \mathbb{E}[z_i\cdot z_i\cdot z_k\cdot z_k] = $$$$ = \mathbb{E}[z_i\cdot z_i]\cdot\mathbb{E}[z_k\cdot z_k] + \mathbb{E}[z_i\cdot z_k]\cdot\mathbb{E}[z_k\cdot z_i] + \mathbb{E}[z_i\cdot z_k]\cdot\mathbb{E}[z_k\cdot z_i] = \mathbb{E}[z_i^2]^2 + 2\cdot\mathbb{E}[z_i\cdot z_k]^2$$
$$ \implies \mathbb{E} \left[(x_i - \bar x)^2 \cdot (x_k - \bar x)^2 \right] = \mathbb{E}[z_i^2]^2 + 2\cdot\mathbb{E}[z_i\cdot z_k]^2$$
- We have calculated the first term in subsection c) :
$$\mathbb{E}[z_i^2] = \mathbb{E}[(x_i - \bar x)^2] = \sigma^2 (1- \frac1N)$$
$$\implies \mathbb{E}[z_i^2]^2 = \sigma^4 (1- \frac1N)^2$$
- We want to find $\mathbb{E}[z_i\cdot z_k])$ to evaluate the quantity above.
$$\mathbb{E}[z_i \cdot z_k] = \underbrace{\mathbb{E}[x_i \cdot x_k]}_{\dots=\mu^2 + \delta(i-k) \cdot \sigma^2} - \mathbb{E}[x_i \cdot \bar x] - \mathbb{E}[x_k \cdot \bar x] + \mathbb{E}[\bar x^2] = $$$$ = \mu^2 + \delta(i-k)\cdot\sigma^2 - 2 \cdot (\frac1N\sigma^2 + \mu^2) + (\frac1N\sigma^2 + \mu^2) = \sigma^2 \cdot \delta(i-k)-\frac{\sigma^2}{N}$$
- We plug it back in the previous term :
$$\implies \mathbb{E}[z_i^2]^2 + 2\cdot\mathbb{E}[z_i\cdot z_k]^2 = \sigma^4 (1-\frac{1}{N})^2 + 2 \cdot (\sigma^2 \cdot \delta(i-k)-\frac{\sigma^2}{N})^2 =$$$$ = \sigma^4 \left[  (1-\frac1N)^2 + 2\cdot (\delta(i-k)-\frac1N)^2\right] = \sigma^4 \left[  1-\frac2N + \frac1{N^2} + 2\cdot (\delta(i-k)-\delta(i-k)\frac2N + \frac1{N^2})^2\right] = $$
$$\implies \mathbb{E}[(x_i - \bar x)^2(x_k - \bar x)^2]= \sigma^4\left[1 + 2\delta(i-k) - (2\delta(i-k)+1)\cdot \frac2N + \frac3{N^2}\right]$$
- We count the amount of time that $i=k$ and the rest of the times and substitute accordingly :
$$\frac1{(N-1)^2}\sum_{i=1}^N \sum_{k=1}^N \mathbb{E} \left[(x_i - \bar x)^2 \cdot (x_k - \bar x)^2 \right] =$$$$ = \frac1{(N-1)^2}\sum_{i=1}^N \sum_{k=1}^N \sigma^4\left[1 + 2\delta(i-k) - (2\delta(i-k)+1)\cdot \frac2N + \frac3{N^2}\right] = $$
$$=\frac{\sigma^4}{(N-1)^2} \cdot \left[ N \cdot \left(3-\frac6N + \frac3{N^2}\right) + N(N-1)\left( 1 -\frac2N + \frac3{N^2} \right) \right] = $$$$ \frac{\sigma^4}{(N-1)^2} \cdot \left[ 3N - 6 + \frac3N +N(N-1) - 2(N-1) + \frac{3(N-1)}{N} \right] =$$$$\implies \mathbb{E}[(\tilde \sigma^2)^2] = \frac{\sigma^4}{(N-1)^2}(N^2 - 1) = \sigma^4\frac{N + 1}{N-1}$$
> [!Success] Result
> Since the estimator we proposed is unbiased we know that : $\mathbb{E}[\tilde\sigma^2] = \sigma^2$
> And therefore, we get the expression for the variance of the estimator :
> $$Var(\tilde\sigma^2) = \mathbb{E}[(\tilde\sigma^2)^2] - \mathbb{E}[\tilde\sigma^2]^2 = \frac{\sigma^4}{(N-1)^2}(N^2 - 1) = \sigma^4\frac{N + 1}{N-1} - (\sigma^2)^2$$
> $$\implies Var(\tilde\sigma^2) = \frac{2\sigma^4}{N-1} \ne \frac{2\sigma^4}{N} = CRLB $$
> >[!fail] Not Efficient 
> >We can see that for any finite number of samples the CRLB is not attained!

### e) $N\to \infty$ :

We repeat d) for the limit as N goes to infinity.

- Consistency :

$$\lim_{N\to \infty}Var(\tilde\sigma^2) = \lim_{N\to \infty}\frac{2\sigma^4}{N-1} = 0$$
- We can see that the estimator is consistent

- Efficiency :
$$\lim_{N\to \infty}\frac{Var(\tilde\sigma^2)}{CRLB} = \lim_{N\to \infty}\frac{\frac{2\sigma^4}{N-1}}{\frac{2\sigma^4}{N}} = \lim_{N\to \infty}\frac{N}{N-1} = 1$$
- Therefore, the proposed estimator is **Asymptotically Efficient !** 
## Question 3
![[Pasted image 20260610182824.png]]
### a) Bhattacharyya Bound
![[Pasted image 20260610140457.png]]

We expand the terms by definition :
$$\mathbb{E}\left[ (\hat\theta - \theta)\frac{1}{f(\mathbf x ; \theta)} \cdot \frac{\partial^if(\mathbf x ; \theta)}{\partial\theta^i} \right] = \int_{\mathbb{R}^N} \left[(\hat\theta - \theta)\frac{1}{\cancel{f(\mathbf x ; \theta)}} \cdot \frac{\partial^if(\mathbf x ; \theta)}{\partial\theta^i}\right] \cancel{f(\mathbf x ; \theta)} d\mathbf x = $$
$$ = \int_{\mathbb{R}^N} (\hat\theta - \theta)\cdot \frac{\partial^if(\mathbf x ; \theta)}{\partial\theta^i}  d\mathbf x = \int_{\mathbb{R}^N} \hat\theta\cdot \frac{\partial^if(\mathbf x ; \theta)}{\partial\theta^i}  d\mathbf x - \int_{\mathbb{R}^N} \theta \cdot \frac{\partial^if(\mathbf x ; \theta)}{\partial\theta^i}  d\mathbf x = $$
- Under regularity condition we can switch between integration and differentiation and since $\theta$ isn't a function of $\mathbf x$ and $\hat\theta$ is, we can take it out the integral :
$$= \frac{\partial^i}{\partial\theta^i}\int_{\mathbb{R}^N} \hat\theta\cdot   f(\mathbf x ; \theta) d\mathbf x - \theta\cdot\frac{\partial^i}{\partial\theta^i} \int_{\mathbb{R}^N} f(\mathbf x ; \theta) d\mathbf x  = $$
- We notice the following :
	1. Since the estimator is given to be unbiased we get :$$\int_{\mathbb{R}^N} \hat\theta\cdot   f(\mathbf x ; \theta) d\mathbf x = \mathbb{E}[\hat\theta] = \theta$$
	2. Since the PDF $f(\mathbf x ; \theta)$ is a valid PDF, the integral over all of its domain is $1$ : $$\int_{\mathbb{R}^N} f(\mathbf x ; \theta) d\mathbf x = 1$$
- So basically the expression we are evaluating is :
$$ \dots= \frac{\partial^i}{\partial \theta^i}(\theta) - \underbrace{\frac{\partial^i}{\partial \theta^i}(1)}_{=0 \ : \ \forall i \ge 1} = \frac{\partial^i}{\partial \theta^i}(\theta) = \begin{cases} 1 \quad\quad : i = 1 \\ 0 \quad\quad : i \ge 2 \end{cases}$$


> [!Success] Result
> We have proven the identity :
> $$\mathbb{E}\left[ (\hat\theta - \theta)\frac{1}{f(\mathbf x ; \theta)} \cdot \frac{\partial^if(\mathbf x ; \theta)}{\partial\theta^i} \right] = \begin{cases} 1 \quad\quad : i = 1 \\ 0 \quad\quad : i \ge 2 \end{cases}$$

### b) Finding Lower bound
![[Pasted image 20260610182807.png]]

We will use the Cauchy-Schwarz inequality to find the lower bound of $\mathbb{E}\left[(\hat\theta-\theta)^2\right]$.

- We are asked to define the bound using the matrix $Q \in \mathbb{R}^n$ while :
$$Q_{ij} = \mathbb{E}\left[ \frac{1}{f^2(\mathbf x ; \theta)}\cdot \frac{\partial^if(\mathbf x ; \theta)}{\partial\theta^i} \cdot \frac{\partial^jf(\mathbf x ; \theta)}{\partial\theta^j} \right] \ : \ i,j \in \{1,2,...n\}$$
- We will define $\mathbf z = [z_1,z_2,...,z_n]^T$ to be a random vector of the form : 
$$z_i = \frac{1}{f(\mathbf{x};\theta)} \frac{\partial^i f(\mathbf{x};\theta)}{\partial \theta^i}$$
- From the definition of the matrix $Q$ we notice that :
$$\mathbf{Q} = \mathbb{E}[\mathbf{z}\mathbf{z}^T]$$
- We will calculate the following cross-covariance:
$$\mathbf{v} = \mathbb{E}[(\hat{\theta} - \theta)\mathbf{z}]$$
- If we plug in the full term we get the result from a) :
$$\mathbf v_i = \begin{cases} 1 \quad\quad : i = 1 \\ 0 \quad\quad : i \ge 2 \end{cases} \implies \mathbf v = [1,0,...,0]^T$$
- We can take the covariance matrix of the random vector $\begin{bmatrix}\hat\theta-\theta \\ \mathbf z \end{bmatrix}$ and notice that, by definition, it must be a semi-positive matrix :
$$\mathbb{E} \left[ \begin{bmatrix} \hat{\theta} - \theta \\ \mathbf{z} \end{bmatrix} \begin{bmatrix} \hat{\theta} - \theta & \mathbf{z}^T \end{bmatrix} \right] = \begin{bmatrix} \mathbb{E}[(\hat{\theta}-\theta)^2] & \mathbf{v}^T \\ \mathbf{v} & \mathbf{Q} \end{bmatrix} \succeq 0$$
- We can apply the **Schur complement** of the covariance matrix and get the following inequality :
$$\mathbb{E}[(\hat{\theta}-\theta)^2] - \mathbf{v}^T \mathbf{Q}^{-1} \mathbf{v} \ge 0 \implies \mathbb{E}[(\hat{\theta}-\theta)^2] \ge \mathbf{v}^T \mathbf{Q}^{-1} \mathbf{v}$$
- Since the vector $v = [1,0,...,0]^T$ when multiplying the terms we actually extract the top left entry of the matrix $Q^{-1}$  

> [!Success] Result
> We get the final inequality of the target expected value that defines the Bhattacharyya bound: $$\mathbb{E}[(\hat{\theta}-\theta)^2] \ge [\mathbf{Q}^{-1}]_{11}$$

### c) Comparison to the CRLB
![[Pasted image 20260610182838.png]]
We will prove by induction that : $\text{Bhattacharyya Bound} \ge \text{Cramer-Rao Bound}$

1. Base : $n=1$
	For the base case, $Q$ and $I(\theta)$ are scalar matrices : $$Q_{11} = \mathbb{E}\left[ \left( \frac{1}{f(\mathbf{x};\theta)} \frac{\partial f(\mathbf{x};\theta)}{\partial \theta} \right)^2 \right] = \mathbb{E}\left[ \left( \frac{\partial \ln f(\mathbf{x};\theta)}{\partial \theta} \right)^2 \right] = I(\theta)$$
	We can see that the 2 matrices are equal by definition and therefore, so are their inverses :
	$$\mathbb{E}[(\hat{\theta}-\theta)^2] \ge Q_{11}^{-1} = \frac{1}{I(\theta)} = \text{CRB}$$
	$\implies$ proven for the case of $n=1$!

2. Step : $n > 1$ 
	We can decompose the matrix $Q$ of dimension $n$ as follows :
	$$\mathbf{Q}_n = \begin{bmatrix} Q_{11} & \mathbf{R}^T \\ \mathbf{R} & \mathbf{S} \end{bmatrix}$$
	Where $Q_{11}$ was previously evaluated, $R,R^T \in \mathbb{R}^n$  is some vector (covariance is symmetric...) and $S\in \mathbb{R}^{(N-1)\times (N-1)}$ is some symmetric matrix.
	
	From a formula we derived in Assignment 1 for the inverse of a matrix of such structure we get: $$[\mathbf{Q}_n^{-1}]_{11} = (Q_{11} - \mathbf{R}^T \mathbf{S}^{-1} \mathbf{R})^{-1}$$
	We have already established that $S$ is positive-definite so we can safely claim that :
	$$\mathbf{R}^T \mathbf{S}^{-1} \mathbf{R} \ge 0 \ : \ \forall\mathbf R \in \mathbb R^N$$
	Therefore the following inequality must hold for every number, specifically for $Q_{11}$ :
	$$Q_{11} - \mathbf{R}^T \mathbf{S}^{-1} \mathbf{R} \ge Q_{11} $$
	We take the reciprocal of both sides, and compare with what we got before : $$ \implies \mathbb{E}[(\hat{\theta}-\theta)^2] \ge [\mathbf{Q}_n^{-1}]_{11} = (Q_{11} - \mathbf{R}^T \mathbf{S}^{-1} \mathbf{R})^{-1} \le Q_{11}^{-1} = I(\theta)^{-1}$$

> [!Success] Result
> We have shown that for any $n\in\mathbb{N}$ the inequality between the bounds holds :
> $$ \implies [\mathbf{Q}_n^{-1}]_{11} \ge Q_{11}^{-1}$$
> $$ \implies \text{Bhattacharyya Bound} \ge \text{Cramer-Rao Bound} $$

## Question 4
![[Pasted image 20260610182925.png]]
![[Pasted image 20260610182947.png]]

### a) Verify Claim
![[Pasted image 20260610183011.png]]

We will take the expectation of the random vector.
- We plug in the terms :
$$\mathbb{E}[\mathbf z] = \begin{pmatrix}\mathbb{E}[\hat\theta - \theta] \\ \mathbb{E}[\frac{\partial \log f(\mathbf x ; \theta)}{\partial\theta}] \\ \end{pmatrix}$$
- We are given that said estimator is unbiased, therefore :
$$\mathbb{E}[\hat\theta-\theta] = 0$$
- We expand the second entry by definition and we expand the differentiation of the logarithm :
$$\mathbb{E}\left[\frac{\partial \log f(\mathbf x ; \theta)}{\partial\theta}\right] = \int_{\mathbb{R}^N}\frac{1}{\cancel{f(\mathbf x ; \theta)}}\frac{\partial f(\mathbf x ; \theta)}{\partial\theta} \cdot \cancel{f(\mathbf x ; \theta)} d\mathbf x = \frac{\partial}{\partial\theta} \int_{\mathbb R ^{N}} f(\mathbf x ; \theta) d\mathbf x = \frac{\partial}{\partial\theta}(1) = 0$$

> [!Success] Result
> We have shown the target identity :
> $$\mathbb{E}[\mathbf z] = \begin{pmatrix}\mathbb{E}[\hat\theta - \theta] \\ \mathbb{E}[\frac{\partial \log f(\mathbf x ; \theta)}{\partial\theta}] \\ \end{pmatrix} = \mathbf 0$$

### b) Covariance
![[Pasted image 20260610184110.png]]

We will derive the expression by definition :
$$\Lambda = \mathbb{E}[\mathbf z \mathbf z ^T] = \begin{bmatrix} \mathbb{E}[(\hat\theta - \theta)^2] \quad\quad\quad\quad\quad \mathbb{E}\left[(\hat\theta-\theta)\cdot\frac{\partial\log f(\mathbf x ; \theta)}{\partial\theta}\right] \\ \mathbb{E}\left[(\hat\theta-\theta)\cdot\frac{\partial\log f(\mathbf x ; \theta)}{\partial\theta}\right] \quad\quad \mathbb{E}\left[(\frac{\partial\log f(\mathbf x ; \theta)}{\partial\theta})^2\right] \end{bmatrix}$$
1. $\Lambda_{11}$ : 
	Since the estimator is unbiased we can safely claim that 
	$$\mathbb{E}[(\hat\theta - \theta)^2] = Var(\hat\theta) + \cancel{Bias(\hat\theta)} = Var(\hat\theta)$$
2. $\Lambda_{22}$ : 
	It is quite clear that the target expected value is by definition the fisher information of the estimation of $\theta$ from the samples $\mathbf x$ :
	$$\mathbb{E}\left[(\frac{\partial\log f(\mathbf x ; \theta)}{\partial\theta})^2\right] = I(\theta)$$
3. $\Lambda_{12},\Lambda_{21}$ : 
	In [[#a) Bhattacharyya Bound | 2.a)]] , we have proven that for the first order derivative is 1 :
	$$\left.\mathbb{E}\left[(\hat\theta-\theta)\cdot\frac{\partial^i\log f(\mathbf x ; \theta)}{\partial^i\theta}\right]\right|_{i=1} = 1$$


> [!Success] Result
> We get the final derivation of the covariance matrix of $\mathbf z$ :
> $$\Lambda = \begin{bmatrix} Var(\hat\theta) \quad\quad 1 \\ 1 \quad\quad\quad I(\theta) \end{bmatrix}$$

### c) Proving the CRLB
![[Pasted image 20260610190700.png]]

Since $\Lambda \succeq 0$  can apply its **Schur Complement** to get the following inequality :
$$\Lambda = \begin{bmatrix} Var(\hat\theta) \quad\quad 1 \\ 1 \quad\quad\quad I(\theta) \end{bmatrix} \succeq 0 \implies Var(\hat\theta) - (1)^T \cdot I(\theta)^{-1}\cdot (1) \ge 0 $$

> [!Success] Result
> We get the original CRLB of the Variance for estimating $\theta$ :
> $$\implies Var(\hat\theta) \ge \frac{1}{I(\theta)}$$


## Question 5
![[Pasted image 20260610191440.png]]



### a) Confirm Regularity
![[Pasted image 20260610191526.png]]

We want to show the following :

$$\mathbb{E}\left[\frac{\partial\log f(\mathbf x ; \theta)}{\partial\theta}\right] = 0$$
- First of all, we want to find the conditional distribution of $\mathbf x | \theta$. We will first find the CDF of $\mathbf x | \theta$. Since $w_n \overset{i.i.d.}{\sim} \mathcal P (w_n)$ (double-exponential...) and we are given that $w_n = x_n - \theta$ we can extract the target distribution as follows :
$$f(x_n ; \theta) = f_{W}(x_n - \theta) = \frac12\exp(-|x_n - \theta|)$$
- We take the $\log$ from both side :
$$\log f(x_n ; \theta) = -\log2 -|x_n - \theta|$$
- We take the derivative with respect to $\theta$ :
$$\overset{\frac{\partial}{\partial\theta}}{\longrightarrow} \frac{\partial \log f(x_n ; \theta)}{\partial\theta} = \begin{cases}\quad 1 \quad :\theta \le x_n \\  -1 \quad :\theta \le x_n \end{cases}$$
$$\frac{\partial \log f(x_n ; \theta)}{\partial\theta} = \text{sgn}(x_n - \theta)$$
- Since the sign function is asymmetric around $\theta$ and the conditional PDF is symmetric around $\theta$, the multiplication of the two is asymmetric around $\theta$ so the integral over the real numbers is :
$$\implies \mathbb E \left[\frac{\partial \log f(x_n ; \theta)}{\partial\theta}\right] = \int_{\mathbb R } \text{sgn}(x_n - \theta) \cdot f(x_n;\theta) dx_n = 0 : \forall x_n \ne \theta$$

> [!Success] Result
> We have shown that the regularity condition regarding the Cramer-Rao bound is satisfied for our case :
> $$\mathbb{E}\left[\frac{\partial\log f(\mathbf x ; \theta)}{\partial\theta}\right] = 0$$

### b) Computing the CRB
![[Pasted image 20260610200759.png]]

We will compute the CRB by definition :

- When we plug in the score we have calculated before we notice that the square of the score is 1 everywhere except for at $\theta = x_n$ which is a 0 probability event that can be ignored while integrating :

$$I_1(\theta) = \mathbb E \left[ \left(\frac{\partial\log f(x_n ; \theta)}{\partial \theta}\right)^2\right] = \mathbb E [\text{sgn}^2(x_n - \theta)] = \mathbb E [1] = 1$$
- The previous derivation applies to a single observation. Since our estimation relies on $N$ i.i.d. samples we can use FIM arithmetic to get the final FIM :
$$\implies I(\theta) = N \cdot I_1(\theta) = N$$

> [!Success] Result
> We have successfully calculated the CRB for our case :
> $$CRB = I(\theta)^{-1} = \frac1N$$


### c) Existence of Efficient Estimator
![[Pasted image 20260610203846.png]]

From a theorem we proved in class we know that the bound is attained 
$\iff$ 
the score function is of the form :
$$\frac{\partial \log f(\mathbf x ; \theta)}{\partial\theta} = c(\theta) \cdot (f(\mathbf x) - \theta)$$
Such that :
- $S(\theta,\mathbf x) = \frac{\partial \log f(\mathbf x ; \theta)}{\partial \theta}$ - is the score function of the parameters and the data samples.
- $c(\theta)$ - is a function of the parameters only.
- $f(\mathbf x)$ - is a function of the data samples only.

If all is satisfied then we can conclude that :
- The CRB is attainable for some unbiased estimator.
- $c(\theta) = I(\theta)$ - the coefficient that is constant with respect to the parameters is the Fisher information and is the inverse of the CRB.
- $f(\mathbf x) = \hat\theta(\mathbf x)$ - the function of the data samples is the unbiased estimator that attains the **CRLB**.

We will see if said form is possible :

- From earlier subsection, plus using the property of i.i.d. distributions, we get :
$$\log f(x_n ; \theta) = -|x_n -\theta| \implies \log f(\mathbf x  ; \theta) = \sum_{i=1}^N \log f(x_i;\theta) = -\sum_{i=1}^N |x_i - \theta|$$
- We differentiate and get :
$$\frac{\partial \log f(\mathbf x ; \theta)}{\partial\theta} = \sum_{i=1}^N\text{sgn}(x_i -\theta)$$
- To see if the attainability condition is satisfied we need to see if the following equation can hold :
$$\sum_{i=1}^N\text{sgn}(x_i -\theta) = I(\theta)(\hat\theta-\theta) = N (\hat\theta - \theta)$$
- We notice that the LHS is a sum of sign functions that can only take discrete values with respect to $\theta$ . Meanwhile the LHS is a continuous function of the data samples that is linear with respect to $\theta$.

> [!fail] Result
> We see that the CRLB is not attainable for an unbiased estimator since there is no way that the following equality holds for any estimator $\hat\theta$ :
> $$\frac{\partial \log f(\mathbf x ; \theta)}{\partial\theta} \ne I(\theta) \cdot (\hat\theta(\mathbf x) - \theta) \ : \ \forall \hat\theta : \mathbb R^N \to \mathbb R$$

## Question 6
![[Pasted image 20260610212947.png]]

### a) Find the Efficient estimator
![[Pasted image 20260610213007.png]]

Using the same theorem we used in [[#c) Existence of Efficient Estimator |5.c)]] , we can find the score function of the estimation of $\sigma^2$ from the data samples $\mathbf x$.

- First we will derive the joint-PDF of the random vector $\mathbf x$, and we know that for a zero-mean gaussian random vector the PDF is given by :
$$\mathbf x \sim \mathcal N (\mathbf 0 , \sigma^2 \cdot I_N) \implies f(\mathbf x ; \sigma^2 ) = \frac{1}{(2\pi\sigma^2)^{\frac N2}} \cdot \exp\left( -\frac{1}{2\sigma^2}\mathbf x^T \mathbf x\right)$$
- We take the $\log$ of the PDF and get :
$$\log f(\mathbf{x};\sigma^2) = -\frac{N}{2} \log(2\pi) - \frac{N}{2} \log(\sigma^2) - \frac{1}{2\sigma^2} \mathbf{x}^T \mathbf{x}$$
- We differentiate with respect to $\theta$ and get the score function : 
$$\overset{\frac{\partial}{\partial\sigma^2}}{\longrightarrow}\frac{\partial \ln f(\mathbf{x};\sigma^2)}{\partial \sigma^2} = -\frac{N}{2\sigma^2} + \frac{1}{2(\sigma^2)^2} \mathbf{x}^T \mathbf{x}$$
- We can take the common factor of $\frac{N}{2\sigma^2}$ and get :
$$\frac{\partial \ln f(\mathbf{x};\sigma^2)}{\partial \sigma^2} = \frac{N}{2(\sigma^2)^2} \left( \frac{1}{N} \mathbf{x}^T \mathbf{x} - \sigma^2 \right)$$
- We have shown in [[#a) + b) Find CRB and|2.a)]] that the Fisher-information of the estimation of the variance of a zero-mean gaussian random vector is :
$$I(\sigma^2) = \frac{N}{2\sigma^4}$$
- We then see that we can define $\hat\theta(\mathbf x) = \frac1N \mathbf x ^T \mathbf x$ to satisfy the condition of attainability and get :
$$\frac{\partial \ln f(\mathbf{x};\sigma^2)}{\partial \sigma^2} = I(\theta) \left( \hat\sigma^2(\mathbf x) - \sigma^2 \right)$$


> [!Success] Result
> We have found the estimator that attains the CRB, and therefore, is an unbiased and efficient estimator :
> $$\implies \hat\sigma^2_{eff}(\mathbf x) = \frac1N \mathbf x ^T \mathbf x$$

### b) Find Bias and MSE of Estimator
![[Pasted image 20260610215755.png]]

#### Bias :
Since the estimator we found is unbiased :  $$\mathbb{E} [\hat\sigma^2_{eff}] = \sigma^2$$
We plug that in the Bias of the new proposed estimator : 

> [!Success] Bias
> $$Bias(\hat\sigma^2_a,\sigma^2) =\mathbb E [\hat\sigma^2_a -\sigma^2] = \sigma^2 (a-1)$$
#### Variance :
Since the estimator we found is efficient :
$$Var(\hat\sigma^2_{eff}) = I(\sigma^2)^{-1} = \frac{2\sigma^4}{N}$$
We plug that in the Variance of the new proposed estimator :

> [!Success] Var
> $$Var(\hat\sigma^2_{a}) = Var(a\cdot \hat\sigma^2_{eff}) = a^2 \cdot Var( \hat\sigma^2_{eff}) = a^2 \cdot \frac{2\sigma^4}{N}$$
#### MSE :
The relationship between the Bias, Variance and MSE is as follows :
$$MSE(\hat\sigma^2_a) = Var(\hat\sigma^2_a) + Bias(\hat\sigma^2_a)^2$$
We plug the terms we found back in and get the expression for the MSE :
$$MSE(\hat\sigma^2_a) = 2a^2 \cdot \frac{\sigma^4}{N} + (\sigma^2(a-1))^2$$

> [!Success] MSE
> $$\implies MSE(\hat\sigma^2_a) = \sigma^4 \left( \frac{2a^2}{N} + (a-1)^2 \right)$$

### c) Optimal Value of a
![[Pasted image 20260610221815.png]]

Since the cost function of the estimation is MSE, we will differentiate the MSE that we found with respect to the factor $a$  and compare to zero :
$$\frac{\partial \text{MSE}}{\partial a} = \sigma^4 \left[ \frac{4a}{N} + 2(a - 1) \right] = 0$$
$$\implies \frac{2a}{N} + a - 1 = 0 \implies a = \frac{N}{N+2} = 1 - \frac{2}{N}$$

> [!Success] Optimal value
> $$a_{opt} = \frac{N}{N+2}$$
> 
> $\implies$ We can see that $a_{opt}$ does not depend on $\sigma^2$!
> For the optimal value we get :
> $$\hat\sigma^2_{a_{opt}} = a_{opt} \cdot \hat\sigma^2_{eff} = \frac{\cancel{N}}{N+2} \cdot \frac1{\cancel{N}} \mathbf x^T \mathbf x = \frac1{N+2} \cdot \mathbf x^T \mathbf x $$
> 
>> [!NOTE] Notice
> >We gave up the constraint of efficiency and got better performance for the estimator! 


### d) + e) Simulating Estimator
![[Pasted image 20260610223948.png]]

![[Assignment3_6_d_e.png]]
![[Pasted image 20260610224631.png]]

> [!Note] conclusions
> As we rightfully claimed in [[#c) Optimal Value of a |6.c)]] we intentionally render the optimal estimator inefficient (not asymptotically...) to get a higher convergence rate (as visible in the first MSE plot) and a lower variance than the efficient estimator (as visible in the second MSE plot). Lower variance is attainable since the CRB applies to **unbiased estimators only!**

## Question 7
![[Pasted image 20260610225139.png]]

### a) Conditional FIM
![[Pasted image 20260610225235.png]]

- As we derived in [[#a) Find the Efficient estimator|6.a)]] we know that the conditional distribution $\mathbf x | \theta$ is given by :
$$f(\mathbf x ; \theta) = (2\pi\theta)^{-\frac N2}\cdot \exp\left(\frac{1}{2\theta} \cdot \mathbf x ^T \mathbf x\right)$$
- And the score function is given by :
$$\frac{\partial \ln f(\mathbf{x};\theta)}{\partial \theta} =  \frac{1}{2\theta^2} \mathbf{x}^T \mathbf{x} -\frac{N}{2\theta}$$
- We take the second order derivative to get :
$$\frac{\partial^2 \ln f(\mathbf{x};\theta)}{\partial \theta^2} = \frac{N}{2\theta^2} - \frac{1}{\theta^3} \mathbf{x}^T \mathbf{x}$$
- We substitute the terms for the Fisher-Information and get :
$$I(\theta) = -\mathbb E_{\mathbf x | \theta} \left[\frac{\partial^2 \ln f(\mathbf{x};\theta)}{\partial \theta^2}\right] = \mathbb E \left[ \frac{1}{\theta^3} \mathbf{x}^T \mathbf{x}- \frac{N}{2\theta^2}\right] = \frac{1}{\theta^3} \mathbb E \left[ \mathbf{x}^T \mathbf{x}\right] - \frac{N}{2\theta^2} = \frac{N\theta}{\theta^3} - \frac{N}{2\theta^2} = \frac{N}{2\theta^2}$$
- To get the conditional FIM we need to derive the following expression :
$$J_D = \mathbb{E}_\theta[I(\theta)]$$
- We substitute the Fisher-Information given the parameter $\theta$ back in and get :
$$J_D = \mathbb{E}_\theta[I(\theta)] = \frac N2 \mathbb E [\theta^{-2}]$$
- We now want to evaluate the expected value $\mathbb E [\theta^{-2}]$, for that we will use the definition supplied in the question as a given of the Beta distribution :
$$\mathbb{E}_\theta[\theta^{-2}] = \int_0^1 \theta^{-2} \frac{\theta^{a-1}(1-\theta)^{b-1}}{\beta(a,b)} d\theta = \frac{1}{\beta(a,b)} \int_0^1 \theta^{(a-2)-1}(1-\theta)^{b-1} d\theta = \frac{\beta(a-2, b)}{\beta(a,b)}$$
- Using the definition of $\beta$ :
$$\frac{\beta(a-2, b)}{\beta(a,b)} = \frac{\Gamma(a-2)\Gamma(b)}{\Gamma(a+b-2)} \cdot \frac{\Gamma(a+b)}{\Gamma(a)\Gamma(b)} = \frac{\Gamma(a-2)}{\Gamma(a)} \cdot \frac{\Gamma(a+b)}{\Gamma(a+b-2)}$$
- Using the property of the Gamma function $\Gamma(z) = (z-1)(z-2)\Gamma(z-2)$ (as an extension for the factorial function... ), we can expand :

$$\Gamma(a) = (a-1)(a-2)\Gamma(a-2)$$
- Same way for the denominator :
$$\Gamma(a+b) = (a+b-1)(a+b-2)\Gamma(a+b-2)$$
- Substituting these back gives:

$$\implies \mathbb{E}_\theta[\theta^{-2}] = \frac{(a+b-1)(a+b-2)}{(a-1)(a-2)}$$

> [!Success] Result
> We get the final expression for the conditional FIM :
> $$J_D = \frac{N(a+b-1)(a+b-2)}{2(a-1)(a-2)}$$

### b) Prior FIM
![[Pasted image 20260610233901.png]]

We want to find the Fisher-Information of the Prior $\theta$ :
$$J_P = -\mathbb E \left[ \frac{\partial^2 f_\theta(\theta)}{\partial\theta^2} \right]$$
- First we find the log of the PDF :
$$\log f_\theta(\theta) =\log\left[ \frac{\theta^{a-1}(1-\theta)^{b-1}}{\beta(a,b)}\right] = (a-1)\log(\theta) + (b-1)\log(1-\theta) - \log\beta(a,b)$$
- We take the first and second order derivative with respect to $\theta$ :
$$\implies \frac{\partial \ln f_\theta(\theta)}{\partial \theta} = \frac{a-1}{\theta} - \frac{b-1}{1-\theta}$$
$$\implies \frac{\partial^2 \ln f_\theta(\theta)}{\partial \theta^2} = -\frac{a-1}{\theta^2} - \frac{b-1}{(1-\theta)^2}$$
- The prior FIM is the negative expectation over $\theta$:
$$\implies J_P = \mathbb{E}_\theta\left[ -\frac{\partial^2 \ln f_\theta(\theta)}{\partial \theta^2} \right] = (a-1)\mathbb{E}_\theta[\theta^{-2}] + (b-1)\mathbb{E}_\theta[(1-\theta)^{-2}]$$

- We already found $\mathbb{E}_\theta[\theta^{-2}]$ in part a. We also notice that the PDF is symmetric with respect to the interval $[0,1]$ :
$$f_{\theta|a,b}(1-\theta) = \frac{(1-\theta)^{a-1}(1-(1-\theta))^{b-1}}{\beta(a,b)} = \frac{\theta^{b-1}(1-\theta)^{a-1}}{\beta(a,b)} = f_{\theta|b,a}(\theta) $$
- We can use this property to get :
$$\mathbb{E}_{\theta|a,b}[(1-\theta)^{-2}] = \mathbb{E}_{\theta|b,a}[\theta^{-2}] = \frac{(a+b-1)(a+b-2)}{(b-1)(b-2)}$$
- We plug it back in to the previous expression for the $J_p$ and get :
$$J_P = (a-1)\frac{(a+b-1)(a+b-2)}{(a-1)(a-2)} + (b-1)\frac{(a+b-1)(a+b-2)}{(b-1)(b-2)}$$
$$ = \frac{(a+b-1)(a+b-2)}{a-2} + \frac{(a+b-1)(a+b-2)}{b-2}$$
$$= (a+b-1)(a+b-2) \left( \frac{1}{a-2} + \frac{1}{b-2} \right)$$

> [!Success] Result
> We get the final expression for the Prior FIM :
> $$J_P = \frac{(a+b-1)(a+b-2)(a+b-4)}{(a-2)(b-2)}$$

