
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

^40fce9

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
^743bd2
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
\hat\theta_{MED}(\underline{y}) = \underset{\theta}{median}\{ f_{\theta|\underline{y}}(\theta|\underline y) \}
$$
- We will use Bayes Theorem to derive the expression for the conditional PDF :
$$
f_{\theta | \underline y}(\alpha | \underline y) = 
\frac{
	f_{\underline y | \alpha }(\underline \beta | \alpha ) \cdot 
	f_{\theta} (\alpha) 
}{
	f_{\underline y}(\underline \beta)
}
$$
- Since $f_{\underline y }(\underline \beta)$ is independent of $\alpha$, we can assume that for a given sample vector $\underline y$ , it is a constant and therefore :
$$
f_{\theta | \underline y}(\alpha | \underline y) = 
c \cdot 
[f_{\underline y | \alpha }(\underline \beta | \alpha ) \cdot 
f_{\theta} (\alpha) ] 
\ : \ c \in \mathbb{R}
$$
- We can calculate $c$ using the definition of the marginal distribution and the PDFs we already know :
$$
\int_{\mathbb{R}}f_{\theta | \underline y}(\alpha | \underline \beta) {d}\alpha = 
c \cdot \int_{\mathbb{R}} f_{\underline y | \theta}(\underline\beta | \alpha) \cdot 
f_{\theta}(\alpha) d\alpha = 
c \cdot \int_{L}^{b} \frac{1}{\alpha^N} \cdot 
\frac{1}{b-a} d\alpha = 
$$
$$
\dots = \frac{c}{b-a} \cdot \left. \frac{\alpha^{-N+1}}{-N+1} \right|_{L}^{b} = 1
: L := max\{a,Y_{max}\} 
$$
$$
\implies \frac{c}{b-a} \cdot
\left[
\frac{b^{-N+1}}{-N+1} - 
\frac{L^{-N+1}}{-N+1}
\right] = 1 \implies
c = (b-a) \cdot 
\left[
\frac{b^{-N+1}}{-N+1} - 
\frac{L^{-N+1}}{-N+1}
\right]^{-1}
$$
$$
\implies f_{\theta | \underline y } (\alpha | \underline \beta) = 
c \cdot 
\frac{1}{\alpha ^ N} \cdot \frac{1}{b-a} =
\left[
\frac{b^{-N+1}}{-N+1} - 
\frac{L^{-N+1}}{-N+1}
\right]^{-1}
\cdot \frac{1}{\alpha^N} \implies f_{\theta | \underline y } (\alpha | \underline \beta) =  K \cdot \alpha^{-N}
$$
- Now we want to find the median estimator based on the definition :
$$
\int_L^{\hat\theta_{MED}}{
	f_{\theta|\underline y} (\alpha | \underline \beta) d\alpha = 0.5
}
\implies 
K \cdot \int_L^{\hat\theta_{MED}}{
	\alpha ^ {-N} d\alpha = 0.5
}
\implies 
K \cdot \left. \frac{\alpha ^ {-N+1}}{-N+1} \right|_{L}^{\hat\theta_{MED}} = 0.5
$$
$$
\implies
\frac{(\hat\theta_{MED})^{-N+1}}{-N+1} =
\frac{0.5}{K} + 
\frac{L^{-N+1}}{-N+1} 
\implies
(\hat\theta_{MED})^{-N+1} =
\frac{0.5(-N+1)}{K} + 
L^{-N+1}
$$
$$
\implies
\hat\theta_{MED} =
\left(\frac{0.5(-N+1)}{K} + 
L^{-N+1}\right)^{\frac{1}{-N+1}}
\implies
\hat\theta_{MED} =\left(
	\frac{b^{-N+1} + L^{-N+1}}{2}
\right)^{\frac{1}{-N+1}}
$$

> [!success] Result
> We get the expression for the MED estimator :
> $$
> \hat\theta_{MED} =\left(\frac{b^{-N+1} + L^{-N+1}}{2}\right)^{\frac{1}{-N+1}}
> : L := max\{a,Y_{max}\}
> $$

