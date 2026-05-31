
## Steiner Trees

Given a network $(G,w)$ and a subset of the vertices $R \subseteq V$ (terminals), we would like to find a spanning sub-graph which satisfies a tree that contains at least the set $R$ with minimal weight.
We can add residual vertices for the sake of reducing the overall weight.

- In the general case ($|R|\ge3$) this is an NP-hard problem. Therefore there are 2 approaches for that :
	1. Specific cases
	2. Approximation Algorithms

**Reminder :**

#Lemma 1 :
If $(G,w)$ is a complete graph and $w$ is a metric, there exists a solution where the the number of steiner vertices.

#Lemma 2 :
The minimal steiner tree in $(G,w)$ with respect to $R$ is equivalent to the minimal steiner tree in $(k_V,d_G)$ with respect to $R$.










#### #algorithm 
$Steiner1(G,w,R):$
- $w \gets \infty$
- $\tilde T \gets \emptyset$ 
- $d \gets FW(G,w)$
- $\text{for }i=0\dots (|R|-2) do :$
	- $\forall A \subseteq V/R ,|A| = i :$
	- $\hat T \gets Prim(K_{A\cup R,d})$
	- if $d_G(\hat T) \lt w$ :
		- $\tilde T \gets \hat T$
		- $W \gets d_G(T)$
- return $S(\tilde T)$



### Exercise 1 

We Given the following algorithm :

#### #algorithm 
$Steiner2(G,w,R):$
- $d \gets FW(G,w)$
- $\hat T \gets Prim(K_{R,d})$
- return $S(\tilde T)$

Show that the algorithm returns a steiner tree that satisfies :
$$w(T) \le 2\cdot w(T^*)$$
**Solution :**

- We notice that 
	1. $\tilde T$ is returned from running Prim on the graph with $(k_R,d)$
	2. $\tilde T$ is an MST in $(k_R,d)$ that uses the terminals
 
- We observe $T^*$ . We will duplicate all edges twice in $T^*$ such that we get an eulerian multi-graph. 
- Every node has an even degree and therefore has an **eulerian walk**. $$O: v_1 \to v_2 \to \dots \to v_n$$

1. Initialize : we set $u_1 = v_1$ for some terminal $v_1$ , we set $j=1$.
2. Step : Assuming that we are in node $v_i$ :
	- If $v_{i+1}$ is a steiner node or a node we already visited : we will proceed to it and not update $j$
	- Else : $j \gets j+1$ , $u_j \gets v_{i+1}$ . proceed to next node. 
3. When we finish we will get a tree that satisfies $w(\hat T ) \le 2 \cdot w(T^*)$ 









