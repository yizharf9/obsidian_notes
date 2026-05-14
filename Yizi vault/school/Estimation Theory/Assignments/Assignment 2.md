
## Question 1 :

![[Pasted image 20260507184131.png]]

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

n = 0.7

x = a \{0 < y < 0.25\} | black
x = b \{0 < y < 0.5\} | black
x = c \{0 < y < 0.25\} | black

0 < y < \frac{1}{3*2*n} \{a-n < x < a+n\} | blue

0 < y < \frac{1}{3*2*n} \{b-n < x < b+n\} | red

0 < y < \frac{1}{3*2*n} \{c-n < x < c+n\} | blue

x = a + n | magenta | dashed
(a+n,0) | label: -0.3 | magenta

x = b - n | magenta | dashed
(-n,0) | label: -0.7 | magenta

x = b + n | magenta | dashed
(n,0) | label: 0.7 | magenta

x = c - n | magenta | dashed
(c-n,0) | label: 0.3 | magenta

```

Based on the statistical model we can see that :  ^3fed49
$$
X = \theta + n \implies X \ | \ \theta \sim U[\theta-0.7,\theta+0.7]
$$
### a) Deriving Estimators
#### MAP decision rule

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

> [!success] result
>Overall the complete MAP decision rule is : 
>$$\theta_{MAP}(x) = \begin{cases}
-1 \quad : x \lt -0.7 \\ 0 \quad : -0.7 \lt x \lt 0.7 \\ 1 \quad : 0.7 \lt x \\
\end{cases}$$

^e8993c

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
	$$ ^7f5859
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
	 ^f2f3ff

> [!success] result
> We get the final expression for the MMSE estimator :
> $$
> \implies \hat{\theta}_{MMSE}(x) = sign(x) \cdot \begin{cases}
> 1 \quad : 0.7 < |x| <1.7 \\
> \frac{1}{3} \quad : 0.3 < |x| < 0.7 \\
> 0 \quad \quad : |x| < 0.3 \\
> Undefined \quad : 1.7 < |x| \\
> \end{cases}
> $$

^bb5352

### b) Error Probability

We will calculate the error of probability for each of the estimators based on the definition :
$$
P_e(\hat{\theta}) =
\mathbb{P}(\hat{\theta}(x) \ne \theta) = 
\sum_{\theta}{\mathbb{P}(error|\hat{\theta}(x) = \theta|x)\cdot}\mathbb{P}(\theta)
$$
#### MAP decision rule

![[Assignment 2#^e8993c| derived expression for MAP desision rule]]

We will examine in which values of $x$ the estimator has an error.
We notice that the cases in which that is possible are the overlapping domains :

1. $-0.7 \le x \le -0.3$ :
	$\mathbb{P}(error|\hat{\theta}_{MAP}(x) = -1) = \mathbb{P}(-0.7 \le x \le -0.3)$ :
		In this case, the estimator will prefer the value $\theta = 0$ because of the higher a-priori probability every time and ignore the cases of $\theta = -1$ :
		$$
		(X | \theta = -1) \sim U[-1.7,-0.3] 
		$$
		$$
		\implies 
		\mathbb{P}(-0.7 \le x \le -0.3) = \int_{-0.7}^{-0.3}{\frac{1}{1.4}dx} = \frac{1}{1.4} \cdot(-0.3 -(-0.7)) = \frac{2}{7}
		$$

2. $0.3 \le x \le 0.7$ :
	$\mathbb{P}(\hat{\theta}_{MAP}(x)\ne \theta|x) = \mathbb{P}(0.3 \le x \le 0.7) \cdot \mathbb{P}(\theta = 1)$ :
		Similarly to previous case, the estimator will prefer the value $\theta = 0$ because of the higher a-priori probability every time and ignore the cases of $\theta = 1$ :
		$$
		(X | \theta = 1) \sim U[0.3,1.7] 
		$$
		$$
		\implies 
		\mathbb{P}(0.3 \le x \le 0.7) = \int_{0.3}^{0.7}{\frac{1}{1.4}dx} = \frac{1}{1.4} \cdot(0.7-0.3) = \frac{2}{7}
		$$

> [!fail] Error Probability
> Overall, we get a total error probability :
> $$
> P_e(\hat{\theta}_{MAP}) =
> P_e(-0.7 \le x \le -0.3)\mathbb{P}(\theta = -1) +
> P_e(0.3 \le x \le 0.7)\mathbb{P}(\theta = 1) 
> $$
> $$
>  = 0.25 \cdot \frac{2}{7} + 0.25 \cdot \frac{2}{7} = \frac{1}{7}
> $$
> The error stems from the preference of the estimator to the highest a-priori probability.
> The higher that probability is for the center value $\theta = 0$ the more justified that decision is and the probability of error will go lower.


#### MMSE estimator
![[#^bb5352 | derived expression for MMSE estimator]]


As of before, we examine for which values of $x$ the estimator has an error.
We notice that the cases in which that is possible are the cases in which the estimator returns values of $\theta$ that are not feasible.

- We can notice that the only interval in which the estimator returns a non-feasible value of $\theta$ is $0.3 \lt |x| \lt 0.7$ where the estimator is incorrect.
- For all other intervals, the estimator returns the correct value (due to no overlap in other regions...)

We will calculate the error of probability for the region $0.3 \lt |x| \lt 0.7$ :
$$
P_e = 
\mathbb{P}(0.3 \le |x| \le 0.7) \cdot \mathbb{P}(\theta = -1,0,1) =
$$
$$
= \mathbb{P}(-0.7 \le x \le -0.3) \cdot \mathbb{P}(\theta = -1) +
\mathbb{P}(0.3 \le x \le 0.7) \cdot \mathbb{P}(\theta = 1) +
\mathbb{P}(0.3 \le |x| \le 0.7) \cdot \mathbb{P}(\theta = 0) =
$$
$$
= 0.25 \cdot \int_{-0.7}^{-0.3}{\frac{1}{1.4}dx} +
0.25 \cdot \int_{0.3}^{0.7}{\frac{1}{1.4}dx} +
2\cdot 0.5 \cdot \int_{0.3}^{0.7}{\frac{1}{1.4}dx}  =
$$
$$
= (\frac{1}{1.4} \cdot (0.7-0.3) ) \cdot (2\cdot 0.25 + 2\cdot 0.5) = 1.5 \cdot \frac{2}{7}
$$


> [!fail] Error Probability 
> We get a total error probability of :
>$$
>\implies P_e = \frac{3}{7}
>$$
>The error stems entirely from the fact that the estimator returns values that are not feasible in almost every region and not from incorrect choices.

### c) - perform a)+b) again for different distribution

In contrast to the initial distribution of $X$ we get a new distribution :

```desmos-graph
left = -2.5
right = 2.5
top = 1
bottom = -0.2
---
a = -1 
b = 0 
c = 1

