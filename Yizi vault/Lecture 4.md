
## Bayesian Parameter Estimation

Our goal is to :
$$
\mathbb{E}[C(\hat{\theta},\theta)] \longrightarrow min.
$$
Equivalent problem :

$$
\mathbb{E}[C(\hat{\theta},\theta)|X] \underset{\hat{\theta}(X)}{\longrightarrow} min.
$$
Given some $\underline{x}$ finding the parameters $\hat{\theta}$ to bring to minimum the estimation error.

### The cost function :

1. $C_{MSE}(\hat{\theta},\theta) = (\hat{\theta} - \theta)^T W (\hat{\theta} - \theta)$   
	- When $W \succ 0 \implies$ MMSE
	- When $W = I \implies$ Norm squared 
	
2. $C_{MAE}(\hat{\theta},\theta) = |\hat{\theta} - \theta|$  - Mean Average Estimator
	
3. $C_{OEP}(\hat{\theta},\theta) = \mathbb{1}_{(\hat{\theta} - \theta) \ge \Delta}(\hat{\theta},\theta)$ - Outage Error Probability 

### MMSE

- The previous approach we took in previous lectures....
$$
\mathbb{E}[C_{MSE}(\hat{\theta},\theta) | X] = \mathbb{E}[(\hat{\theta}-\theta)^TW(\hat{\theta}-\theta)] \longrightarrow min.
$$
- After taking derivative and finding minimum of the cost function we get :
$$
\hat{\theta}_{MMSE} = \mathbb{E}[\theta|X]
$$

- MMSE gives us the average Power of the estimation error.
- In the case in which $\underline{X},\underline{\theta}$ are joint-gaussian, the optimal estimator converges to the linear estimator and then the estimation is quite simple.
- Otherwise in other cases the estimator is of the form :
$$
\hat{\theta}_{MMSE} = 
\int_{\Omega_{\theta}}{\underline{\varphi} \cdot 
f_{\underline{\theta} | \underline{x}}(\underline{\varphi} | \underline{x})
}d\underline{\varphi}
$$
- usually finding the joint PDF is near impossible if not very hard!
- Therefore, we can simplify the PDF using Bayes theorem giving us a much more managable expression to work with in most cases : 
$$
f_{\underline{\theta} | \underline{x}}(\underline{\varphi} | \underline{x}) = 
\frac{f_{ \underline{x}| \underline{\theta}} \cdot f_{\underline{\theta}}}
{\int_{\Omega_\theta}{f_{\underline{x}|\underline{\theta}}}} \
 : \ \underline{X} = \underline{h}(\underline{\theta}) + \underline{v}
$$
- We conclude our derivation with the final expression for the MMSE estimator :

$$
\hat{\theta}_{MMSE} = 
\frac{
\int_{\Omega_\theta}{
		\underline{\varphi}\cdot 
		f_{ \underline{x}| \underline{\theta}} \cdot f_{\underline{\theta}}\cdot d\underline{\varphi}
	}
}
{
\int_{\Omega_\theta}{
f_{\underline{x}|\underline{\theta}}}
\cdot f_{\underline{\theta}}\cdot 
d\underline{\varphi}
}
$$
- Usually the distribution of $\theta$ is a given and so as its PDF.
- Additionally, $f_{\underline{x}|\underline{\theta}}$ ,once $\underline{x}$ is known in under the previously stated statistical model, $\underline{h}(\underline{\theta})$ becomes deterministic and  $f_{\underline{x}|\underline{\theta}} \sim f_{\underline{v}}$ 

- We will find the expression for the $m^{th}$ entry of $\underline{\theta}$ :
$$
\hat{\theta}_{MMSE} = 
\int_{\Omega_\theta}{
	\varphi_m\cdot 
	f_{
		\underline{\theta} | \underline{x}
	}(\underline{\varphi} | \underline{x})
	\cdot d\varphi_m
}=
$$

$$
\int_{\Omega_{\theta_m}}{
	\varphi_m\cdot 
	(\int_{\Omega_{\theta_1}...\Omega_{\theta_m-1},\Omega_{\theta_m+1}...\Omega_{\theta_M}}{
		
		f_{
			\underline{\theta} | \underline{x}
		}(\underline{\varphi} | \underline{x})
		\cdot d\varphi_1...
		\cdot d\varphi_m-1,
		\cdot d\varphi_m+1...
		\cdot d\varphi_M
	})\cdot d\varphi_m
}= 
$$
$$
\implies \hat{\theta}_{m,MMSE}(\underline{X}) = \mathbb{E}[\theta_m|\underline{X}]
$$


