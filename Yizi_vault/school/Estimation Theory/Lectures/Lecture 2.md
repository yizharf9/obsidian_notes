
## Continuing - WLS estimator
[[Lecture 1#Weighted Least Squares (WLS) estimator| link to previous lecture]]

We will now calculate the estimation : $$\underline{\varepsilon}_{WLS} = \mathbb{E}[\hat{\theta}_{WLS} - \theta] = (H^TWH)^{-1}H^TW \cdot \mathbb{E}[\underline{x}]  - \underline{\theta}$$
$$\dots = (H^TWH)^{-1}H^TW \cdot (H\theta + \underbrace{\mathbb{E}[\underline{v}}_{\dots = 0}]) - \underline{\theta} = \mathbb{I} \cdot \underline{\theta} - \underline{\theta} = \underline{0} $$

> [!info] Notice
> That the WLS estimator is **Unbiased** as long as the Covariance of the additive noise is 0.

We now calculate the Second Order Statistics of the WLS estimator : 
- We assume $\mathbb{E}[\underline{v}] = 0$ 
- We assume $\mathbb{E}[\underline{v}\underline{v}^T] = \underline{\underline{R}} =  Cov(\underline{x})$ 
$$\implies Cov(\hat{\theta}_{WLS}) = Cov(\underline{\varepsilon}_{WLS}^T) = (H^TWH)^{-1}H^TW \cdot Cov(\underline{x}) \cdot [(H^TWH)^{-1}H^TW]^T =\dots $$

> [!warning] 
> The assumption of $W$ symmetric is not a necessary one...
> 
> $\implies$ We continue with the assumption that $W$ is not symmetric...

$$
Q(\hat{\theta}_{WLS}) = 
\underbrace{(\underline{x} - H \underline{\theta})^T}_{:=\Gamma^T}
\cdot W \cdot 
\underbrace{(\underline{x} - H \underline{\theta})}_{:=\Gamma} = 
\sum_{i=1}^{N} \sum_{j=1}^{N} {w_{i,j} \cdot \Gamma_i \cdot \Gamma_j} = \dots
$$
$$
\dots = \sum_{i=1}^N{w_{i,i} \cdot \Gamma_i^2} + 
\sum_{i=i+1}^N \sum_{j=1}^N{w_{i,j} \cdot \Gamma_i \cdot \Gamma_j} + 
\sum_{j=j+1}^N \sum_{i=1}^N{w_{j,i} \cdot \Gamma_i \cdot \Gamma_j} = \dots
$$
$$
\dots = 
\sum_{i=1}^N\underbrace{w_{i,i} \cdot \Gamma_i^2}_{:= \tilde{w}_{i,i}} +

\sum_{i=i+1}^N \sum_{j=1}^{N} {\underbrace{\frac{1}{2}(w_{j,i} + w_{j,i}) \cdot \Gamma_i \cdot \Gamma_j}_{:=\tilde{w}_{i,j}}} + 

\sum_{i=i+1}^N \sum_{j=1}^{N} {\underbrace{\frac{1}{2}(w_{j,i} + w_{j,i}) \cdot \Gamma_i \cdot \Gamma_j}_{:=\tilde{w}_{j,i}}} = 
$$
$$
\dots = \sum_{i=1}^{N} \sum_{j=1}^{N} {w_{i,j} \cdot \Gamma_i \cdot \Gamma_j} =  (\underline{x} - H\theta)^T \cdot \tilde{W} \cdot (\underline{x} - H\theta)^T
$$

> [!info] 
> This means that when we have a $W$ that **is not symmetric**,
> $\implies$ we can always get an equivalent representation of the form : $$ \hat{\theta}_{WLS}(\underline{x}) = 
(\underline{x} - H\theta)^T \cdot \tilde{W} \cdot (\underline{x} - H\theta)^T = 
(\underline{x} - H\theta)^T \cdot (\frac{\tilde{W}^T + W}{2}) \cdot (\underline{x} - H\theta)^T
$$

### Finding Optimal $W$ for WLS

We would like to find $W$ that minimizes $Cov(\underline{\theta}_{WLS})$ .

#### Lemma
#Lemma 

- The $\hat{\theta}_{WLS}$ estimator has lower covariance than the $\hat{\theta}_{LS}$ estimator if : $$Cov(\hat{\underline{\theta^*}}) \le Cov(\hat{\underline{\theta}})$$
- Or in other words : $$ \iff Cov(\hat{\underline{\theta^*}}) -   Cov(\hat{\underline{\theta}}) \succeq 0 $$
$$ 
\iff \forall \underline{a} \in \mathbb{R}^N \ : \  \underline{a}^T \cdot (Cov(\hat{\underline{\theta^*}}) -   Cov(\hat{\underline{\theta}})) \cdot \underline{a}
\succeq 0 
$$
$$ 
\iff \forall \underline{a} \in \mathbb{R}^N \ : \  
\underline{a}^T \cdot Cov(\hat{\underline{\theta}}) \cdot \underline{a} \le  
\underline{a}^T \cdot Cov(\hat{\underline{\theta^*}}) \cdot \underline{a}
$$
$$
\iff
\forall \underline{a} \in \mathbb{R}^N \ : \
Var(\underline{a}^T \hat{\underline{\theta}}) \le
Var(\underline{a}^T \hat{\underline{\theta^*}})
$$
- The variance of every linear combination of $\hat{\underline{\theta}}$ is bounded by the variance of the same linear combination of $\hat{\underline{\theta^*}}$ .

- In particular, if we chose : $$
\begin{pmatrix}
0\\0\\\dots\\1\\\dots\\0
\end{pmatrix} = \underline{a} = \underline{e}_i
$$
- The standard base of dim. $N$ we get : 
$$
\forall i \in 1\dots N \ : \ Var(\hat{\underline{\theta_i}}) \ge Var(\hat{\underline{\theta_i^*}})
$$
 -  We are looking for $\hat{\theta}^* = \hat{\theta}(W)$ such that :
$$
\forall W \succ 0 \ : \ Cov(\hat{\underline{\theta}^*}) \le Cov(\hat{\underline{\theta}}(W))
$$

#### Lemma
#Lemma

The WLS estimator with weight matrix $W = R^{-1}$ minimizes the covariance matrix of the estimation error, Meaning : 
$$
Cov(\hat{\underline{\theta}}_{WLS}^*) = 
Cov(\hat{\underline{\theta}}_{WLS}(W = R^{-1})) \le 
Cov(\hat{\underline{\theta}}_{WLS}(W)) \ : \ \forall W \succ0  
$$
**Proof** :

- We denote : 
$$
K = (H^TWH)^{-1}H^T \cdot W
$$
$$
K_0 = (H^TWH)^{-1}H^T \cdot R^{-1}
$$
$$
\implies A = (K - K_0)^T \cdot R \cdot (K - K_0)
$$
- We will show that $A$ is positive semidefinite :
$$
\forall \underline{a} \in \mathbb{R}^N \ : \ 
\underbrace{\underline{a}^T \cdot (K - K_0)^T }_{:=\underline{b}^T}
\cdot R \cdot 
\underbrace{(K - K_0) \cdot \underline{a}} _{:=\underline{b}}
\ge 0 
$$
$$
\implies \underline{b}^T \cdot R \cdot \underline{b} \ge 0 
$$
- Since $R \succeq 0$ ...
$$
\implies A \succeq 0
$$

> [!success] 
> We can see that $A$ is symmetric, positive semidefinite.

$$
A = K^T \cdot R \cdot K - K^T_0 \cdot R \cdot K - K^T \cdot R \cdot K_0 + K^T_0 \cdot R \cdot K_0 =\dots
$$
 - We substitute back in the values for $K,K_0$ :
$$
\begin{cases}
K^T_0 \cdot R \cdot K = (H^TWH)^{-1}H^TW \cdot R R^{-1} \cdot H (H^TR^{-1}H)^{-1} = (H^TR^{-1}H)^{-1}   \\ 
K^T \cdot R \cdot K_0 = (H^TR^{-1}H)^{-1}   \\ 
K^T_0 \cdot R \cdot K_0 = (H^TR^{-1}H)^{-1}   \\ 
\end{cases}
$$
- After subtracting from both sides :
$$
 \implies K^T \cdot R \cdot K  - K^T_0 \cdot R \cdot K_0 = A \succeq 0
$$
$$
K^T \cdot R \cdot K \succeq K_0^T \cdot R \cdot K_0  \ : \ \forall W 
$$
$$
\implies 
Cov(\hat{\underline{\theta}}_{WLS}(W = R^{-1})) \le 
Cov(\hat{\underline{\theta}}_{WLS}(W)) \ : \ \forall W 
$$

> [!info] Meaning...
> If we choose $W = R^{-1}$ we get that the Cov. is smaller or equal always, for every choice of $W$ (notice that we didn't put any requirements on the matrix...).
> Therefore, the minimum is achieved with this choice of $W$.

> [!warning] Notice... 
> $W$ is not necessarily the only minimum!


> [!Example]-
> 
> $\underline{x} = \mathbb{1} \cdot \theta + \underline{v}$ 
> $\mathbb{E}[\underline{v}] = 0$
> $\mathbb{E}[\underline{v} \cdot \underline{v}^T] = 0$ 
> Every data sample with large variance that will be added will yield large $Var(\hat{\underline{\theta}}_{LS})$ : $$\hat{\underline{\theta}}_{LS} = \frac{1}{N}\sum_{n=1}^{N}{x_n}$$
>$$\implies Var(\hat{\underline{\theta}}_{LS}) = \frac{1}{N^2}\sum_{n=1}^{N}{\sigma_n^2}$$
> In contrast to the WLS estimator, that will not affect the variance as much : $$
\implies Var(\hat{\underline{\theta}}_{LS}) = 
(\mathbb{1}^T \cdot R^{-1} \cdot \mathbb{1})^{-1} = 
\frac{1}{\sum_{n=1}^{N}{\frac{1}{\sigma_n^2}}}$$
>For the case in which the variance of all samples is equal $\sigma_1^2 = \dots = \sigma_n^2 = \sigma^2$  we get : $$
Var(\hat{\underline{\theta}}_{LS}) = \frac{1}{N} \cdot N \cdot \sigma^2 = \frac{\sigma^2}{N}$$
>$$ Var(\hat{\underline{\theta}}_{WLS}) = \frac{1}{N \cdot \frac{1}{\sigma^2} } = \frac{\sigma^2}{N}$$
>
>> [!info] Meaning...
> The WLS estimator uses the weights to weight out any exceptionally high variance of a data sample.
> $\implies$ If all data samples are statistically equivalent, the WLS estimator looses all advantage over the LS estimator.
>
>The estimator in the example : $$\hat{\theta}_{WLS} = (H^TR^{-1}H)H^TR^{-1}\underline{x} = (\mathbb{1}^T\cdot R^{-1} \cdot \mathbb{1})\cdot \mathbb{1}^T \cdot R^{-1} \cdot \underline{x}$$ 
>$$\implies \hat{\theta}_{WLS} = \frac{\sum_{n=1}^{N}{\frac{x_n}{\sigma^2}}}{\sum_{n=1}^{N}{\frac{1}{\sigma^2}}}$$


## WLS estimator in Non-Linear Problems

-  Model that is not necessarily Linear :
$$
\underline{x} = \underline{h}(\underline{\theta}) + \underline{v} \ : \ 
\underline{h} : \mathbb{R}^M \to \mathbb{R}^N
$$
- The matching estimation criterion will be :
$$
Q(\underline{\theta}) = ||\underline{x} - \underline{h}(\underline{\theta})||^2 = (\underline{x} - \underline{h}(\underline{\theta'}))^T \cdot W \cdot (\underline{x} - \underline{h}(\underline{\theta'}))
$$
$$
\implies \hat{\underline{\theta}}_{LS} = \underset{\underline{\theta'}\in \mathbb{R}^{M}}{argmin}\{ Q(\underline{\theta'})\}
$$

> [!danger] Problem
>The problem right now is that this task might be a lot more difficult...


> [!Example]+
> This is an example of when the measurements are continuous and not discrete as it has been so far...
> $x(t) = s(t,\underline{\theta}) + v(t) \ : \ \forall t \in [0,T]$
>We sample the signal in time intervals with length $t_n = n\cdot T_s \ : \ T_s \to 0$  :
>$$x(t_n) = s(t_n,\underline{\theta}) + v(t_n) \ : \ \forall t \in [0,T]$$
>We take $N$ samples such that :
>$$\underline{x} = \underline{s}(\underline{\theta}) + \underline{v} \ : \ \underline{x} \in \mathbb{R}^N$$
>$$
>Q(\theta) = ||\underline{x}||^2 - 
>2 \underline{s}(\underline{\theta})^T \underline{x} +
>||\underline{s}(\underline{\theta})||^2
>\underset{\underline{\theta}}{\longrightarrow} min
>$$
>$$
>\underline{s}(\underline{\theta})^T \underline{x} =  
>\frac{1}{T_s}\sum_{n=1}^{N}s(t_n,\underline{\theta})x_nT_s \
>\underset{T_s \to 0 }{\longrightarrow} \
>\frac{1}{T_s} \int_{0}^{T}{s(t,\underline{\theta})x_ndt}
>$$
>$$
>\underline{s}(\underline{\theta})^T \underline{s}(\underline{\theta}) 
>\underset{T_s \to 0 }{=} \
>\frac{1}{T_s} \int_{0}^{T}{s(t,\underline{\theta})^2dt}
>$$
>And therefore, the LS estimator will be derived :
>$$
>\hat{\theta}_{LS} = \underset{\underline{\theta'}\in \mathbb{R}^{M}}{argmax}
>\frac{1}{T_s} 
>\{
> 2\int_{0}^{T}{s(t,\underline{\theta})dt} - 
> \int_{0}^{T}{s(t,\underline{\theta})^2dt}
>\}
>$$
>> [!info]
>> $T_s$ is independent of $\underline{\theta}$, and therefore in this maximization problem with respect to $\underline{\theta}$ this parameter can be omitted.
>> $\implies$ the performance of the estimator does not depend on the sample rate!
> >



### Time Delay estimation (TDE) Problem

- In many problems such as this, the entire expression : 
$$
\dots \int_{0}^{T}{s(t,\underline{\theta})^2dt} = Const.
$$
- since the energy of the signal does not change when we perform a delay/phase shift...
- And since a constant does not depend on $\underline{\theta}$ we get the equivalent optimization problem :
$$
\hat{\theta}_{LS} = \underset{\tau\in \mathbb{R}}{argmax}
	\int_{0}^{T}{s(t- \tau)x(t)dt}
$$
![[TDE system.canvas | visual TDE system]]
- In this case it is easy to derive the maximization problem - we will find a maximum to the system as a function of $\tau$.
- this is a specific case in which, despite the non-linearity of the system we may still estimate under the assumption of a specific model of the system.

- 

















[[school/Estimation Theory/Lectures/Lecture 3| link to next lecture...]]

