
## The problem

- undirected
- each process knows the entire graph
- start with $v$ , a fixed initial value
- For each process, there is exactly **one start state** containing each input 
- A limited number $\le f$   of processes might fail

- The goal is for all processes to output the same value.

#### Conditions for Correctness : 
1. **Agreement** - all nodes decide on same value.
2. a) **Validity** - if all nonfaulty processes start with the same initial value, $v \in V$ then $v$ is the only possible decision value for a nonfaulty process.
3. **Termination** - all nonfaulty processes eventually decide on a value

Alternative **Validity** condition :
2. b)  **Strong Validity** - any decision value for process is the initial value of some process

### Question 1

Solving a consensus with stopping failures.
Form an agreement in the stopping failure model, for the special case of a complete graph $K_n$ .


#### Assumptions 
$decision \in V \cup {unknown}, Some$ $v_0 \in V$ is given to all

#### Init for each process :
$Round = 0 , decision = unknown , W = \{ v_i\}$ 

#### Algorithm 

1. $Round \gets Round +1$
2. Let $X_i$ be the message received from some node $j$.
3. $W = W U \underset{1\le j \le i-1}{\cup}X_j$ 
4. if $Round \le f$ :
	1. Send $W$ to all
5. else if $|W| == 1$:
	1. $decision \gets W = \{v_i\}$
6. else :
	1. $decision = v_0$
7. **Halt**