### c) conclusion

From derivations and proofs performed in class, we know that the optimal estimator in terms of the Minimum Average Error $MAE(\hat\theta,\theta) := |\theta - \hat\theta| = C(\hat\theta , \theta)$ is the median estimator and therefore the second estimator yields a smaller cost respectively :


> [!success] Conclusion
> $$
> \mathbb{E}[C(\hat\theta_{MED},\theta)] \le \mathbb{E}[C(\hat\theta_{MAP},\theta)]
> $$


## Question 4

![[Pasted image 20260517161523.png]]

- Statistical model :
$$
\underline{x} = \underline {\underline H} \cdot \underline \theta + \underline v
$$
$$
H \in \mathbb{R}^{N \times M} : Rank(HCH^T + \sigma_v^2 \cdot I_N)  = N
$$
$$
\underline v \in \mathbb{R}^{N} \sim \mathcal{N}(0,\sigma_v^2 \cdot I)
$$
$$
\underline\theta \in \mathbb{R}^{M} \sim \mathcal{N}(\underline\mu,C)
$$
### a) Find MMSE estimator

Since the parameter vector $\underline \theta$ is non-deterministic and holds a prior, known statistical model, we want to use a joint-gaussian model of the parameters and the data samples.

- We will denote $\varepsilon_\theta$ as the error of the estimation of the parameters $\theta$.
- We would like to have a statistical model that estimates some deterministic vector $\tilde\theta$ so we denote :
$$
\underline\mu = \underline\theta + \underbrace{(\underline\mu-\underline\theta)}_{\underline{\varepsilon}_\theta} 
$$
- We quickly notice that :
$$
\mathbb{E}[\underline{\varepsilon}_{\theta}] = 0 , \ : \ Cov(\underline{\varepsilon}_{\theta}) = Cov(\underline\theta) = C
$$
- We build the following equation based on the definition of $\underline{\varepsilon}_\theta$ and the prior statistical model of the data samples $\underline x$  to get :
$$
\underbrace{
	\begin{pmatrix}
	\underline x \\
	\underline \mu \\
	\end{pmatrix}
}_{\underline{\tilde{x}}\in \mathbb{R}^{N+M}}
=
\underbrace{
	\begin{pmatrix}
	H \\
	\mathbb{I}_M \\
	\end{pmatrix}
}_{\tilde{H} \in \mathbb{R}^{(N+M)\times M} } \cdot \underline \theta 
+
\underbrace{
	\begin{pmatrix}
	\underline v \\
	\underline{\varepsilon_\theta} \\
	\end{pmatrix}
}_{\underline{\tilde{v}} \in \mathbb{R}^{N+M}}
$$
- We get a new statistical model for the data samples vector :
$$
\implies 
\underline{\tilde x} = \tilde H \cdot \underline\theta + \underline{\tilde v}
$$
- Now, since the prior of the parameters $\underline\theta$  are taken in consideration in the new model, we can use the WLS solution for the MMSE estimator :
$$
\hat\theta_{WLS}(\tilde{\underline x}) = 
(\tilde H^TW \tilde H)^{-1}
\tilde H^TW \cdot \tilde{\underline x} 
$$
- Since we have already proven in class that $W^* = \tilde R ^{-1}$ we need to find the correlation matrix of the newly constructed noise vector $\tilde{\underline v}$ :
$$
\tilde R = 
\mathbb{E}[\tilde{\underline v} \cdot \tilde{\underline v}^T] = 
\left\{ 
	\tilde{\underline{v}} := 
	\begin{pmatrix}
		\underline v \\
		\underline{\underline \varepsilon} \\
	\end{pmatrix}
\right\} =
\begin{pmatrix}
		\sigma_v^2 \cdot \mathbb{I}_N \quad  \ \mathbb{0} \\
		\mathbb{0} \quad\quad\quad   \  C \\
