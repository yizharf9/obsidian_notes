
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
K^T \cdot R \cdot K  = (H^TWH) \\ 
K^T_0 \cdot R \cdot K \\
K^T \cdot R \cdot K_0 \\
K^T_0 \cdot R \cdot K_0 =\dots
\end{cases}
$$