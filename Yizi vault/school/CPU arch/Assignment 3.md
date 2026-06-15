
## Question 1
![[Pasted image 20260613190324.png]]

```
g = 0; 
r = 0; 
s = 0; 
some_large_number = 1000000; 

do 
	for (j=0; j<5; j++) { 
		r++; 
	} 
	
	for (k=0; k<7; k++) { 
		s++; 
	} 
	
	g++; 
	
} while (g < some large number)
```

### a) Miss rate
![[Pasted image 20260614134532.png]]

We will count the amount of continuous and non continuous executions that each of the block in the code yields, sum all the continuous ones and divide by the total.


#### First loop 
```
for (j=0; j<5; j++) { 
		r++; 
} 
```

We need to analyze all of the instructions that happen in the loop in runtime :

- j=0 : we initialize the counter of the loop to be 0 in the first iteration only $\implies$ 1 continuous
- j<5 : we check the loop condition on the counter to know if to branch out of the loop. It is non-continuous only on the last iteration (j=5) when the condition is not satisfied $\implies$ 1 continuous, 5 non-continuous
- j++ : we increment the counter each iteration $\implies$ 5 continuous
- r++ : we increment the variable r each iteration $\implies$ 5 continuous
- j top_loop : we jump back to the top of the loop to the condition checking $\implies$ 5 non- continuous

| insturction\iter | 1   | 2   | 3   | 4   | 5   | 6   |
| ---------------- | --- | --- | --- | --- | --- | --- |
| j=0              | ✅   | --- | --- | --- | --- | --- |
| j < 5            | ✅   | ✅   | ✅   | ✅   | ✅   | ❌   |
| j ++             | ✅   | ✅   | ✅   | ✅   | ✅   | --- |
| r++              | ✅   | ✅   | ✅   | ✅   | ✅   | --- |
| j top_loop       | ❌   | ❌   | ❌   | ❌   | ❌   | --- |
overall we got : 
- ✅ 16 continuous instructions 
-  ❌ 6 non-continuous instructions 

#### Second Loop
```
for (k=0; k<7; k++) { 
		s++; 
} 
```

Applying the same logic we applied to the first loop :

| insturction\iter | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   |
| ---------------- | --- | --- | --- | --- | --- | --- | --- | --- |
| k=0              | ✅   | --- | --- | --- | --- | --- | --- | --- |
| k < 5            | ✅   | ✅   | ✅   | ✅   | ✅   | ✅   | ✅   | ❌   |
| k ++             | ✅   | ✅   | ✅   | ✅   | ✅   | ✅   | ✅   | --- |
| k++              | ✅   | ✅   | ✅   | ✅   | ✅   | ✅   | ✅   | --- |
| j top_loop       | ❌   | ❌   | ❌   | ❌   | ❌   | ❌   | ❌   | --- |
overall we got : 
- ✅ 22 continuous instructions 
-  ❌ 8 non-continuous instructions 

#### Outer Loop
```
do{ 
	
	{...}
	
	g++; 
	
} while (g < some large number)
```

Every outer loop yields one continuous instruction and one non continuous instruction.

overall we got : 
- ✅ 1 continuous instructions 
-  ❌ 1 non-continuous instructions 

#### Overall Ratio

