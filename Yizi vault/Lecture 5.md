
## Cramer - () Bound

We want to prove two properties of the theorem :
1. Inequality :
$$
Cov(\hat\varphi) \ge
\frac{dg(\theta)}{d\theta} 
\cdot J^{-1} \cdot 
\frac{dg(\theta)}{d\theta} ^T
$$
$$
\mathbb{E}[\hat\varphi - \varphi] = 0 : \forall \varphi \in \Omega_\varphi
$$
$$
\mathbb{E}[\frac{dg(\theta)}{d\theta} ] = 0
$$
$$
\mathbb{I}(\theta) = 
\mathbb{E}[\frac{\partial logf(x,\theta)}{\partial\theta}^T \cdot \frac{\partial logf(x,\theta)}{\partial\theta}] =
\mathbb{E}[\frac{\partial^2 logf(x,\theta)}{\partial \theta}^T ]
$$

2. Equality iff :
$$
\hat\varphi - \varphi = \frac{dg}{d\theta} \mathbb{I}(\theta) \frac{logf(x,\theta)}{d\theta}^T
\implies \mathbb{E}[\hat\varphi - \varphi] = 0 : \forall\varphi \in \Omega_\varphi
$$
