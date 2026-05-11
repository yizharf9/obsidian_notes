
#### Question 1 :
![[Pasted image 20260507184131.png]]
#### a) 
First we examine the statistical model of the observation model : ^81944c

```desmos-graph
left = -2.5
right = 2.5
top = 1
bottom = -0.2
---
a = -1 
b = 0 
c = 1


x = a \{0 < y < 0.25\} | black
x = b \{0 < y < 0.5\} | black
x = c \{0 < y < 0.25\} | black

0 < y < \frac{1}{3*1.4} \{a-0.7 < x < a+0.7\} | blue

0 < y < \frac{1}{3*1.4} \{b-0.7 < x < b+0.7\} | red

0 < y < \frac{1}{3*1.4} \{c-0.7 < x < c+0.7\} | blue

```

#### MAP decision rule

Based on the statistical model we can see that :  ^3fed49
$$
X = \theta + n \implies X \ | \ \theta \sim U[\theta-0.7,\theta+0.7]
$$
- We divide the entire x axis into decision regions.

1. $(x \le -1.7) \lor (1.7 \le x)$ :

	In these regions, the probability of $X$ having values in them is a probability of 0.
	therefore we can choose arbitrarily any decision, we will choose : 
	- $f_{MAP}(x \le -1.7) = -1$
	- $f_{MAP}(1.7 \le x) = 1$

2. $1.7 \le x \le -0.7$ :

	In this region, we can see that the only probable way that $X$ receives a value there is for a give $\theta = -1$ with no intersections for other cases of $\theta$.
	therefore, we can say for certain that the appropriate MAP decision rule is as follows :
	- $f_{MAP}(1.7 \le x \le -0.7) = -1$

3. $0.7 \le x \le 1.7$ :
	For the same consideration as previous section we set the decision rule as follows:
	- $f_{MAP}(0.7 \le x \le 1.7) = 1$

4. $-0.3 \le x \le 0.3$ :
	For the same consideration as the two previous sections we set the decision rule as follows:
	- $f_{MAP}(-0.3 \le x \le 0.3) = 0$


