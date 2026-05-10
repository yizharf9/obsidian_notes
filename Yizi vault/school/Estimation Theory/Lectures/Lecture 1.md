
#### Notation :

- $\mathbf{\theta}, \underline{\theta}$  - vector of estimation parameters.

- $\{x_n\}_{n=1}^N$ - series of sampled data.

- $\underline{x} = \begin{bmatrix} x_1 \\ ... \\ x_n \end{bmatrix}$ - vector of sampled data

- $\hat{\mathbb{\theta}}(\underline{x}),\underline{\hat{\mathbb{\theta}}}(\underline{x})$ -  estimator of parameters based on sampled data.

#### There are 2 main methods of estimation discussed in this course :

##### Bayesian estimation 

- $\underline{\theta} \sim \mathcal{P(\underline{\theta})}$ - Random Vector (denoted as R.V.)
- $C(\hat{\underline{\theta}},\underline{\theta})$ - Cost function of estimation

In this method our goal is to find $\hat{\theta}$  which yields : $$risk(\hat{\underline{\theta}},\underline{\theta}) = \mathbb{E}[C(\hat{\underline{\theta}},\underline{\theta})] \ , \ risk(\hat{\underline{\theta}},\underline{\theta}) \to min$$
For example, the $MMSE$ estimator is as follows :

$C(\hat{\theta}, \theta) = (\hat{\theta} - \theta)^2 \ \implies \ risk = \mathbb{E} [(\hat{\theta}-\theta)^2] \underset{\hat{\theta(\underline{x})}}{\longrightarrow}  min$  
Usually, for this method we will need the common PDF of the random variables : $x \sim \mathcal{P(x)},\theta \sim \mathcal{P(\theta)} \implies f_{\underline{x},\underline{\theta}}(\underline{\alpha},\ \underline{\varphi})$ 
That is what ties us to what we want to estimate.
That is in fact the statistical description of how the samples affect the estimation parameter.

##### Non-Bayesian estimation


- $\underline{\theta}$ - Can be deterministic  (not a Necessary condition...). 
	If $\theta$ is random, we will treat it as if it was deterministic

- $C(\hat{\underline{\theta}},\underline{\theta})$ - Cost Function of the estimation

- $risk = \mathbb{E}[C(\hat{\underline{\theta}},\underline{\theta})]$ 

The problem with this approach is that the expected value is being performed on $\hat{\underline{\theta}}(\underline{x})$ , which is dependent on the data samples only and not random and the risk is a function of $\underline{\theta}$ .
For that we need the PDF of the samples $\underline{x}$ : $f_{\underline{x}}(\underline{\alpha} ; \underline{\theta})$ , meaning that $\underline{\theta}$ is a **parameter** of the PDF and not a variable.
for each different set of values of $\underline{\theta}$ we will get a different PDF...




## Non-Bayesian estimation

In Non-Bayesian estimation we will want to estimate $\theta$ out of the data samples $X$.
The estimator is denoted as $\hat{\theta}$

we will plot the desired PDF of $\hat{\theta}$ :

##### Biased and Un-Biased  estimation

```desmos-graph
left = -0.2; right = 6
top = 2 ; bottom = -0.2
---
a = 2
b = 3.5
f_{1}(x) = \frac{1}{0.5\sqrt{2\pi}}e^{-0.5\left(\frac{x-a}{0.5}\right)^{2}}
f_{2}(x) = \frac{1}{0.25\sqrt{2\pi}}e^{-0.5\left(\frac{x-a}{0.25}\right)^{2}}
f_{3}(x) = \frac{1}{0.8\sqrt{2\pi}}e^{-0.5\left(\frac{x-b}{0.8}\right)^{2}}
x = a \{0 < y < 2.1\}
x = b \{0 < y < 0.5\}
0 < y < f_{1}(x) \{x < 1.1\} 
0 < y < f_{1}(x) \{x > 2.9\}
(a, -0.1)
(b, -0.1)
```