Taking all previous considerations we get :
$$R_{continuous} = \frac{\text{\#continuous}}{\text{\#total instruction}} = \frac{16(\text{first loop}) + 22 (\text{second loop}) + 1(\text{outer loop})}{22+30+2} = \frac{39}{54} \approx 72.2\%$$

### b) One Bit Predictor
![[Pasted image 20260614160823.png]]

```graphviz
digraph{
    rankdir = LR ;
	"predict NT"->"predict T"[label = "actually T"];
    "predict NT"->"predict NT"[label = "actually NT"];

    "predict T"->"predict NT" [label = "actually NT"];
    "predict T"->"predict T"[label = "actually T"];
}
```

We re-evaluate the code block, this time while using a LTP:
#### First loop 
```
for (j=0; j<5; j++) { 
		r++; 
} 
```

Based on the previous table we made, we know that the sequence of entries for the first loop is :

| iter.      | 1           | 2   | 3   | 4   | 5   | 6   |
| ---------- | ----------- | --- | --- | --- | --- | --- |
| Branching  | T           | T   | T   | T   | T   | NT  |
| Prediction | NT(Default) | T   | T   | T   | T   | T   |
| Result     | ❌           | ✅   | ✅   | ✅   | ✅   | ❌   |
overall we got : 
- ✅ 4 correct predictions  
-  ❌ 2 incorrect predictions

#### Second Loop
```
for (k=0; k<7; k++) { 
		s++; 
} 
```

Applying the same logic we applied to the first loop :

| iter.      | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   |
| ---------- | --- | --- | --- | --- | --- | --- | --- | --- |
| Branching  | T   | T   | T   | T   | T   | T   | T   | NT  |
| Prediction | NT  | T   | T   | T   | T   | T   | T   | T   |
| Result     | ❌   | ✅   | ✅   | ✅   | ✅   | ✅   | ✅   | ❌   |
overall we got : 
- ✅ 6 correct predictions  
-  ❌ 2 incorrect predictions
#### Outer Loop
```
do{ 
	
	{...}
	
	g++; 
	
} while (g < some large number)
```

The predictor is initialized to the NT state so the prediction is always NT which is the correct prediction (except for the last iteration of the outer loop that is to be neglected...)

overall we got : 
- ✅ 1 correct prediction

#### LTP Hit Ratio

Taking all previous considerations we get :
$$R_{continuous} = \frac{\text{\#correct}}{\text{\#branchings}} = \frac{4+6+1}{6+8+1} = \frac{11}{15}$$

### c) Two Bit Predictor - Miss Rate
![[Pasted image 20260615132405.png]]

```graphviz
digraph{
    rankdir = LR ;

    "strongly predict NT"->"strongly predict NT"[label = "NT"];

	"strongly predict NT"->"predict NT"[label = "T"];
    "predict NT"->"strongly predict NT"[label = "NT"];

    "predict NT"->"predict T" [label = "T"];
    "predict T"->"predict NT"[label = "NT"];

    "strongly predict T"->"predict T"[label = "NT"];
    "predict T"->"strongly predict T"[label = "T"];

    "strongly predict T"->"strongly predict T"[label = "T"];
}
```

We re-evaluate the code block, this time while using a BMP:
#### First loop 
```
for (j=0; j<5; j++) { 
		r++; 
} 
```

Based on the previous table we made, we know that the sequence of entries for the first loop is :

| iter.      | 1           | 2   | 3   | 4   | 5   | 6   |
| ---------- | ----------- | --- | --- | --- | --- | --- |
| Branching  | T           | T   | T   | T   | T   | NT  |
| state      | ST(Default) | ST  | ST  | ST  | ST  | T   |
| Prediction | T           | T   | T   | T   | T   | T   |
| Result     | ✅           | ✅   | ✅   | ✅   | ✅   | ❌   |
overall we got : 
- ✅ 5 correct predictions  
-  ❌ 1 incorrect predictions

#### Second Loop
```
for (k=0; k<7; k++) { 
		s++; 
} 
```

Applying the same logic we applied to the first loop :

| iter.      | 1           | 2   | 3   | 4   | 5   | 6   | 7   | 8   |
| ---------- | ----------- | --- | --- | --- | --- | --- | --- | --- |
| Branching  | T           | T   | T   | T   | T   | T   | T   | NT  |
| state      | ST(Default) | ST  | ST  | ST  | ST  | ST  | ST  | T   |
| Prediction | T           | T   | T   | T   | T   | T   | T   | T   |
| Result     | ✅           | ✅   | ✅   | ✅   | ✅   | ✅   | ✅   | ❌   |
overall we got : 
- ✅ 7 correct predictions  
-  ❌ 1 incorrect predictions
#### Outer Loop
```
do{ 
	
	{...}
	
	g++; 
	
} while (g < some large number)
```

The predictor is initialized to the ST state so the prediction is T for the entire loop except for the last iteration when the predictor predicts T when in fact it is NT.

overall we got : 
- ✅ 1 correct prediction

#### BMP Hit Ratio

Taking all previous considerations we get :
$$R_{continuous} = \frac{\text{\#correct}}{\text{\#branchings}} = \frac{5+7+1}{6+8+1} = \frac{13}{15}$$

### d) Local Predictor
![[Pasted image 20260615160425.png]]

The assumption that a large enough number of the while loop iterations were finished lets us assume that the Pattern History Table of the predictor is already filled and stabilized.

#### First loop 

| iter.     | 1   | 2   | 3   | 4   | 5   | 6   |
| --------- | --- | --- | --- | --- | --- | --- |
| Branching | T   | T   | T   | T   | T   | NT  |
Since the sequence is repeating for the first loop and it is of length 6, from a discussion in class we concluded that it can be predicted with 100% accuracy using a local predictor with a history buffer of length 5, which fits our case exactly.

overall we got : 
- ✅ 6 correct predictions  $\implies$ 100%

#### Second Loop

| iter.     | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   |
| --------- | --- | --- | --- | --- | --- | --- | --- | --- |
| Branching | T   | T   | T   | T   | T   | T   | T   | NT  |
For the second loop the assumption regarding the length of the predictor does not hold so we need to re-evaluate the situation.

For the following entries we can assume that the predictor will converge to the states yielding 100% prediction accuracy since every time those subsequences appear the following branching is always a T : `11110`, `11101`,`11011`,`10111`,`01111`

The only case left to evaluate is the entry of `11111`.
We know that for the second loop the subsequence appears three times :

- iteration 6  $\implies$ T
- iteration 7  $\implies$ T
- iteration 8  $\implies$ NT

We can deduce that the FSM for the entry of `11111` will always be in either the ST state or the T state when both states predict T.

overall we got :
- ✅ 7 correct predictions
- ❌ 1 incorrect prediction

#### Outer Loop

| Iter.     | 1   | 2   | 3   | ... |
| --------- | --- | --- | --- | --- |
| Branching | NT  | NT  | NT  | NT  |

We can see that the while loop branching sequence is a constant sequence of NT and therefore from a certain point, the predictor will always see the subsequence `11111` and predict NT correctly.

overall we got : 
- ✅ 1 correct prediction

#### Local Predictor Hit Ratio

Taking all previous considerations we get :
$$R_{continuous} = \frac{\text{\#correct}}{\text{\#branchings}} = \frac{6+7+1}{6+8+1} = \frac{14}{15}$$

## Question 2
![[Pasted image 20260615172955.png]]
![[Pasted image 20260615173015.png]]

### a) Fill in Table 

```
y = [18,13,10,11,12,20,27,30,33];

for y_i in y :
	
	if y%2 == 0 :
		r++;
		
	if y%10 == 0 :
		s++;
```

**g = 0 :**

|           | 18  | 13  | 10  | 11  | 12  | 20  | 27  | 30  | 33  |
| --------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| b1 pred   |     |     |     |     |     |     |     |     |     |
| b1 actual | ✅   | ❌   | ✅   | ❌   | ✅   | ✅   | ❌   | ✅   | ❌   |
| b2 pred   |     |     |     |     |     |     |     |     |     |
| b2 actual | ❌   | ❌   | ✅   | ❌   | ❌   | ✅   | ❌   | ❌   | ❌   |
**g = 1 :**

|           | 18  | 13  | 10  | 11  | 12  | 20  | 27  | 30  | 33  |
| --------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| b1 pred   |     |     |     |     |     |     |     |     |     |
| b1 actual |     |     |     |     |     |     |     |     |     |
| b2 pred   |     |     |     |     |     |     |     |     |     |
| b2 actual |     |     |     |     |     |     |     |     |     |
| b2 actual |     |     |     |     |     |     |     |     |     |