\end{pmatrix}
$$
$$
\implies \tilde R^{-1} =
\begin{pmatrix}
		\frac{1}{\sigma_v^2} \cdot \mathbb{I}_N \quad  \ \mathbb{0} \\
		\mathbb{0} \quad\quad\quad   \  C^{-1} \\
\end{pmatrix}
$$
- We plug in the result for said correlation matrix to the definition of the WLS solution :
$$
\hat\theta_{WLS}(\tilde{\underline x}) = 
(\begin{pmatrix}
	H^T \ , \
	\mathbb{I}_M \\
	\end{pmatrix}
\begin{pmatrix}
		\frac{1}{\sigma_v^2} \cdot \mathbb{I}_N \quad  \ \mathbb{0} \\
		\mathbb{0} \quad\quad\quad   \  C^{-1} \\
\end{pmatrix}
\begin{pmatrix}
	H \\
	\mathbb{I}_M \\
	\end{pmatrix})^{-1}
\begin{pmatrix}
	H^T \ , \
	\mathbb{I}_M \\
	\end{pmatrix}
\begin{pmatrix}
		\frac{1}{\sigma_v^2} \cdot \mathbb{I}_N \quad  \ \mathbb{0} \\
		\mathbb{0} \quad\quad\quad   \  C^{-1} \\
\end{pmatrix}
\cdot \tilde{\underline x} 
$$
$$
\implies \hat\theta_{WLS}(\tilde{\underline x}) = 
(\begin{pmatrix}
	H^T \ , \
	\mathbb{I}_M \\
	\end{pmatrix}
\begin{pmatrix}
	\frac{1}{\sigma_v^2} H \\
	C^{-1}
	\end{pmatrix})^{-1}
\begin{pmatrix}
	H^T \ , \
	\mathbb{I}_M \\
	\end{pmatrix}
\begin{pmatrix}
		\frac{1}{\sigma_v^2} \cdot \mathbb{I}_N \quad  \ \mathbb{0} \\
		\mathbb{0} \quad\quad\quad   \  C^{-1} \\
\end{pmatrix}
\cdot \tilde{\underline x} = 
$$
$$
= (H^T \frac{1}{\sigma_v^2} H  + C^{-1})^{-1} \cdot 
(H^T , \mathbb{I}_M) \cdot (\frac{1}{\sigma_v^2}\underline{x} ,C^{-1}\underline\mu)^T = (H^T \frac{1}{\sigma_v^2} H  + C^{-1})^{-1} \cdot 
(\frac{1}{\sigma_v^2} \cdot H^T \cdot \underline x + C^{-1}\underline\mu)
$$


> [!success] Result
> Overall, we get the final MMSE estimator :
> $$\hat\theta_{WLS}(\underline x , \underline \mu ) = (H^T \frac{1}{\sigma_v^2} H  + C^{-1})^{-1} \cdot 
(\frac{1}{\sigma_v^2} \cdot H^T \cdot \underline x + C^{-1}\underline\mu)$$


### b) Estimate Of $\varphi = h_0^T \cdot \theta$ 

Now, we are required to estimate a function of the linear combination of the parameters.

- First we look at the target expression that we want to derive :
$$
\hat{(\varphi^2)}_{MMSE}(\tilde x) = \mathbb{E}[\varphi^2 | \tilde x]
$$
- We Manipulate the definition of the Variance of the R.V. $\varphi^2|x$ :
$$
Var(\varphi^2 | x ) = \mathbb{E}[\varphi^2 | x ] - \mathbb{E}[\varphi|x]^2
\implies
\mathbb{E}[\varphi^2 | x ] = Var(\varphi^2 | x ) +  \mathbb{E}[\varphi|x]^2 =
\hat{(\varphi^2)}_{MMSE}(\tilde x)
$$
- Now we separately calculate each of the terms :
 $$
