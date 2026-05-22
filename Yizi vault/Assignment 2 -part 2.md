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
$$\underbrace{\begin{pmatrix}\underline x \\\underline \mu \\ \end{pmatrix}}_{\underline{\tilde{x}}\in \mathbb{R}^{N+M}}=\underbrace{\begin{pmatrix} H \\ \mathbb{I}_M \\ \end{pmatrix} }_{\tilde{H} \in \mathbb{R}^{(N+M)\times M} } \cdot \underline \theta +\underbrace{ \begin{pmatrix} \underline v \\ \underline{\varepsilon_\theta} \\ \end{pmatrix}}_{\underline{\tilde{v}} \ \mathbb{R}^{N+M}}$$
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