### MAP Estimator

==FILL IN BLANK==

#### #Theorem :

 If the a-posteriori PDF is symmetric around the conditional expected value
 $\implies \hat{\theta}_{MS}$ minimizes every expected value of a symmetric and convex function.

**proof** : 

- We will denote : $\underline{\varphi} = \underline{\theta} - \underline{\hat{\theta}}_{MS}$ 
- We get :
$$
Symmetric \implies
f_{\underline{\theta}|\underline{x}}(\underline{\varphi}|\underline{x}) = 
f_{\underline{\theta}|\underline{x}}(\underline{-\varphi}|\underline{x}) 
$$
The Theorem assumes the following :
1. Symmetric
2. $\bar{C}(\underline{\varepsilon}) = \bar{C}(-\underline{\varepsilon})$ 
3. $\bar{C}(\cdot)$ - Convex 

**Aux. claim** :
$$
\mathbb{E}[\bar{C}(\hat{\theta}_{MS} -\theta)] \le
\mathbb{E}[\bar{C}(\hat{\theta} -\theta)] 
\ : \ \forall \hat{\theta}(\cdot) \ : \ \mathbb{R}^N \to \mathbb{R}^N
$$
- From convexity we get : 
$$
\bar{C}(\lambda \underline{\varepsilon_1} + (1- \lambda) \underline{\varepsilon_1}) \le
\lambda \bar{C}( \underline{\varepsilon_1}) + 
(1- \lambda) \bar{C}( \underline{\varepsilon_1}) 
\ : \ \forall 0 \le \lambda \le 1
\ : \ \forall \underline{\varepsilon}_1,\underline{\varepsilon}_2 \in \Omega_\theta
$$
- We expand the term for the conditional expected value :
$$
\mathbb{E}[\bar{C}(\hat{\theta}-\theta)|X]=
\frac{1}{2}\mathbb{E}[\bar{C}(\hat{\theta}-\theta)|X]+
\frac{1}{2}\mathbb{E}[\bar{C}(\theta-\hat{\theta})|X] =
\frac{1}{2}\mathbb{E}[ \bar{C}(\underline{\varphi} +\hat{\theta}-\theta)|X]+
\frac{1}{2}\mathbb{E}[\bar{C}(-\underline{\varphi} + \hat{\theta}-\theta)|X]=
$$
$$
\implies\mathbb{E}[ \bar{C}(\underline{\varphi}+\hat{\theta}-\theta)|X] =
\frac{}\int_{\Omega_\theta}{\bar{C}(\underline{\varphi} + \hat{\theta}-\theta)}f_{\underline{\varphi}|\underline{x}}(\underline{\varphi}|\underline{x}) d\underline{\varphi} \underset{\varphi' := -\varphi}{=}
\mathbb{E}[\bar{C}(\hat{\underline{\theta}}+\underline{\varphi} - \hat{\theta}_{MS})] 
$$
$$
\dots= \mathbb{E}[\bar{C}(\hat{\underline{\theta}}-\theta)] =
\mathbb{E}[
	\underbrace{ \frac{1}{2} }_{:=1-\lambda}
	\bar{C}(\hat{\underline{\theta}}-\theta + \underline{\varphi}) +
	\underbrace{ \frac{1}{2} }_{:=\lambda}
	\bar{C}(\hat{\underline{\theta}}-\theta - \underline{\varphi})
	| \underline{X}
] \underset{convex\to}{=} 
$$
$$
\dots = \mathbb{E}[\bar{C}(\hat{\underline{\theta}}-\theta)|\underline{X}] \ge 
\mathbb{E}[\bar{C}(\hat{\underline{\theta}}_{MS}-\theta)|\underline{X}]
\implies \hat{\theta}_{MS} = \underset{\hat{\theta}}{argmin}\{
\mathbb{E}[\bar{C}(\hat{\underline{\theta}}-\theta)]
\}
$$

> [!Example] Usecase
> In tests, we might be asked to evaluate the minimum of a function of the style :
> $$
> \mathbb{E}[ \ e^{|\hat{\theta}-\theta|} + |\hat{\theta}-\theta|^4 \ ]
> $$
> which seems intimidating...
> Using the Theorem we just proved, if we can prove that the conditional expected value $\mathbb{E}[\theta|X]$ is symmetric we are almost done!
> We just need to prove the functions' convexity and symmetry which is much easier...



## Non-Bayesian Parameter Estimation

We can expand the initial term we worked with using the **Law of total expectation** :
$$
\mathbb{E}[ C( \underline{\hat\theta} - \underline\theta ) ] = 
	\mathbb{E}_\theta[
		\mathbb{E}[ C( \underline{\hat\theta} - \underline\theta ) 
		] | \theta
] \underset{\theta - deter.}{=}...
$$
$$
\mathbb{E}[C( \underline{\hat\theta} - \underline\theta )] = 
\int_{\Omega_x}{
	C( \underline{\hat\theta} -\underline\theta )\cdot
	f_{\underline x}(\underline\alpha ; \theta) d\underline\alpha
}
$$
$$
C( \underline{\hat\theta},\underline\theta) :=
( \underline{\hat\theta}-\underline\theta )^2 \implies
\mathbb{E}[( \underline{\hat\theta}-\underline\theta )^2 ] \underset{\underline{\hat\theta}}{\longrightarrow} min \implies \hat\theta_{opt} = 0
$$
- When forcing the condition of Non-biased estimator we often get either high estimation variance , instability of the estimator or both.


> [!example] 
> $$
> x_n = \theta + v_n \ : \ n = 1...N \ , \
> v_n - i.i.d.\ , \
> \mathbb{E}[v_n] = 0\ , \
> Var(v_n) = \sigma^2
> $$
> 
> $$
> \hat\theta_{LS} = 
> \frac{1}{N} \sum_{n=1}^{N}{x_n}
> \ , \ 
> Var(\hat\theta_{LS}) = \frac{\sigma^2}{N}
> \hat\theta_{a} = a \cdot \hat\theta_{LS} 
> $$
> 
> $$
> b(\hat\theta_{a}) = 
> \mathbb{E}[\hat\theta_{a} -\theta] =
> \mathbb{E} [ a \cdot \hat\theta_{LS} - \theta ] =
> (a-1) \theta
> $$
> 
> $$
> MSE(\underline{\hat\theta}) = 
> \mathbb{E}[(\underline{\hat\theta} - \theta) (\underline{\hat\theta} - \theta) ^T]=
> \mathbb{E}[
> (\underline{\hat\theta} - \mathbb{E}[\underline{\hat\theta}]) (\underline{\hat\theta} - \mathbb{E}[\underline{\hat\theta}])^T
> ] +
> \underline{b}(\underline{\hat\theta})\underline{b}(\underline{\hat\theta})^T +
> \mathbb{E}[
> 	(\underline{\hat\theta} - \mathbb{E}[\underline{\hat\theta}]) 
> 	\underline{b}(\underline{\hat\theta})^T
> ]
> \mathbb{E}[
> 	\underline{b}(\underline{\hat\theta})
> 	(\underline{\hat\theta} - \mathbb{E}[\underline{\hat\theta}]) ^T
> ]
> $$
> 
> $$
> \implies MSE(\underline{\hat\theta}) = Cov(\underline{\hat\theta}) + 
> \underline{b}(\underline{\hat\theta})
> \underline{b}(\underline{\hat\theta})^T
> $$
> 
> $$
> \implies MSE(\underline{\hat\theta_a}) = 
> a^2 \cdot \frac{\sigma^2}{N} + (a-1)^2 \cdot \theta^2
> $$
> 
> $$
> \frac{dMSE(\underline{\hat\theta_n})}{da} = 
> \frac{a\sigma^2}{N} + (a-1)\theta^2 = 0
> a_{opt} = \frac{1}{
> 	\frac{\sigma^2}{N\theta^2} + 1
> }\cdot \hat\theta_{Ls}
> $$
> We can see that for adding the bias $a$ the optimal value depends on the estimator itself...
>$$
>MSE(\hat\theta_n) = 
>\frac{1}{
> 	\frac{\sigma^2}{N\theta^2} + 1
> }\frac{\sigma^2}{N} +
> \frac{
> 	\frac{\sigma^2}{N^2}
> }
> {
> 	\frac{\sigma^2}{N\theta^2} + 1
> } \theta^2
>$$ 








