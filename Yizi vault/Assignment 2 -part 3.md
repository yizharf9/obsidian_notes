
## Question 5

![[Pasted image 20260520164810.png]]

We want to prove that :
$$
\exists \hat\theta_2 \ne \hat\theta_1 : MSE(\hat\theta_2) \lt MSE(\hat\theta_1)
$$
For that we will give an example for such an estimator.

- We define $\hat\theta_{2,c}$ to a family of estimators as follows :
$$
\hat\theta_{2,c}(\mathbf{y}) = \hat\theta_1(\mathbf{y}) + c \cdot g(\mathbf{y}) :c\in \mathbb{R}
$$
- We derive the expression for the MSE of said estimator :
$$MSE(\hat\theta_{2,c}(\mathbf{y})) = \mathbb{E}\left[(\hat\theta_{2,c}(\mathbf{y}) - \theta)^2\right] = \mathbb{E}\left[(\hat\theta_{1}(\mathbf{y}) + c\cdot g(\mathbf{y}) - \theta)^2\right] = $$$$= \mathbb{E}[(\hat\theta_{1}(\mathbf{y}) - \theta)^2] + 2 \cdot c \cdot \mathbb{E}[(\hat\theta_{1}(\mathbf{y}) - \theta) \cdot g(\mathbf{y})] + c^2 \cdot \mathbb{E}[g(\mathbf{y})^2] =MSE(\hat\theta_1) + 2 c \rho + c^2 \sigma^2$$
- We get  an expression for the MSE  of the new estimator as a function of the free parameter $c$.
- To find the global minimum of the function (parabolic function is convex...) we take the derivative with respect to the parameter $c$ , equate to 0 and observe the new MSE of the argmin of the function :
$$
\overset{\frac{d(MSE(\hat\theta_1))}{dc}}{\longrightarrow} 
2 \rho + 2c \sigma^2 = 0\implies
c_{min} = - \frac{\rho}{\sigma^2}
$$
$$
\left. MSE(\hat\theta_{2,c}(\mathbf{y})) \right|_{c_{min}} = 
MSE(\hat\theta_1) + 2 (- \frac{\rho}{\sigma^2}) \rho + (- \frac{\rho}{\sigma^2})^2 \sigma^2 =
MSE(\hat\theta_1) -  2 \frac{\rho^2}{\sigma^2} + \frac{\rho^2}{\sigma^2} = 
MSE(\hat\theta_1) - \frac{\rho^2}{\sigma^2}
$$
- We define the estimator $\hat\theta_2$ to be the estimator in the family for the $c_{min}$ value we found.



> [!success] Done!
> We can see that the new estimator's MSE is strictly lower than the original one's and so we have found an estimator that satisfies the target property :
>$$\forall \rho , \sigma \in \mathbb{R} : \frac{\rho^2}{\sigma^2} \gt 0 \implies MSE(\hat\theta_2) < MSE(\hat\theta_1)$$


## Question 6

![[Pasted image 20260521150527.png]]

### Find MMSE estimator

We want to find the estimator $\hat {(y_{N+k})}\left(\{y_n \}_{n=1}^N\right)$ of the AR process. For that we need to find the the explicit expression for that data sample.

- We derive the estimator according to the target expected value by definition.
- First, we find an explicit expression for the ${(N+k)}^{th}$ sample :
$$
y_{_{N+k}} = a \cdot y_{_{N+k-1}} + u_{_{N+k}} =
a \cdot \left[ a \cdot y_{_{N+k-2}} + u_{_{N+k-1}} \right] + u_{_{N+k}} =
a^2 \cdot y_{_{N+k-2}} + a \cdot u_{_{N+k-1}} + u_{_{N+k}} = \dots 
$$
- We can notice that since We are given the sample $y_{_{N}}$ ,we can stop deriving at that point and ignore the $N^{th}$ noise sample since it is contain in that data sample :
$$
= a^k \cdot y_{_{N}} + 
\left[u_{_{N+k}} + a \cdot u_{_{N+k-1}} + \dots + a^{k-1} \cdot u_{_{N+1}}\right]  = 
a^k \cdot y_{_{N}} + 
\sum_{m=1}^k{a^{k-m} \cdot u_{_{N+m}}} 
$$
- Finally, we substitute the expression in the conditional expected value to find the MMSE estimator :
$$
\implies \mathbb{E}[y_{_{N+k}} | y_0 ... y_N] 
\underbrace{=}_{\text{independent of :} y_0 ... y_N}
\mathbb{E}[y_{_{N+k}} | y_N] = 
\mathbb{E}[
	a^k \cdot y_{_{N}} + 
	\sum_{m=1}^k{a^{k-m} \cdot u_{_{N+m}}} 
]
$$
$$
= a^k \cdot y_{_{N}} +
\sum_{m=1}^k{
	a^{k-m} \cdot 
	\underbrace{
		\cancel{
		\mathbb{E}[	
		 u_{_{N+m}}
		]
		}
	}_{\dots = 0}
} =  a^k \cdot y_{_{N}}
$$