| **Object**          | **Math Symbol**      | **Color** | **Brief Description**                         |
| ------------------- | -------------------- | --------- | --------------------------------------------- |
| **True Parameter**  | $\theta$             | **Black** | The target value (The center-line).           |
| **Best Option**     | $f_{\hat{\theta}_2}$ | **Blue**  | Most efficient; hits the target consistently. |
| **Standard Option** | $f_{\hat{\theta}_1}$ | **Black** | Correct on average, but wider spread.         |
| **Poor Option**     | $f_{\hat{\theta}_3}$ | **Red**   | Systematically wrong (Biased) and unreliable. |
| **Expected Value**  | $E[\hat{\theta}_3]$  | **Red**   | The center of the biased distribution.        |

>[!info] [[Lecture 1#Biased and Un-Biased estimation]]
>We would like the center of mass of the PDF to be around the **true value** of the estimation target $\theta$.
>In the tails of the PDF - these are probabilities that we didn't estimate correctly.

- $f_{\hat{\theta_3}}$ - biased estimator, it's expected value is not the same as theta's $\mathbb{E}[\theta_3] \not= \mathbb{E}[\theta]$ 
There is a visual trade-off between Un-Biased and distance from **true value**.


![[Pasted image 20260509154435.png]]

- $f_{\hat{\theta_4}}$ - It is  an Un-Biased estimator, yet it has a larger probability of error.
$\implies$We get a PDF with much larger variance.

- $f_{\hat{\theta_5}}$ - We will usually require the property of Being Un-Biased, asymptotically : $\mathbb{E}[\hat{\theta} - \theta] \underset{n \to \infty}{\longrightarrow} 0$  

**Definition : Unbiased**

An unbiased estimator $\hat{\underline{\theta}}$ of $\underline{\theta}$  satisfies : $$\mathbb{E}[\underline{\hat{\theta}}-\underline{\theta}] = 0 $$
The **Bias** of an estimator is denoted as : $$\underline{b} = \mathbb{E}[\hat{\underline{\theta}}-\underline{\theta}]$$
**Definition : Consistency**

We would like that as the number of the independent data samples $N \to \infty$ , the estimator will converge to the target parameter $\theta$  : $$\underline{\hat{\theta}} \underset{N \to \infty}{\longrightarrow} \underline{\theta}$$
We will denote the estimator of the the first $n$ samples as $\hat{\theta}_n$ 
while the vector of the sample vectors is denoted as $\underline{\underline{x}}^{(n)} = \begin{bmatrix} \underline{x_1} \\ ... \\ \underline{x_n} \end{bmatrix}$
Meaning that we would like to get : $$\lim_{n\to\infty}{\mathbb{P}( |\hat{\theta}^{(n)} - \theta| > \varepsilon)} = 0 \ : \ \forall\varepsilon>0$$

```desmos-graph
left=-0.5 ; right = 10;
top = 0.8 ; bottom = -0.2
---
a = 4
d = 1.5
f(x) = \frac{1}{1.5\sqrt{2\pi}}e^{-0.5\left(\frac{x-(a+d)}{1.5}\right)^{2}}
x = a+d \{0 < y < f(a+d)\} | dashed | red
x = a-d \{0 < y < f(a-d)\}| dashed | red
(a,0) | label: the estimators expected value
x = a | dashed | black
0 < y < f(x) \{x > a+d\} | Blue
0 < y < f(x) \{x < a-d\} | Blue
```

A consistent estimator is an estimator that, the more samples are taken in consideration during the estimation, the smaller the filled tails of the plot (representing the estimation error) will grow smaller.

#### Example

- $\{x_n\}_{n=1}^N$ - i.i.d with distribution : $x_n \sim \mathcal{N}(0,1) : \forall n \in \mathbb{N}$ 
- $\underline{x} = \begin{bmatrix} x_1 \\ ... \\ x_n \end{bmatrix}$ - data sample vector 
- $f_{\underline{x}}(\underline{x} ; \theta) = \frac{1}{(2\pi)^{\frac{N}{2}}}exp(-\frac{1}{2}\sum_{n=1}^{N}{(x_n-\theta)^2})$  -  common PDF of data samples
We would like to estimate the parameter $\theta$ from the samples $\underline{x}$ :

The estimators examined :
1. $\hat{\theta_1}(\underline{x}) = \frac{1}{N}\sum_{n=1}^{N}{x_n}$ - accumulated average
2. $\hat{\theta_2}(\underline{x}) = x_1$ - first sample
3. $\hat{\theta_2}(\underline{x}) = \frac{1}{N}\sum_{n=1}^{N}{x_n} + \frac{1}{N}$

##### We check bias of estimators 

1. $\underline{b_1} \ = \ \mathbb{E}[\hat{\theta_1}(\underline{x}) - \theta] = \frac{1}{N}\sum_{n=1}^{N}{\mathbb{E}[x_n - \theta]} = 0 \implies$ **Unbiased** 
2. $\underline{b_2} \ = \ \mathbb{E}[\hat{\theta_2}(\underline{x}) - \theta] = \mathbb{E}[x_1] = 0 \implies$ **Unbiased** 
3. $\underline{b_3} \ = \ \mathbb{E}[\hat{\theta_3}(\underline{x}) - \theta] = \frac{1}{N}\sum_{n=1}^{N}{\mathbb{E}[x_n - \theta]} + \frac{1}{N} \underset{N \to \infty}{\longrightarrow} 0 \implies \dots \overset{a}{\approx}$   **Unbiased**

##### We check consistence of estimators

1. $Var(\hat{\theta}_1) = \frac{1}{N^2} \sum_{n=1}^{N}{Var(x_n) = \frac{1}{N}}$ - grows smaller and approaches 0, N grows $\implies$ **Consistent**
2. $Var(\hat{\theta}_2) = 1$ $\implies$ **Not Consistent!**
3. $Var(\hat{\theta}_3) = \frac{1}{N}$ - **Consistent**

```desmos-graph
left = -4.2 ; right = 13;
top = 10 ; bottom = -0.2;
---
c = 4
y = 5\exp\left(-\frac{\left(x-c\right)^{2}}{1.5}\right) | black 
y = 3\exp\left(-\frac{\left(x-c\right)^{2}}{15}\right) | red
y = 4\exp\left(-\frac{\left(x-\left(c+2.5\right)\right)^{2}}{1.5}\right) | purple
y = 8\exp\left(-\frac{\left(x-c\right)^{2}}{0.2}\right) | dashed | black
y = 8\exp\left(-\frac{\left(x-\left(c+1\right)\right)^{2}}{0.2}\right) | black
```



#### Lemma 
If $\hat{\theta}$ is an Unbiased estimator with asymptotically 0 variance $\implies$ The estimator is **Consistent!**

**Proof:**
We will use the Chebyshev inequality : $$\mathbb{P}(|  \ \hat{\theta} - \mathbb{E}[\hat{\theta}] \ | \gt \varepsilon) \le \frac{var(\hat{\theta})}{\varepsilon^2}$$
We will take the limit on both sides of the inequality : $$\lim_{n \to \infty}\mathbb{P}(|  \ \hat{\theta} - \mathbb{E}[\hat{\theta}] \ | \gt \varepsilon) \le \frac{ \lim_{n \to \infty} var(\hat{\theta})}{\varepsilon^2}$$
- $\lim_{n \to \infty}{var(\hat{\theta})} = 0$  - since $\hat{\theta}$ is defined as Unbiased and therefore, RHS is 0.
- We get that $\hat{\theta} is a **Consistent** estimator by definition.

>[!warning] [[Lecture 1#Lemma]]
>This is a sufficient condition but not a necessary one! 

## Least-Squares (LS) estimator

#### Notation

- $\underline{x} \in \mathbb{R}^{N\times1}$ - **Random** vector of the data samples
- $\underline{\theta} \in \mathbb{R}^{M\times1}$ - **Deterministic** vector (estimation parameters...)
- $\underline{\underline{H}} \in \mathbb{R}^{N\times M}$ - Predefined, known matrix
- $\underline{v} \in \mathbb{R}^{N\times1}$ - **Random** vector of additive noise

##### Underlying Assumption : $rank(H) = M \le N$ 
Meaning that i have more data samples then the same vector I am trying to estimate (collected enough data...). 

- No assumptions are made about the distribution of the Noise.

##### The goal  :  estimate $\theta$ from the samples $\underline{x}$

##### Estimator Structure : $$\hat{\theta}_{LS} = \underset{\theta' \in \mathbb{R^{M}}}{argmin} \parallel \underline{x} - \underline{\underline{H}} \cdot \underline{\theta} \parallel_2^2 $$
##### Vector Derivatives :

- $g(\underline{\theta})$ - scalar function $\implies \underline{\theta} = \begin{bmatrix} \theta_1 \\ ... \\ \theta_N \end{bmatrix}$ $$\nabla g = \frac{\partial g}{\partial \underline{\theta}} = \begin{bmatrix}  \frac{\partial g}{\partial \theta_1} , \dots , \frac{\partial g}{\partial \theta_N}\end{bmatrix}$$ 

- $\underline{g}(\underline{\theta})$ - vector function :$$\frac{d\underline{g}}{d\underline{\theta}} = \frac{\partial g}{\partial \underline{\theta}} = \begin{bmatrix}  \frac{\partial g_1}{\partial \underline{\theta}} \\ \dots \\ \frac{\partial g_N}{\partial \underline{\theta}}\end{bmatrix} \ : \ [\frac{d\underline{g}(\underline{\theta})}{\partial \underline{\theta}}]_{n,m} = \frac{\partial g_n(\underline{\theta})}{\partial\theta_m}$$ 

- Second Order Derivative of a scalar function : $$[\frac{\partial^2 g(\underline{\theta})}{\partial\underline{\theta}^2}]_{m,k} = \frac{\partial^2 g(\underline{\theta})}{\partial\underline{\theta}  \ \partial\underline{\theta}^T} = \frac{\partial^2 g(\underline{\theta})}{\partial\underline{\theta_m}  \ \partial\underline{\theta_k}^T}$$

- Derivative of linear mapping $A$ : $$\frac{\partial(A\cdot\underline{\theta})}{\partial \underline{\theta}} = A$$
- Derivative of Cubic scaling $A$ : $$\frac{\partial(\underline{\theta}^TA\cdot\underline{\theta})}{\partial \underline{\theta}} = \underline{\theta}^T (A^T + A) \ : \ A \in \mathbb{R}^{N\times N}$$ 
- Second Order Derivative of Cubic scaling $A$ : $$\frac{\partial^2(\underline{\theta}^TA\cdot\underline{\theta})}{\partial \underline{\theta}^2} = A^T + A \ : \ A \in \mathbb{R}^{N\times N}$$
#### Back to our estimator...

- We would like to further derive the structure of the estimator.

$$Q(\underline{\theta}) = \parallel \underline{x} - H \cdot \underline{\theta} \parallel^2 = (\underline{x} - H \cdot \underline{\theta})^T(\underline{x} - H \cdot \underline{\theta}) = ||\underline{x}||^2 - 2 \underline{x}^T H \underline{\theta} + \underline{\theta}^THH^T\underline{\theta}$$
- We will find the critical points using derivation : $$\frac{dQ(\underline{\theta})}{d\underline{\theta}} = - \not2 \underline{x}H + \not2 \underline{\theta}^T (HH^T) = \underline{0}$$
- We compare to $\underline{0}$ and find min.  
- We will remind that we forced that $rank(H) = M$ therefore , $H$ is invertible: 
$$
HH^T\underline{\hat{\theta}}_{LS} = H^T\underline{x} \implies \ \hat{\underline{\theta}}_{LS} = (H^TH)^{-1}H^T \cdot \underline{x}
$$

>[!info] 
>We get The LS estimator and we can see that it is **linear** with the Data samples.

- We will reassure that the LS-estimator indeed, yields a min. using the hessian matrix (SOD):
$$
\frac{
\partial Q(\underline{\theta})
}{
\partial\underline{\theta}^T\partial\underline{\theta}
}
= 2H^TH \longrightarrow Const. 
$$
- Since $H$ is positive semidefinite matrix, so as $H^TH$ and therefore : $$
\underline{a}^T (H^TH)\underline{a} = ||H \underline{a}||^2 \ge 0 \ : \ \forall a \in \mathbb{R}^{N}
$$
- Since $H^TH$ is not singular and we proved that $H^TH$ is positive semidefinite, we conclude that $H^TH$ is positive definite : $$
H^TH  \succ 0
$$
### LS estimator performance

#### Bias
$$
\mathbb{E}[\hat{\theta}_{LS} - \theta] =
\mathbb{E}[(H^TH)^{-1}H^T\cdot \underline{x} - \theta] =
(H^TH)^{-1}(H^T H)\mathbb{E}[\underline{x}] -\underline{\theta}  = \dots$$
$$
 = 
\{\dots \mathbb{E}[\underline{x}] = \dots  H \underline{\theta} + \mathbb{E}[\underline{v}] =  
H \underline{\theta} \dots \}{=} 0
$$
>[!info]
>Meaning that the LS estimator is **Unbiased** as long as the noise is white $\mathbb{E}[\underline{v}] = 0$

#### Squared Error

We assume :
1. $\mathbb{E}[\underline{v}] = 0$
2. $\mathbb{E}[\underline{v}\underline{v}^T] = Cov(\underline{v}) = \underline{\underline{R}}$

>[!info]+ reminder
>$Cov(A\underline{x}) = A Cov(\underline{x}) A^T : A \in \mathbb{R}^{N\times N}$

$$Cov(\hat{\theta}_{LS}) = 
Cov( (H^TH)^{-1}H^T \underline{x} ) =
(H^TH)^{-1}H^T \cdot Cov(\underline{x} ) \cdot ((H^TH)^{-1}H^T ) ^T = \dots
$$ $$
\dots = (H^TH)^{-1}H^T \cdot \underline{\underline{R}} \cdot ((H^TH)^{-1}H^T )^T
$$
> [!info]+ Notice
> $Cov(\hat{\theta}_{LS})$ is linear with the **covariance** of the data samples

> [!Example]+
> $x_n = \theta + v_n : n \in 1\dots n$
> $\underline{x} = \mathbb{1} \cdot \theta + \underline{v}$
> 
> $\implies\hat{\theta}_{LS}(\underline{x}) = (H^TH)^{-1}H^T \underline{x} = (\mathbb{1} ^ T \mathbb{1})^{-1} \mathbb{1}^T \underline{x} = \frac{1}{N}\sum_{n=1}^{N}{x_n}$
> 
> $\implies\hat{\theta}_{LS}(\underline{x}) = \frac{1}{N}\sum_{n=1}^{N}{x_n}$
>  
>  We denote the **Estimation error** as : $\underline{\varepsilon}_{LS} = \underline{\hat{\theta}_{LS}} - \underline{\theta}$
>$$Cov(\hat{\theta}_{LS}) \underset{M \gt 1}{=} Var(\hat{\theta}_{LS}) = (\mathbb{1}^T\mathbb{1})^{-1}\mathbb{1}^T \cdot \underline{\underline{R}} \cdot ((\mathbb{1}^T\mathbb{1})^{-1}\mathbb{1}^T ) ^ T = \frac{1}{N^2} \mathbb{1}^T \cdot  \underline{\underline{R}} \cdot \mathbb{1} $$
>Now, we assume that $\underline{\underline{R}}$ is diagonal, meaning that the data samples $\underline{x}$ are uncorrelated : 
>$\implies Cov(\hat{\theta}_{LS}) = \frac{1}{N^2}\sum_{n=1}^{N}{\sigma_n^2}$

We notice that if we have a data sample $x_i$ that is added a lot of noise $\sigma_i^2 >> 1$, we might consider weighing it differently with respect to other samples to have a lower estimation error. for that 

## Weighted Least Squares (WLS) estimator

- We denote the WLS solution as : $$\hat{\theta}_{WLS} = \underset{\underline{\theta} \in \mathbb{R}^M}{argmin}\{ (\underline{X} - H \underline{\theta}) \cdot \underline{\underline{W}} \cdot (\underline{X} - H \underline{\theta}) \}$$
- When $W$ is a weight matrix. 
- We assume $W \succ 0 \ , \ W = W^T \ , \ \exists W^{1/2} \in \mathbb{R}^{N\times N} \ : \ W = W^{1/2} \cdot W^{1/2}$
$$Q(\underline{\theta}) = [W^{1/2}(\underline{x} - H \underline{\theta})] \cdot [W^{1/2}(\underline{x} - H \underline{\theta})] ^T = \dots  $$
- We denote as follows :
$$\tilde{\underline{x}} := W^{1/2}\underline{x} \ , \ \tilde{H} := W^{1/2} H \underline{\theta}$$
- Overall we get an estimator that is linear with respect to the data samples as well :
$$\hat{\underline{\theta}}_{WLS}(\tilde{\underline{x}}) = (\tilde{H}^T\tilde{H})^T \tilde{H}^T \cdot \tilde{\underline{x}} $$
$$\dots = (H^TWH)^{-1}H^TW \cdot \underline{x} $$
[[Lecture 2 | link to next lecture]]
