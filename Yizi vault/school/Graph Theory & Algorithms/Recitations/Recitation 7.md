
### Subjects :

1. MST
2. Questions from Test

## MST's


**Definition** :

A tree that is made of a subset of the edges of the original graph.

1. Spanning - all nodes are reachable from each other
2. minimal - $w(T) = \underset{T \subset G }{min \{\sum_{e\in E}w(e)\}}$

### Exercise 1

We are Given a graph $G = (V,E) , w(E)$ - connected and with weighted edges.
In addition, We are given the MST of G $T = (V,E_T)$.

#### a)
engineer a) performed an upgrade to the graph by adding an edge $E_1 = E\cup\{uv\}$.

What is the most efficient way to calculate $G_1$'s MST?

**solution :**
Adding the new edge to the the given MST $T$, must add a cycle.
We can iterate over the edges of that cycle and remove the max. weighted edge in that cycle.
That will yield the MST of the new graph.

**Correctness :**
We will use an auxiliary lemma :

#Lemma
A spanning tree is an MST $\iff$ $\forall e' \in C_T(e) : w(e) \ge w(e')$ 

We denote the max. edge in the new cycle as $xy$.

- First case : $e = xy$ 
	From the definition of $xy$, it already answers the condition of the lemma and therefore removing it will yield the new MST

- Second case : $uv \not\in C_T(e)$
	The lemma condition of the lemma is satisfied since all edges in $C'_T(e)$ are in $T$.
	$\implies C'_T(e) = C_T(e)$

- Third case :  $uv \in C_T(e)$
	Since $e$ closes a cycle  in the original tree $T$ (the tree containig $xy$).
	We denote that cycle as $C_T(e)$.
	Therefore, we get that the following exists:
	$$\forall e' \in C_T(e) : w(e) \ge w(e')$$
	And in particular :
	$$\implies w(uv) \le w(xy) \le w(e)$$
	Since we know that :
	$$C_{T'}(e) \backslash \{uv\} \subset C_T(e) $$
	The lemma holds for this case!

#### b)


### Exercise 4 - Question from test 
![[Pasted image 20260524102031.png]]

#### a) 
![[Pasted image 20260524102102.png]]

**Solution :**

1. leaves send to 1,2 ; 1 and 2 hold information of two leaves each
2. 1 and 2 send one of their vectors to the root.
3. ... 1 and 2 send therir second vector to the root.



#### b) 
![[Pasted image 20260524102805.png]]

**Solution :**
- $T(U =\emptyset)$

Table representing the amount of vectors each node holds in each time stamp for the right subtree.
We look only at the right subtree since it is longer and dictates the time of the process.

| Time/nodes | 5   | 6   | 4   | 2   |
| ---------- | --- | --- | --- | --- |
| 1          | 1   | 2   | 0   | 1   |
| 2          | 0   | 1   | 2   | 0   |
| 3          | 0   | 0   | 2   | 1   |
| 4          | 0   | 0   | 1   | 1   |
| 5          | 0   | 0   | 0   | 1   |
| 6          | 0   | 0   | 0   | 0   |

- $T(U = I)$ 

Since all inner nodes are **summing** nodes the duration of the process is as long as the depth of the tree and therefore $\implies T(I) = 4$


#### c)
![[Pasted image 20260524104451.png]]

We can take the counter example of a root, a node and a leaf.

``` mermaid
graph LR

r ---> 1
1 ---> l
```

We can see that if we include ($U = I = \{1\}$) or exclude ($U = \emptyset$) the node 1 in the set $U$, it won't change the time yet the sets are not equal.

#### e)

**The algorithm :**

![[WhatsApp Image 2026-05-24 at 11.01.29.jpeg]]
$CalcT(G,root):$
- $T \gets 0$
- $\text{If } root \in L :$
	- $return T$
- $\forall v \in children(root) :$
	- $T \gets max\left\{ T,CalcT(G,v) \right\}$
- return $T+1$

**Correctness :**

- Base : a root which is a leaf 

- Induction hypothesis : 
	Assuming that all child $c$ of some inner node $v$ , the algorithm returns the correct value $T_v$.

- Induction step : We need to prove that the the algo. returns the correct value $T_v$.
	We notice that since the algo. returns : 
	$$T_v = max\left\{ T_c | c - \text{child of v} \right\} + 1$$
	Since $U = I$, the transfer time of the vector from child $c$ to $v$ is 1.
	$v$ is a summing node and therefore needs to wait for all children to pass their vectors.
	Meaning, $T_v$ is the max between the children + the transfer time $(=1)$.