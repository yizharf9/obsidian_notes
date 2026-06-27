## Least Squares Solution - Non-linear system models

[[Lecture 2#Time Delay estimation (TDE) Problem | link to previous lecture]]

In previous lecture we observed the model :
$$\underline x = \underline h (\underline \theta) + \underline v \ : \ \underline x \in \mathbb{R}^N, \underline \theta \in \mathbb{R}^M ,\underline h : \mathbb{R}^M \to \mathbb{R}^N $$

And we wanted to find an estimator of the form :
$$\hat \theta_{WLS}(\underline x) = \underset{Q(\theta)}{argmin}\left\{ (\underline x - \underline h(\underline \theta))^T \cdot W \cdot (\underline x - \underline h(\underline \theta))\right\} $$
We would like to have an iterative solution for finding the optimal estimator. 
The following is a method from the **Newton-Raphson** family.

- We denoted $\theta^*$ - the current estimation of the optimal parameter vector.
- We derive the first-order Taylor series of the $\underline h (\underline \theta)$ around $\theta^*$.
$$\underline h (\underline \theta) = \underline h (\underline \theta^*) + \underbrace{\left.\frac{ d\underline h (\underline \theta)}{d\theta}\right|_{\theta = \theta^*} }_{:=H(\theta^*)}\cdot (\theta - \theta*) + \mathcal{o}\left(||\theta - \theta^*||^2\right) : [H(\theta^*)]_{i,j} = \frac{\partial h_i(\theta^*)}{d\theta_j}$$
- We get that our estimator is :
$$\hat \theta_{WLS}(\underline x) = \underset{Q(\theta)}{argmin}\left\{ (\underline x - \underline h(\underline \theta))^T \cdot W \cdot (\underline x - \underline h(\underline \theta))\right\}  = $$$$ = \left(\underbrace{\underline x - \underline h (\underline \theta^*)}_{\underline {\tilde x}} -H(\theta^*)  \cdot \underbrace{(\theta - \theta*)}_{\underline{\tilde \theta}}\right)^T \cdot W \cdot \left(\underbrace{\underline x - \underline h (\underline \theta^*)}_{\underline {\tilde x}} -H(\theta^*)  \cdot \underbrace{(\theta - \theta*)}_{\underline{\tilde \theta}}\right)$$
$$ = \left(\underline{\tilde x} - H(\underline \theta^*)\cdot \underline{\tilde \theta}\right)^T \cdot W \cdot \left(\underline{\tilde x} - H(\underline \theta^*)\cdot \underline{\tilde \theta}\right)$$
- Now we get a linear problem that its solution we've already derived in previous lectures :
$$\hat\theta_{WLS}(\underline{\tilde x}) = \left[H(\underline \theta^*)^T WH(\underline \theta^*)\right]^{-1}H(\underline \theta^*)^T W \cdot \underline{\tilde x}$$
$$\implies \hat\theta_{WLS}(\underline{x}) - \underline {\theta^*} = \left[H(\underline \theta^*)^T WH(\underline \theta^*)\right]^{-1}H(\underline \theta^*)^T W \cdot (\underline{\tilde x} - \underline h (\underline \theta))$$

> [!success] Result
> We derive the explicit form of the iterative equation :
> $$\hat\theta^{k+1} = \hat\theta^{k} + \left[H(\underline \theta^*)^T WH(\underline 
> \theta^*)\right]^{-1}H(\underline \theta^*)^T W \cdot (\underline{\tilde x} - \underline h (\underline \theta))$$
> > [!info] Notice
>  We notice that the estimator $\hat {\underline \theta}$ might not be linearly dependent in $\underline x$ Since the former steps are also dependent on $\underline x$. Therefore, we cannot state that the estimator is linear.


## Least Squares - given a prior 

In this case we will keep using the linear model of the data samples
$$\underline x = H \cdot \underline \theta + \underline v$$
But this time, we are given a prior statistical model of the parameters :
$$\mathbb{E}[\theta] = \underline \mu \ , \ Cov(\underline \theta) = \Lambda$$
A question arises, how do we consider the information about the distribution of the parameters in our estimator?