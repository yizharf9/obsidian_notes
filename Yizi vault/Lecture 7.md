
### Probabilistic Algorithm - for the case of byz. failures

- Assuming that a coin flip is global - meaning that all processes have access to the same realization of the random variable of the coin.
- We assume that the number of failures are $f \lt \frac{n}{8}$ 
- The inputs satisfy $i \in \{0,1\}$

####  #algorithm  for the $i^{th}$ process

1. $vote = b_i$
2. Broadcast vote to the rest of the processes
	- denote $maj$  as the majority vote out of all zeros and ones that were received 
	- denote $tally$ as the amount of the majority vote.
3. Flip a fair coin.
	- if $coin = HEAD$ then we set $thresh = \frac{5n}{8} + 1$
	- else, we set $thresh = \frac{6n}{8} + 1$
	- if $tally \ge thresh \implies vote = maj$ 
	- else $tally \lt thresh \implies vote = 0$ 
4. if $tally \ge \frac{7n}{8} \implies d_i = maj$

Since the probability of continuing for another round without decision is $p=0.5$, we get :
$$
\mathbb{E}[\#steps] = \frac{1}{1-p} = \frac{1}{1-0.5} = 2 \ Steps
$$


### Ben-Or's Algorithm - for the case of stopping failures

- The algorithm assumes $f\lt \frac{n}{2}$
- We denote the input bit as $a_i \in \{0,1\}$

####  #algorithm  for the $i^{th}$ process

1. $r=1$
2. repeat
3. broadcast $(a_i,r)$
4. We observe the first $n-f$ messages that were received with fields $(a,r)$ :
	1. if all messages hold the same value of $r$ $\implies b_i = v$
	2. else $\implies b_i = null$ 
5. broadcast $(b_i,r)$
6. We observe the first $n-f$ messages that were received with fields $(b,r)$ 
	1. if all messages are identical $\implies a_i,d_i = v$
	2. else if not all messages are null $\implies a_i = \text{that value}$
	3. else $\implies a_i = \{0,1\} \ w.p. 0.5$ 
7. $r\gets r+1$ 


We denote as $a_{i,r},b_{i,r}$ as the $a$ and $b$ of process $i$ in stage $r$.


## #Lemma 

$$\forall r \in \mathbb{N} : b_{i,r} \in \{0,null\} \lor b_{i,r} \in \{1,null\}$$

**Proof :**

We assume by contradiction that the opposite happens :
- $n-f$  - zeros
- $n-f$  - ones
- $\implies 2n-2f , f \lt \frac{n}{2}$

Agreement - Assuming that in stage $r$, process $p$ decides 0, And that happens in stage $r$ for the first time. We claim that until the end of stage $r+1$ everyone agrees 0.
$\implies$ That means that in the end of stage $r$ it got $n-f$ containing 0. Out of all of them $n-2f \ge 1$ are messages that failed up until now. They contain 0 therefore every other process that did not fail got a message containing 0 in the end of stage $r$.

## K - agreement Problem

- The network is a complete graph with $n$ processes - $K_n$ 
- Up to K different decisions are allowed
- We notice that for $k=1$ we get the original problem from the beginning of the course
	- stages - $\mathcal{O}(f+1)$
	- messages - $\mathcal{O}((f+1)n^2)$ 


### #algorithm 

- for $\lfloor \frac{f}{k} \rfloor +1$ do :
	- Broadcast $\underset{1\le i \le r}{min}\{m_i\}$ 

#### Correctness 

$M(r) :=$ the set of minimal values of processes that did not fail after $r$ stages.
We will prove that : $\forall r \in \mathbb{N} : M(r) \le M(r-1)$

Let $d \in \mathbb{N}$ . If at most $d-1$ processes fail during stage $r : \ 1 \le r \le \lfloor \frac{f}{k} \rfloor + 1$ 
then $M(r) \le d$, meaning that there are at most $d$ different minimum values for processes that did not fail after stage $r$.

We assume by contradiction that at most $d-1$ fail in stage $r$ but $M(r) \gt d$ .
Let $m$ be the maximum value in $M(r)$ and let there be $m' \in M(r)$ another value where $m \ne m'$

From definition we can derive that : $M(r) \subseteq M(r-1) , m' \in M(r-1)$, thus $m'$ was the minimal value of some process $i'$ after $r-1$.

At step $r$ , $i'$ broadcasts $m'$ and therefore $i'$ failed at step $r$ because otherwise $m$ could not be in $M(r)$.

Since we chose $m'$ arbitrarily, that holds for every process that holds a minimal value in $M(r)$ different than $m$.
$$M(r) = \{m,m',m'',\dots \} \implies |M(r)| \ge d+1$$
It  holds that at least $d$ processes need to fail but we assumed that at most d-1 fail 
$\implies$ contradiction!

All that is left to show is that after $\lfloor \frac{f}{k} \rfloor + 1$ stages we will have at most k decisions...

Assuming that the amount of decisions is $\lt k$ .

meaning that the amount of the minimal values after $\lfloor \frac{f}{k} \rfloor + 1$ is at least $k+1$,
$$\implies M(\lfloor \frac{f}{k} \rfloor + 1) \ge k+1$$
$$\implies M(r) \ge k+1 \ : \ 1 \le r \le \lfloor \frac{f}{k} \rfloor + 1$$
then how many failures were at stage $r$ ? $\implies$ at least k!

$\implies M(r) \le M(r-1)$
Failures : $$\underbrace{(\lfloor \frac{f}{k} \rfloor + 1)}_{\text{num of stages}} \cdot \underbrace{k}_{\text{failures in each stage}} = f + k \implies \text{Impossible!}$$

## Failure Detectors - 8 types


> [!Example] 
> ACK(N) - the acknowledgement  in communication protocols.

**Property - Completeness :**

- Strong Completeness - every process that fails is recognized by **all other** processes.
- Weak Completeness - every process that fails is recognized by **at least one** other process.

**Property - Accuracy :**
- Perpetual Strong Accuracy - processes never suspect a non-failing process.
- Perpetual Weak Accuracy - processes never suspect a specific non-failing process.

- Eventual Strong Accuracy - processes don't suspect a specific non-failing process starting from some Unknown specific time.
- Eventual Weak Accuracy - processes never suspect a specific non-failing process starting from some Unknown specific time.