n = 0.5

x = a \{0 < y < 0.25\} | black
x = b \{0 < y < 0.5\} | black
x = c \{0 < y < 0.25\} | black

0 < y < \frac{1}{3*1.4} \{a-n < x < a+n\} | blue

0 < y < \frac{1}{3*1.4} \{b-n < x < b+n\} | red

0 < y < \frac{1}{3*1.4} \{c-n < x < c+n\} | blue

x = a + n | magenta | dashed
(-0.3,0) | label: -0.3 | magenta

x = b - n | magenta | dashed
(-n,0) | label: -0.7 | magenta

x = b + n | magenta | dashed
(n,0) | label: 0.7 | magenta

x = c - n | magenta | dashed
(0.3,0) | label: 0.3 | magenta

```

Now we can clearly see that there is no overlap between the intervals.
We will re-examine the estimators :

#### New - MAP decision rule

- Since we now have now overlap, the MAP rule will not have to prioritize different values of $\theta$ over each other.
- In each interval, the choice that maximizes the PDF in the interval is a singular value which is the correct estimation.
- The new MAP estimator will be :
	$$\theta_{MAP}(x) = \begin{cases}
	-1 \quad : x \lt -0.5 \\
	0 \quad : -0.5 \lt x \lt 0.5 \\
	1 \quad : 0.5 \lt x \\
	\end{cases}$$

- The new error probability will be 0, since in every cases the only choice is the correct one :
	$$P_e(\hat{\theta}_{MAP}) = 0 $$

#### New - MMSE estimator

- Since the only change in the statistical properties of the problem is the change in the intervals in which $x$ can land in, the derivation for the expected value needs only that adjustment :

- First we will derive the new PDF $f(x)$ :
	1. $-1.5<x<-0.5$ - only possible values of $\theta$ is -1 : $$	f(x) = 0.25\cdot f(x|\theta=-1) + 0 + 0  = \frac{0.25}{1} = 0.25 $$
	2. $-0.5<x<0.5$ - only possible values of $\theta$ is 0 : $$	f(x) = 0.5\cdot f(x|\theta=0) + 0 + 0  = \frac{0.5}{1} = 0.5 $$
	3. $0.5<x<1.5$ - only possible values of $\theta$ is 1 : $$	f(x) = 0.25\cdot f(x|\theta=1) + 0 + 0  = \frac{0.25}{1} = 0.25 $$
	Overall, we get the new PDF :
	$$
	f(x) =
	\begin{cases}
	0 \quad : |x| \ge 1.5 \\
	0.25 \quad : 0.5 \le |x| < 1.5 \\
	0.5 \quad :  |x| \le 0.5 \\
	\end{cases}
	$$
- We substitute the PDF back to our derived expression for the expected value with new intervals of interest :
	$$
	\implies \hat{\theta}_{MMSE}(x) = 
	0.25 \cdot [ 
	\frac{f(x|\theta = 1) - f(x|\theta = -1)}{f(x)}
	] =
	0.25 \cdot [ 
	\frac
	{\mathbb{1}_{x\in [0.5,1.5]} - \mathbb{1}_{x\in [-1.5,-0.5]}}
	{f(x)}
	] 
	$$
- We get the new derivation for the MMSE estimator :
	$$
	\implies \hat{\theta}_{MMSE}(x) = sign(x) \cdot \begin{cases}
	1 \quad \quad  : 0.5 < |x| <1.5 \\
	0 \quad \quad : |x| < 0.5 \\
	Undefined \quad : 1.5 < |x| \\
	\end{cases}
	$$
- We notice that the MMSE doesn't have any intervals in which he has to average between possible values and therefore only factor in the true value of $\theta$.

- We also notice that the new MMSE estimator is identical to the new MAP estimator and therefore, also has an error probability of 0 : 
	$$P_e(\hat{\theta}_{MMSE}) = 0$$

## Question 2

![[Pasted image 20260512203214.png]]

### a) Find MMSE Estimator

- We will find the MMSE estimator based on definition :
$$
\hat{\theta}_{MMSE}(N) = \mathbb{E}[\theta|N]
$$

- We will expand the expected value term by definition :
$$
\mathbb{E}[\theta|N] = \int_{0}^{\infty}{\alpha}\cdot f_{\theta|N=k}(\alpha)d\alpha
$$
- We are given the distribution of $\theta$ by :
$$
\theta \sim exp(\lambda)
$$
- We want to find the distribution of the R.V. $\theta|N$, so we will use Bayes theorem :
$$
f_{\theta}(\alpha | N = k) = 
\frac{
	\overbrace{\mathbb{P}(N = k|\theta=\alpha)}^{\sim Poi(\alpha)}
	\cdot
	\overbrace{f_{\theta}(\alpha)}^{\sim exp(\lambda)}
}{
\mathbb{P}(N=k)
}
$$
- Since we know all terms in the RHS but $\mathbb{P}(N)$, we will find that term to substitute back in :
	We will use the **Law of Total Probability** to express the term in question :
	$$
	\mathbb{P}(N = k) = 
	\int_0^{\infty}{
		\mathbb{P}(N = k|\theta = \alpha) \cdot
		f_{\theta}(\alpha)d\alpha
	}=
	\int_0^{\infty}{
		\frac{\alpha^k}{k!}e^{-\alpha} \cdot
		\lambda e^{-\lambda\alpha}d\alpha
	}=
	\int_0^{\infty}{
		\lambda \cdot \frac{\alpha^k}{k!} \cdot
		 e^{-\alpha (\lambda+1) }d\alpha
	}=\dots
	$$
	- We will use the identity we were given for the following integral :
	$$
	\dots =
	\frac{\lambda}{k!} \cdot
	 \int_0^{\infty}{
		 \alpha^k \cdot
		 e^{-\alpha (\lambda+1) }d\alpha
	}=\frac{\lambda}{k!} \cdot
	 \underbrace{\int_0^{\infty}{
		 \alpha^k \cdot
		 e^{-\alpha (\lambda+1) }d\alpha
	}}_{identity}=\frac{\lambda}{\not{k!}} \cdot \frac{\not{k!}}{(\lambda+1)^{k+1}}=
	\frac{\lambda}{(\lambda+1)^{k+1}}
	$$ ^46194c
- Now we have all terms so we can substitute them in :
$$
f_{\theta}(\theta = \alpha | N = k) = 
\frac{
	\frac{\alpha^k}{k!}e^{-\alpha} \cdot 
	\not{\lambda} e^{-\lambda\alpha}
}
{
	\frac{\not{\lambda}}{(\lambda+1)^{k+1}}
}=
\frac{(\lambda+1)^{k+1} \cdot \alpha^k}{k!} \cdot e^{-\alpha(\lambda+1)}
$$ ^6b0cb7
- We can now calculate the expected value in question :
$$
\mathbb{E}[\theta|N] = \int_{0}^{\infty}{
	\alpha^{k+1} \cdot \frac{(\lambda+1)^{k+1}}{k!} \cdot 
	e^{-\alpha(\lambda+1)} d\alpha
}=
 \frac{(\lambda+1)^{k+1}}{k!} \cdot 
\underbrace{\int_{0}^{\infty}{
	\alpha^{k+1} \cdot e^{-\alpha(\lambda+1)} d\alpha
}}_{
	m = k + 1 \ , \ \alpha' = (\lambda + 1)
}=\dots 
$$
$$
\dots=
\frac{
	{m!}
}{\alpha^{m+1}} =
\frac{
(\lambda+1)^{\overbrace{\cancel{k+1}}^{-1}}
}{\cancel{k!}} \cdot 
\frac{
	\overbrace{\cancel{(k+1)!}}^{k+1}
}{(\cancel{\lambda+1)^{k+2}}} =
\frac{k+1}{\lambda + 1}
$$

> [!success] result
> We get the derivation of the MMSE estimator :
> $$\implies \hat\theta_{MMSE} (N) =  \mathbb{E}[\theta|N=k] = \frac{k+1}{\lambda + 1}$$

### b) Find MAP estimator

We will derive the MAP estimator based on the definition :
$$
\hat\theta_{MAP}(N) = 
\underset{\alpha \in \mathbb{R}}{argmax}\{
	f_{\theta|N}(\alpha)
\}
$$
- Since we have already derived the conditional PDF in a) :
$$
f_{\theta}(\theta = \alpha | N = k) = 
\frac{(\lambda+1)^{k+1} \cdot \alpha^k}{k!} \cdot e^{-\alpha(\lambda+1)}
$$
- We can take the derivative with respect to $\alpha$ and compare to 0 :
$$
\frac{df_{\theta}(\theta = \alpha | N = k)}
{d\alpha} =
\frac{(\lambda+1)^{k+1}}{k!}\cdot
\begin{bmatrix}
k\alpha^{k-1}\cdot e^{-\alpha(\lambda+1)} -
(\lambda + 1)\alpha^{k}\cdot e^{-\alpha(\lambda+1)}
\end{bmatrix}=\dots
$$
$$
\frac{(\lambda+1)^{k+1}}{k!} \cdot
e^{-\alpha(\lambda+1)} \cdot 
\alpha^{k-1}\cdot
\begin{bmatrix}
k  -
\alpha\cdot (\lambda + 1) 
\end{bmatrix}= 
\begin{cases}
\alpha = 0 \\
\alpha = \frac{k}{\lambda +1}
\end{cases}
\implies
$$
- We notice that in the value $\alpha = 0$ the PDF value is 0, so it must be a minimum...
- Which means that $\alpha = \frac{k}{\lambda+1}$ is the only possible maximum and therefore :


> [!success] result
> We get the final derivation of the MAP estimator
> $$\hat\theta_{MAP}(N) = \underset{\alpha \in \mathbb{R}}{argmax}\{f_{\theta|N}(\alpha)\} = \frac{k}{\lambda +1}$$

```desmos-graph
top = 2
bottom = -0.2
left = -0.2
right = 3
---
l = 5
k = 5

