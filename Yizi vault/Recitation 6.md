
## Floyd-Warshall

### algorithm :

**Init :** 
$$d_{i,i}^{(0)} = 0$$
$$
d_{i,j}^{(0)} = 
\begin{cases}
w_{i,j} \quad : ij \in E \\
\infty \quad : ij \not\in E \\
\end{cases}
$$
**Loop :**

-  for $k = 1,\dots, |v|$ do : 
	- for $i = 1,\dots, |v|$ do : 
		- for $j = 1,\dots, |v|$ do : 
			- $d_{i,j}^{(k)} = min(d_{i,j}^{(k-1)}, d_{i,k}^{(k-1)} + d_{k,j}^{(k)})$ 
- return $d(\cdot)$



### Exercise : 
Find an algorithm to check negative cycles.

#### option 1 : Bellman Equations - $\mathcal{O}(|V||E|)$

1. for each $i \in V$ :
	1. $\forall uv \in E$ :
		1. If $d_{i,v}^{n} \ge d_{i,u}^{n} + w_{u,v}$:
			1. NNC = False

#### option 2 : Checking Cycles - $\mathcal{O}(|V|)$

- $\forall i \in V$ :
	- if $d_{i,i}^(n) \lt 0$ :
		- NNC = False

#### Correctness 

**Claim :** 
$G$ has negative cycles $\iff$ $\exists i \in 1\dots n \ : \ d_{i,i}^{(n)} \lt 0$ 

**Proof :**

- $\implies$ 
	$\exists i \in 1\dots n \ : \ d_{i,i}^{(n)} \lt 0$ , meaning that FW has found a negative Path from $i$ to itself 
	$\implies$ Has negative Cycle!

- $\impliedby$ 
	We assume $G$ has a negative cycle. We need to prove that $\exists i \in 1\dots n \ : \ d_{i,i}^{(n)} \lt 0$ .
	We observe a negative cycle $C \subseteq G$ in which the max. index in the cycle is minimal over the set of all negative cycles :
	$$
	k := \underset{C \in G}{min}\{\underset{i\in C}{max}\{i\}\}
	$$
	We denote that node as $k$...
	We observe node $i$ in the cycle that contains $k$ in it.
	After the (outer loop) $k-1$ iteration :
		$d_{k,i}^{(k-1)} , d_{i,k}^{(k-1)}$, from the minimality of $k$, are the distance that did not use any other cycles for their distance calculation and therefore still have valid distances.
		$d_{i,i}^{(n)} \le d_{i,i}^{(k)} \le d_{k,i}^{(k-1)} + d_{i,k}^{(k-1)} \le w(C) \lt 0$
		$\implies d_{i,i}^{(n)} \lt 0$ , Done!

### Exercise 3 : from test 2019 B

![[Pasted image 20260517103729.png]]

**Definition :**
Given an undirected Graph $G = (V,E)$, a node set $D \subseteq V$ is called a **control group** if :
$$
V = D \cup N(D) \ : \ N(D) := \{ u \in V \ : \ \exists v \in D \ : \ uv\in E\}
$$
$$
\implies \forall v \in V : 
(\exists u \in D \:\ uv\in E) \lor 
(\exists u \in N(D) \:\ uv\in E)
$$
**Definition :** 
Given an undirected Graph $G = (V,E)$ , a node set $C \subseteq V$  is called a **vertex cover** if :
$$
\forall e \in E \ : \ \exists v \in e \ : \ v \in C
$$

#### d) Prove/contradict :
If $S$ is a V.C. in a connected Graph $G \implies$ $\forall v \in V \ : \ (v\in S) \lor (v\in N(S))$ 

We separate to cases :

- If $v \in S$ : Were done!
- If $v \not\in S$ : $S$ is a V.C. in a connected graph meaning $\forall ux \in E \implies x\in S \implies v \in N(S)$ 

#### e) Prove/Contradict :
$S \subseteq V$ is a control group in $G = (V,E) \implies$ $S$ is a V.C.

- Since $S$ is a control group : $\forall v \in V \ : \ (v \in S) \lor (v \in N(S))$
- Therefore, if we observe any edge in $G$ we know that they are both in either one of the sets : $\forall e = uv \in E : \forall w \in e : (w \in S ) \lor (w \in V / S = N(S))$ 
- $\implies \forall uv \in E : (u \in S) \lor (v \in S) \implies S$ - V.C.
