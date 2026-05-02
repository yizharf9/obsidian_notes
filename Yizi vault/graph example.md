
#### graph example using mermaid
```mermaid
graph TD;
id1((2)) --> id2((7));
id1((2)) --> id3((5));
id2((7)) --> id4((2));
id2((7)) --> id5((10));
id2((7)) --> id6((6));
id3((5)) --> id7((9));
id7((9)) --> id8((4));
id6((6)) --> id9((5));
id6((6)) --> id10((11));
```

```mermaid
block-beta
    columns 3
    
    %% Top Row
    n2["(2, 17)"] 
    space:1
    n3["(3, 75)"]

    %% Middle Spacer Row to stretch vertical distance
    space:3

    %% Bottom Row
    n1["(1, 11)"] 
    space:1
    n4["(4, 33)"]

    %% Connections with specific directions to force the 'X'
    n2 <--> n3
    n1 <--> n4
    n2 <--> n1
    n3 <--> n4
    
    %% Diagonal "X" connections
    n2 <--> n4
    n3 <--> n1

    %% Styling for better visibility
    style n1 fill:#1a1b26,stroke:#7aa2f7,stroke-width:2px,color:#fff
    style n2 fill:#1a1b26,stroke:#7aa2f7,stroke-width:2px,color:#fff
    style n3 fill:#1a1b26,stroke:#7aa2f7,stroke-width:2px,color:#fff
    style n4 fill:#1a1b26,stroke:#7aa2f7,stroke-width:2px,color:#fff

```

```mermaid
block-beta
    columns 3
    
    %% Top Row
    n2("S") 
    space:1
    n3("v1") 

    %% Middle Spacer Row to stretch vertical distance
    space:3

    %% Bottom Row
    n1("v2") 
    space:1
    n4("v3")
    space:1
    n5("v4")

    %% Connections with specific directions to force the 'X'
    n2 <--> n3
    n1 <--> n4
    n2 <--> n1
    n3 <--> n4
    n5 --- n4
    
    %% Diagonal "X" connections
    n2 <--> n4
    n3 <--> n1

```

#### code block in c

```
#include stdio;
#define NUM_STAGES 6;

void main{
int i = 0 ;

	for( i=0 ; i<NUM_STAGES ; i++){
		if (i%3 == 0){
			printf("multiple of 3!")
		}
	}
}
```

