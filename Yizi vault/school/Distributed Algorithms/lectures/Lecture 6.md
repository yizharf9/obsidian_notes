---
cover: "[[Lecture 6 cover.png]]"
tags:
  - lecture
Last Lecture: "[[Lecture 5]]"
---
## Agreement Problem with Byzantine Falls:
We saw the `EIG Tree` algorithm for solving the problem but it uses a lot of messages and information.

>[!info] EIG
>You can see more about that in [[Lecture 4#Exponential Information Gathering - EIG]]
### BBA - Binary Byzantine Agreement:
For solving the problem in a more efficient way, we can solve the problem as such:
We will show that using a smart translation we can transform our problem to one where the inputs are $1$ and $0$, and then we will show how to efficiently solve the problem with binary inputs.

>[!info] Turpin-Coan
>You can see more about that in [[Lecture 5#BBA - Binary Byzantine Agreement]]

>[!question]
>How do we deal with the problem while there are binary inputs in a more efficient way?
>
>>[!solution]-
>>The solution in composed from two corner stones:
>> 1. We will build a mechanism - `Consistant Broadcast`, which purpose is a guarantee of message arrival.
>> 2. We will use the `consistant broadcast` in order to solve the problem.
>

---
#### Consistant Broadcast:
These are the conditions that need to be met in the mechanism of `consistant broadcast`:
1. If a non-fallen computer $i$ sends a message $(m,i,r)$ at step $r$, then this message must be approved by all the non-fallen computers at step $r$ or step $r+1$.
2. If a non-fallen computer $i$ didn't send a message $(m,i,r)$ at step $r$, then this message will never be approved by any non-fallen computer.
3. If some message $(m,i,r)$ is approved by non-fallen computer $j$ at step $r'$, then it must be approved by all non-computer at step $r'$ or $r'+1$.

**The mechanism:**
- In order to send a message $(m,i,r)$ by computer $i$ at step $r$, computer $i$ sends a message: $(init, m, i, r)$ to all computer at step $r$.
- If computer $j$ receives $(init,m,i,r)$ from computer $i$ at step $r$, it sends everyone at step $r+1$ a message: $(echo,m,i,r)$.
- If before step $r+2$ a computer received at least $f+1$ $(echo,m,i,r)$ messages, then $j$ sends $(echo,m,i,r)$ (if not sent already).
- If by the end of step $r+1$ a computer received at least $n-f$ $(echo,m,i,r)$, then he approves the message.

**Why does it work?**
1. At step $r+1$ every non-fallen computer has received at least $n-f$ `echo` messages, and by the last dot, every non-fallen computer will approve the message.
2. The liars can't affect the creation of more than $f$ `echo` messages, therefor they can't cause an approval of a fictive message.
3. Assuming computer $j$ has approved some message:
	1. He saw at least $n-f$ `echo` messages.
	2. From them at least $n-2f$ `echo` messages from valid computers.
	3. $n-2f\ge f+1 \implies$ computer $j$ saw $f+1$ valid `echo` messages and thus all other valid computers saw $f+1$ `echo` message.
	4. This guarantees that by the next step, there will be $n-f$ `echo` messages.
	5. Thus, by the last dot, every valid computer will approve that message.

##### Poly-Byz Algorithm:
#algorithm - poly-byz.

The algorithm works in $f+1$ basic steps.
Every step is composed of two stages.
All messages that are sent are of the form $(1,i,r)$.

**The algorithm:**
- **Step $1$:** Valid computer $i$ sends a message $(1,i,1)$ if the start value for $i$ is $1$.
- **Step $2s-1$:** $2\le s\le f+1$. Valid computer $i$ sends a message $(1,i,2s-1)$ if $i$ received at least $f+s-1$ messages from different computers and didn't send yet. 
- **decision:** After $2f+1$ steps, $i$ decides $1$ if it received at least $2f+1$ messages, else $0$.
---
### Aproximate Byzantine Agreement:
**Agreement:** It is allowed to agree on a value as far as $\varepsilon$ : $|d_i-d_j|\le \varepsilon$.
**Attack:** Every decision value must be at the range of input values of non-fallen computers.
**Finish:** All non-fallen computer must decide.

>[!info]- Inefficient valid algorithm
>A valid solution is to take the median from all received values. This way everyone decide on the same value $\to \varepsilon = 0$.
>This is not efficient since epsilon is not used.

#### Definitions:
#definition - reduce, select, mean.
Let there be a group $U$ of at least $2f$ values $u_1,u_2,\dots ,u_k$ in a non decreasing order.
**reduce:** $reduce(U)=u_{f+1},u_{f+2},\dots, u_{k-f}$
**select:** $select(U) = u_1, u_{f+1},u_{2f+1},\dots$
**mean:** $mean(U) = {1\over k}\displaystyle\sum_{i=1}^{k}u_i$
#### The algorithm:
#algorithm - aprox. byzantine agreement
- Assuming $val_i$ is an initial value for computer $i$.
- $i$ sends everyone (including itself) $val_i$, and gathers all values that have been received at this step.
- If someone is missing then $i$ replaces it with a default value.
- Marking by $W$ the set of values that $i$ gathered (including replacements), $i$ determines: $val_i = mean(select(reduce(W)))$.
- In the next iterations, we continue with regard to $\varepsilon$.

#### Lemmas:

>[!example] #Lemma **Lemma 1:**
>Assume $val_i=v$ after step $r$.
>Then $v$ is guarantee to be in the range of the inputs of valid computers before step $r+1$.
>**proof:**
>$W_i$ is a set of values that computer $i$ gathered at step $r$.
>From then, $f$ can belong to liars.
>Therefor, at the moment we perform $reduce(W_i)$ all other values that remain are in the range of values of valid computers and thus also $mean(select(reduce(W_i)))$ is in the range.

>[!example] #Lemma **Lemma 2:**
>Let $Val_i = v$ and $Val_{i'} = v'$ be values of computers $i$ and $i'$ after $r$ steps. 
>thus, $|v-v'|\le{d\over{\lfloor{n-2f-1\over f}\rfloor+1}}$ where $d$ is the range of values before step $r$ .
>**Proof:**
>Assume that $i$ gathered $W_i$ and $i'$ gathered $W_{i'}$.
>$S_i = select(reduce(W_i))$ and $S_{i'}=select(reduce(w_{i'}))$.
>$c = \lfloor{n-2f-1\over f}\rfloor + 1 = |S_i|=|S_{i'}|$
>How many elements are there in $S_i$ and $S_{i'}$.
>
>>[!example]- **Assisting Lemma 1:**
>>$|reduce(W_i)-reduce(W_{i'})|\le f$.
>>Proof: 
>>Looking on $|W_i-W_{i'}|\le f$ thus the lemma holds.
>>If we delete the smallest element in $W_i$ and $W_{i'}$ it will not affect the difference, because if it is the same element it will not change it, and if they are different the difference remains the same.
>
>>[!example]- **Assisting Lemma 2:**
>>$u_j\le u'_{j+1}$ and $u'_j\le u_{j+1}$, where $S_i=u_1,u_2,\dots, u_c$ and $S_{i'}=u'_1,u'_2,\dots ,u'_c$.
>>Proof:
>>$u_j$ is element $((j-1)\cdot f + 1)$ of $reduce(W_i)$.
>>$u'_{j+1}$ is element $(j\cdot f + 1)$ of $reduce(W_{i'})$.
>>By A`ssisting Lemma 1`, There are at most $f$ elements of $reduce(W_{i'})$ that are not of $reduce(W_i)$, therefor $u_j\le u'_{j+1}$.
>
Back to `Lemma 2`: $$\begin{align*}
|v-v'| &= |\text{mean}(S_i) - \text{mean}(S_{i'})| \\
&= \frac{1}{c} \left| \sum_{j=1}^{c} |u_j - u'_j| \right| \\
&\le \frac{1}{c} \sum_{j=1}^c |u_j - u'_j| \\
&= \frac{1}{c} \sum_{j=1}^c (\max(u_j, u'_j) - \min(u_j, u'_j)) \\
&\le \frac{1}{c} \sum_{j=1}^{c-1} (\min(u_{j+1}, u'_{j+1}) - \min(u_j, u'_j)) + \frac{1}{c} (\max(u_c, u'_c) - \min(u_c, u'_c)) \\
&= \frac{1}{c} (\max(u_c, u'_c) - \min(u_1, u'_1)) \\
&\le \frac{d}{c}
\end{align*}$$


>[!question]
>How do make the algorithm more efficient?
>>[!solution]
>>As soon as someone has finished, it can send a `finish` message to everyone, so they finish.
>>If we receive at least $f+1$ `finish` messages, we finish.