y = (l+1)^{k+1}  x^k  e^{ -x*(l+1) } / k! \{ 0 < x \}

x = (k+1)/(l+1) | black | dashed
( (k+1)/(l+1) , 0 ) | Label: MMSE

x = k/(l+1) | red | dashed
( (k)/(l+1) , 0 ) | red | Label: MAP

x = 0 | blue | dashed
```

> [!Warning] Notice...
> The two estimators are not identical!
>That is because the MAP estimator is showing the **Mode** of the posterior distribution  
>while the MMSE estimator is showing the **Mean** of the posterior distribution.
>These two are not identical since the distribution is **not symmetric**!


## Question 3

![[Pasted image 20260513203611.png]]
![[Pasted image 20260513203630.png]]

- Distribution of $\theta$ :
$$
\theta \sim U[a,b] \implies
f_{\theta}(\alpha) = \begin{cases}
\frac{1}{b-a} \quad : \alpha \in [a,b] \\
0 \quad : else \\
\end{cases}
$$
- Conditional distribution of $y_n | \theta$ :

$$
y_n | \theta \sim U[0,\theta] \implies
f_{y_n|\theta}(z) = \begin{cases}
\frac{1}{\theta} \quad : z \in [0,\theta] \\
0 \quad : else \\
\end{cases}
$$
### a) Find MAP estimator

For finding the MAP estimator  we need to find the term :
$$
\hat\theta(\underline{y}) = 
\underset{\alpha \in [a,b] }{argmax}\{
f_{\underline{y}|\theta=\alpha}(z) \cdot f_\theta(\alpha)
\}
\ : \ \underline{y} := \begin{pmatrix}
y_1 \\
\vdots \\
y_n
\end{pmatrix}
$$

- We notice that $f_\theta(\alpha)$ is constant so we can omit it from the argument.
- We examine the conditional distribution that to maximize the value of the PDF we would like to choose the value of $\theta$ as smallest as possible. For that , we need to determine what is the smallest legitimate value of $\theta$ we can choose based on the data samples $\{y_n\}_{n=1}^N$. 
- We denoted the max value of the data samples : $Y_{max}=max\{y_n\}_{n=1}^N$ 
- We examine each case separately :
	1. If $Y_{max} \le a$ :
		That means that we can choose the smallest possible value for $\theta$ which is the lower bound of its uniform distribution. $$\implies \hat\theta_{MAP}(\underline{y}) = a$$
	2. If $Y_{max} \gt a$ :
		That means the new value is the best possible candidate for $\theta$. Choosing any lower value is like stating that the maximum value of the data samples is lower than the new sample we just got which is a contradiction. Choosing any value higher will yield a lower value of the PDF which serves us no purpose.$$\implies \hat\theta_{MAP}(\underline{y}) = Y_{max}$$

> [!success] Result
> Overall, we get the final MAP estimator :
>$$
>\hat\theta_{MAP}(\underline{y}) = max\{a,\underset{1\le n \le N}{max}\{y_n\}\}
>$$
>

- To derive the bias of the estimator we first define the distribution of the estimator. For that we will take the derivative of the CDF of the estimator by the definition :
$$
F_{\hat\theta_{MAP}}(t) = 
\mathbb{P}(\hat\theta_{MAP} \le t) = 
\mathbb{P}(max\{a,Y_{max}\} \le t) = \dots
$$
$$
max\{a,Y_{max}\} \le t \implies (y_1\le t)\land \dots \land (y_N\le t)\land (a \le t)
$$
- We separate to 2 different cases :
	1. $t \le a$  : 
		In this case, the estimator will choose the value $a$ anyway so the probability it will land below it is 0 and we have a spike in the value $t = a$ in which the accumulated probability of all lower values of $t$ are packed in that value :
$$
F_{\hat\theta_{MAP}}(t) = 
\mathbb{P}(max\{a,Y_{max}\} \le t) =
\mathbb{1}_{a \le t}(t) \cdot \mathbb{P}(Y_{max} \le t) =
\mathbb{1}_{a \le t}(t) \cdot \prod_{n=1}^N{ \mathbb{P}(y_n \le t) } =
$$
$$
\dots = \mathbb{1}_{a \le t}(t) \cdot \prod_{n=1}^N{\int_0^a{\frac{1}{\theta}} dt} = 
\mathbb{1}_{a \le t}(t) \cdot \prod_{n=1}^N{\frac{a}{\theta}} = 
\mathbb{1}_{a \le t}(t) \cdot (\frac{a}{\theta})^N  
$$
$$
\overset{\frac{d}{dt}}{\implies} f_{\hat\theta_{MAP}}(t) = 
\delta(t-a)\cdot(\frac{a}{\theta})^N 
\ : \ t \le a
$$
	2. $a \lt t$ :
		In this case the estimator will choose the max value between the data samples :
$$
F_{\hat\theta_{MAP}}(t) = 
\mathbb{P}(max\{a,Y_{max}\} \le t) =
\mathbb{P}(a \le Y_{max} \le t) =
\prod_{n=1}^N{\mathbb{P}(a \le y_n \le t)} =
\prod_{n=1}^N{ \int_a^t{ \frac{1}{\theta} dt} } = \dots
$$
$$
\dots = \prod_{n=1}^N{ \int_a^t{ \frac{1}{\theta} dt} } = 
\prod_{n=1}^N{ \frac{t-a}{\theta} } = 
(\frac{t-a}{\theta})^{N}
$$
$$
\overset{\frac{d}{dt}}{\implies} f_{\hat\theta_{MAP}}(t) = 
N \cdot (\frac{t-a}{\theta})^{N-1}
\ : \ a \lt t
$$

- Now we have the PDF of the distribution so we can derive the bias :
$$
b(\hat\theta_{MAP}) = \mathbb{E}[\hat\theta_{MAP} - \theta] = \mathbb{E}[\hat\theta_{MAP}] - \frac{a+b}{2}
$$
$$
\mathbb{E}[\hat\theta_{MAP}] = 
\int_\mathbb{R}{t\cdot f_{\hat\theta_{MAP}}(t)dt} =
\int_0^a{t \cdot \delta(t-a)\cdot (\frac{a}{\theta})^N dt} +
\int_a^\theta{t \cdot \frac{t^{N-1}}{\theta^N} \cdot Ndt} = \dots
$$
$$
\dots = \frac{a^{N+1}}{\theta^N} +
\frac{N}{\theta^N} \cdot \left. \frac{t^{N+1}}{N+1}\right|_a^\theta =
\frac{a^{N+1}}{\theta^N} +
\frac{N}{N+1} \cdot(\frac{\theta^{\cancel{N+1}}}{\cancel{\theta^N}} - 
\frac{a^{N+1}}{\theta^N})= \dots
$$
$$
\dots =
\overbrace{
	\cancel{\frac{1}{N+1} \cdot \frac{a^{N+1}}{\theta^N}}
}^{N \to \infty} +
\overbrace{
	{\frac{N}{N+1}}
}^{\underset{N \to \infty}{\longrightarrow}1}
\cdot \theta
\underset{N\to \infty}{\longrightarrow} \theta
$$
$$
\implies \lim_{N\to \infty }{b(\hat\theta_{MAP})} = \theta - \theta = 0
$$

> [!success] Result
> We find that the estimator is **asymptotically unbiased** : $b(\hat\theta_{MAP})\overset{a}{\approx} 0$

### b) Find MED estimator

We want to find the median estimator :
$$
\hat\theta_{MED}(\underline{y}) = \underset{\theta}{median}\{ f_{\theta|\underline{y}}(\theta|x) \}
$$