> [!success] Result
> We get the final expression for the estimator :
> $$ \hat y_{_{N+k}}(\mathbf y) = \mathbb{E}[y_{_{N+k}} | y_0 ... y_N] = a^k \cdot y_{_{N}}$$

### Find Bias of the estimator

We will find the Bias of the estimator according to the definition.

$$
b(\hat y_{_{N+k}}) = 
\mathbb{E}[\hat y_{_{N+k}} - y_{_{N+k}} | \mathbf{y}] = ...
$$
- Based on the same logic used to derive the expression for the estimator previously, we will derive the expression for the $n^{th}$  data sample :
$$
\implies y_n = \underbrace{a^n \cdot y_0}_{\dots = 0 } + \sum_{k=1}^n {a^{k-n} \cdot u_{n+k}} \implies 
y_n = \sum_{k=1}^n {a^{n-k} \cdot u_{n+k}}
$$
- We substitute terms of both the estimator and the derivation of the $n^{th}$ sample :
$$
\dots = \mathbb{E}[a^k \cdot y_{_N}| \mathbf{y}] - 
\mathbb{E}\left[
	\left.
	\sum_{m=1}^n {a^{n-m} \cdot u_{m}} 
	\right | \mathbf{y}
\right] = 
a^k \cdot y_{_N} - 
\mathbb{E}\left[
	\left.
	\sum_{m=1}^n {a^{n-m} \cdot u_{m}} 
	\right | \mathbf{y}
\right]  = 
$$
- We notice that since the $N^{th}$ sample is given, the following data samples are statistically dependent on that sample and the noise added in the next $k$ samples :
$$
= a^k \cdot y_{_N} - 
\sum_{m=1}^n {a^{n-m} \cdot 
\mathbb{E}\left[
	u_{m} | \mathbf{y}
\right]} =
a^k \cdot y_{_N} - 
\sum_{m=1}^n {a^{n-m} \cdot 
\mathbb{E}\left[
	u_{m} | \mathbf{y}
\right]} =
$$
$$
= a^k \cdot y_{_N} - 
a^k \cdot y_{_N}  -
\sum_{m=N+1}^{N+k} {
	a^{N+1-m} \cdot 
	\underbrace{\mathbb{E}[u_{m}|\mathbf{y}]}_{u_{_{N+k}} \perp \! \perp y_n : \forall n \le N }
}
= 0 
$$

> [!success] Result
> We find that the estimator is **strict sense unbiased**  :
> $$b(\hat y_{_N+k}) = 0$$ 

### MSE of the estimator

We will calculate the MSE by definition.

- Using the same logic as the last transition we made while calculating the bias we get :
$$
MSE(\hat y_{_N+k}) = 
\mathbb{E}[(\hat y_{_N+k} - y_{_N+k})^2] =
\mathbb{E}\left[
\left(\sum_{m=1}^{k} {a^{N-m} \cdot u_{_{N+m}}}\right)^2
\right] = 
\sum_{n,m}^{k} {a^{k-m + (k-n)} \cdot 
\mathbb{E}\left[
	u_{_{N+m}} \cdot u_{_{N+m}} 
\right]} = 
$$$$\dots = \left\{u_m \perp \! \perp u_n : \forall n\ne m\right\} = \sum_{m = 1}^k (a^2)^{k-m} \sigma^2 =\sigma^2 \cdot \frac{a^{2k} - 1}{a-1}$$

> [!success] Result
> We get the final expression for the MSE of the estimator :
> $$ MSE(\hat y_{_N+k}) =  \sigma^2 \cdot \frac{a^{2k} - 1}{a-1} = \mathcal{O}(a^k)$$
> Meaning that the MSE grow exponentially with respect to how far to the future we are trying to estimate.