5. $-0.7 \le x \le -0.3$ :
	Now the decision rule is not that straight forward as of before. We will set it using the definition of the MAP decision rule :
	$$
	f_{MAP}(x) = \underset{\theta}{argmax}
	\{ 
	f(x \ | \ \theta)\cdot \mathbb{P}(\theta)
	\}
	$$
	- We can notice right away from the [[#^81944c | Distribution of X]] that in the given region, we get that:$$ f(x \ | \ \theta = -1) = f(x \ | \ \theta = 0) = \frac{1}{1.4}$$
	- Therefore , the only consideration we need to take is in the a-priori probability of $\theta$...
	- Since $\mathbb{P}(\theta = -1) = 0.25 \lt 0.5 = \mathbb{P}(\theta = 0)$ the decision rule is as follows : $$\implies f_{MAP}(-0.7 \le x \le -0.3) = 0$$
6. $0.3 \le x \le 0.7$ :
	For the same considerations as previous section, we can similarly deduce :
	$$ f(x \ | \ \theta = 1) = f(x \ | \ \theta = 0) \ \land \ \mathbb{P}(\theta = 1) = 0.25 \lt 0.5 = \mathbb{P}(\theta = 0)$$
$$\implies f_{MAP}(0.3 \le x \le 0.7) = 0$$

> [!success] Final decision rule
>Overall the complete MAP decision rule is : 
>$$f_{MAP}(x) = \begin{cases}
-1 \quad : x \lt -0.7 \\ 0 \quad : -0.7 \lt x \lt 0.7 \\ 1 \quad : 0.7 \lt x \\
\end{cases}$$

#### MMSE estimator

As we proved in class, we know that the MMSE estimator is defined to be :
$$
\hat{\theta}_{MMSE}(x) = \mathbb{E}[\theta \ | \ x]
$$
We will now derive the explicit expression for this estimator.

- If we expand the definition of the MMSE estimator we get :$$\mathbb{E}[\theta|x] = \sum_{\theta_i}{\theta_i \cdot \mathbb{P}(\theta = \theta_i | x)}$$
- Therefore we need to explicitly derive the term for the conditional probability of $\theta$ based on the **law of total probability** :$$
	\mathbb{P}(\theta | x) = \sum_{\theta \in \{-1,0,1\}}\mathbb{P}(\theta | x)\cdot\mathbb{P(\theta)} 
	$$

We can use **Bayes Theorem** to rearrange the expression of the expected value in question :
$$
\mathbb{P}(\theta|x) = f(x|\theta)\cdot \frac{\mathbb{P}(\theta)}{f(x)}
$$
Now we calculate each term separately based on the statistical model we evaluated earlier.

- $\mathbb{P}(\theta)$ - already given by : 
	$$
	\mathbb{P}(\theta) = 
	\begin{cases}
	0.25 \quad : \theta = \pm1 \\
	0.5 \quad : \theta = 0
	\end{cases}
	$$
- $f(x|\theta)$ - derived earlier in [[#^3fed49| Distribution of X]]  

- $f(x)$ - We will derive the explicit formula using the **Law of total probability** :$$
	f(x) = \sum_{\theta \in \{-1,0,1\}}f(x | \theta)\cdot\mathbb{P(\theta)} 
	$$
	Since we already know the distribution of $x | \theta$  , the full expression comes out to be:
	$$
	f(x) = 
	0.25\cdot f(x|\theta=-1) + 
	0.5\cdot f(x|\theta=0) + 
	0.25\cdot f(x|\theta=1)
	$$
	
	We will examine each case separately :
	
	1. $-1.7<x<-0.7$ - only possible values of $\theta$ is -1 : $$	f(x) = 0.25\cdot f(x|\theta=-1) + 0 + 0  = \frac{0.25}{1.4} \approx 0.179$$
	2. $0.7<x<1.7$ - only possible values of $\theta$ is 1 : $$	f(x) = 0.25\cdot f(x|\theta=1) + 0 + 0  = \frac{0.25}{1.4} \approx 0.179$$
	3. $-0.7<x<-0.3$ - only possible values of $\theta$ is -1,0 : $$	f(x) = 0.25\cdot f(x|\theta=-1) + 0.5\cdot f(x|\theta=0) + 0  = \frac{0.25 + 0.5}{1.4} \approx 0.536$$
	4. $0.3<x<0.7$ - only possible values of $\theta$ are 0,1 : $$	f(x) = 0.25\cdot f(x|\theta=1) + 0.5\cdot f(x|\theta=0) + 0  = \frac{0.25 + 0.5}{1.4} \approx 0.536$$
	5. $-0.3<x<0.3$ - only possible values of $\theta$ is 0 : $$	f(x) = 0.5\cdot f(x|\theta=0) + 0 + 0  = \frac{0.5}{1.4} \approx 0.357$$
	Overall we get the explicit expression for the conditional probability density :$$
	f(x) = \frac{1}{1.4} \cdot
	\begin{cases}
	0 \quad : |x| \ge 1.7 \\
	0.25 \quad : 0.7 \le |x| < 1.7 \\
	0.75 \quad : 0.3 \le |x| < 0.7 \\
	0.5 \quad :  |x| \le 0.3 \\
	\end{cases}
	$$
- Now we have all terms of the conditional probability in question. We will cacluate the required expected value term : 
	$$
	\hat{\theta}_{MMSE}(x) = 
	\mathbb{E}[\theta|x] = 
	\sum_{\theta_i}{\theta_i \cdot \mathbb{P}(\theta = \theta_i | x)} = \dots
	$$
	$$
	\dots = 
	-1 \cdot \mathbb{P}(\theta=-1 | x ) + 
	0 \cdot \mathbb{P}(\theta=-1 | x ) + 
	1 \cdot \mathbb{P}(\theta=1 | x ) =
	$$
	$$
	\dots = \mathbb{P}(\theta=1 | x ) - \mathbb{P}(\theta= -1 | x ) =
	 \mathbb{P}(\theta = 1)\cdot \frac{f(x|\theta = 1)}{f(x)} - 
	 \mathbb{P}(\theta = -1)\cdot \frac{f(x|\theta = -1)}{f(x)} = \dots
	$$
	$$
	\dots = 0.25 \cdot [ 
	\frac{f(x|\theta = 1) - f(x|\theta = -1)}{f(x)}
	] = \dots 
	$$
	For convenience, we denoted : $\mathbb{1}_{x\in [a,b]} = \begin{cases}1 \quad : x\in[a,b] \\ 0 \quad  : else\end{cases}$
	$$
	\implies \hat{\theta}_{MMSE}(x) = 
	0.25 \cdot [ 
	\frac{f(x|\theta = 1) - f(x|\theta = -1)}{f(x)}
	] =
	0.25 \cdot [ 
	\frac
	{\mathbb{1}_{x\in [0.3,1.7]} - \mathbb{1}_{x\in [-1.7,-0.3]}}
	{f(x)}
	] 
	$$
	

> [!success] result
> We get the final expression for the MMSE estimator :
> $$
> \implies \hat{\theta}_{MMSE}(x) =\begin{cases}
> 1.4 \quad : 0.7 < |x| <1.7 \\
> \frac{7}{15} \quad : 0.3 < |x| < 0.7 \\
> 0 \quad \quad : |x| < 0.3 \\
> Undefined \quad : 0.3 < |x| < 0.7 \\
> \end{cases}
> $$

### b)
