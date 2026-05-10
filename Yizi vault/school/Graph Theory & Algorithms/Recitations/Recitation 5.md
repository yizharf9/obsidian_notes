
## Exercise 1

Let $G = (V,E)$ a graph with capacities $w : E \to \mathbb{R}$ .
Find the max bottleneck in the graph.

**Solution** : 
We will use a variation of dijkstra's algorithm for finding max. bottleneck.

#### The algorithm

$Bottleneck(G=(V,E),w : E \to \mathbb{R},s\in V)$
1. $Q \gets V$
2. while $Q \ne \emptyset$ do :
	1. $u \gets Q.dequeue()$
	2. for each $v \in (N(u) \cap Q)$ do :
		1. if $\lambda[v] \lt min\{\lambda[u] , w(u,v) \}$ then
			1. $\lambda[v] = min\{\lambda[u] , w(u,v) \}$ 
			2. $p[v] = u$
3. return $\lambda , p$

**Correctness** :

 - We denote $B(s,v)$ as the max bottleneck between $s$ and $v$. $$B(s,v) = \underset{P\in E}{max}\{ \underset{e\in P }{min\{ w(e)\}}\}$$
 - We want that $\forall v \in V$ in the end of the run of the algorithm we get : 
	 1. After dequeuing a vertex from the queue, $\lambda(v)$ does not change.
	 2. $\lambda (v) \le B(s,v)$ , we assume by contradiction that  $\lambda (v) \gt B(s,v)$ ...

We will prove these by induction on the order of dequeuing of the vertices.

**Base** : 
$n=1 \implies \lambda(s) = \infty = B(s,v)$  

**Induction Hypothesis** :
We assume for some arbitrary $n-1$ that $\forall v \in Q : \lambda(s) = B(s,v)$  
for every $v$ pulled from the queue before $u$.

**Step** :
We need to show $\lambda(u) =B(s,v)$ 
- We examine $P$, the path for which we derive $B(s,u)$ $$P : s = v_0 \to \dots \to v_{k-1} \to v_k = u$$
- We examine 2 possible cases :

1. $v_0,\dots,v_{k-1}$ were pulled from the queue before u :  
$$ \lambda(u) \ge min\{ \lambda(v_{k-1}) , w(e_k) \} =  min\{ B(s,v_{k-1}) , w(e_k) \} \underset{I.H.}{=} 
min\{ \underset{1\le j \le k-1}{min \{ e_j \}} , w(e_k) \} = 
\underset{1\le j \le k}{min \{ e_j \}}= 
B(s,u) $$
$$\implies \lambda(u) \le B(s,u) \implies \lambda = B(s,u)$$
2. $\exists v_i \in P$ that were pulled from the queue after $u$ in the run of the algorithm.
	Let $v_i$ with index $\forall j \lt i : v_j \not\in Q$ 
	$$
	\lambda(v_i) \ge min\{ \lambda(v_{i-1} , w(e_i))\} \underset{I.H.}{=}  
	\lambda(v_i) \ge min\{ B(s,v_i) , w(e_i))\} =  
	\lambda(v_i) \ge \underset{1 \le j \le k}{min}\{ w(e_j)\} =  
	B(s,v_k = u)
	$$
	$$\implies B(s,u) \gt \lambda(u) \implies \lambda(v_i) \gt \lambda(u)$$
>[!danger]
>**Contradiction** : To the fact that the order of dequeuing from the queue is by current max. bottleneck $\implies v_i$ should have been dequeued from the queue before $u$ 

## Exercise 2

Given a graph $G = (V,E)$ find an algorithm for finding all shortest paths from the starting node $s$.

**Solution** :

$$
path[v] = \begin{cases}
1 : v = s \\ 
0 :v\ne s
\end{cases}
$$
$$dist[v] = \begin{cases}
0 : v = s \\ 
\infty :v\ne s
\end{cases}$$

### The algorithm

$ShortestPath(G=(V,E),s\in V,t\in V)$
1. $Q.enqueue(s)$
2. while $Q \ne \emptyset$ do :
	1. $current \gets Q.dequeue()$
	2. for each $child \in N(current)$ do :
		1. if $dist[child] == \infty$ then
			1. $Q.enqueue(child)$ 
			2. $dist[child] \gets dist[current] + 1$
			3. $paths[child] \gets paths[current]$
		2. else if $dist[child] == dist[current] + 1$ then 
			1. $paths[child] \gets paths[child] + paths[current]$ 
3. return $paths[t]$

**Correctness** :

Since we proved the correctness of `BFS` and therefore $\forall v \in V : dist[v] = d(s,v)$.
in line () the condition checks if there is a path shorter than the one updated and so in line ()+1 the update adds the number of shortest paths discovered so far with number of paths : " "  discovered in the current iteration