\mathbb{E}[\varphi|x] = 
\mathbb{E}[h_0^T \cdot \theta |x] = 
h_0^T \cdot \mathbb{E}[\theta |x] =
h_0^T \cdot \underbrace{\hat\theta_{MMSE}(x)}_{\text{previously calculated...}}
$$$$
\implies \mathbb{E}[\varphi|x]^2 = 
(h_0^T \cdot (H^T \frac{1}{\sigma_v^2} H  + C^{-1})^{-1} \cdot 
(\frac{1}{\sigma_v^2} \cdot H^T \cdot \underline x + C^{-1}\underline\mu))^2
$$
  
$$
Var(\varphi^2 | x )  = 
\mathbb{E}[h_0^T \cdot \theta \cdot \theta^T \cdot h_0 |x] =
h_0^T \cdot \mathbb{E}[ \theta \cdot \theta^T  |x] \cdot h_0 = 
h_0^T \cdot \mathbb{E}[ \hat\theta(x) \cdot \hat\theta^T(x) ] \cdot h_0 = \dots
$$

- For the second term we notice that the term $\mathbb{E}[ \hat\theta(x) \cdot \hat\theta^T(x)]$  is the Covariance matrix of the estimator we found previously $C_{\theta| x}$. So all that is left to do is calculate this matrix:
$$
\mathbb{E}[ \hat\theta(x) \cdot \hat\theta^T(x) ] = 
Cov(\theta|x)
$$
- Since the statistical model of the data samples is a **Linear Gaussian Model**, we know that the covariance of the posterior distribution is the inverse of the of the posterior distribution:
$$
C_{\theta|x} = (\frac{1}{\sigma_v^2} H^T H + C^{-1})
$$
- We substitute this matrix back in our original expression to get the variance of $\varphi^2|x$ :
$$
Var(\varphi|x) = 
h_0^T \cdot C_{\theta|x} \cdot h_0 = 
h_0^T \cdot (\frac{1}{\sigma_v^2} H^T H + C^{-1}) \cdot h_0 
$$

> [!success] Result
> And now we get the final expression for the estimator :
> $$\hat(\varphi^2) = \left(h_0^T \cdot (H^T \frac{1}{\sigma_v^2} H  + C^{-1})^{-1} \cdot 
(\frac{1}{\sigma_v^2} \cdot H^T \cdot \underline x + C^{-1}\underline\mu)\right)^2 + h_0^T \cdot (\frac{1}{\sigma_v^2} H^T H + C^{-1})^{-1} \cdot h_0 $$

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
$$
MSE(\hat\theta_{2,c}(\mathbf{y})) = 
\mathbb{E}\left[(
	\hat\theta_{2,c}(\mathbf{y}) - \theta
)^2\right] = 
\mathbb{E}\left[(
	\hat\theta_{1}(\mathbf{y}) + c\cdot g(\mathbf{y}) - \theta
)^2\right] = 
$$$$
 = \mathbb{E}[(\hat\theta_{1}(\mathbf{y}) - \theta)^2] + 
2 \cdot c \cdot \mathbb{E}[(\hat\theta_{1}(\mathbf{y}) - \theta) \cdot g(\mathbf{y})] + 
c^2 \cdot \mathbb{E}[g(\mathbf{y})^2] =
MSE(\hat\theta_1) + 2 c \rho + c^2 \sigma^2
$$
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
$$$$
\dots = \left\{
u_m \perp \! \perp u_n : \forall n\ne m
\right\} = 
\sum_{m = 1}^k (a^2)^{k-m} \sigma^2 =
\sigma^2 \cdot \frac{a^{2k} - 1}{a-1}
$$

> [!success] Result
> We get the final expression for the MSE of the estimator :
> $$ MSE(\hat y_{_N+k}) =  \sigma^2 \cdot \frac{a^{2k} - 1}{a-1} = \mathcal{O}(a^k)$$
> Meaning that the MSE grow exponentially with respect to how far to the future we are trying to estimate.

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
$$$$
\implies 
\hat\theta \cdot \alpha  = \ln
\left(
\frac{1}{\mathbb{E}[e^{-\alpha\theta}| \underline x]}
\right)
= -\ln
\left(
\mathbb{E}[e^{-\alpha\theta}| \underline x]
\right) 
$$

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


