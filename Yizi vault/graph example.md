
#### graph example using mermaid
```mermaid
graph LR;
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

>[!info]
>[[lecture 5#Building the _ELG_ tree]]


## Story time... (By eyal the _Gay_)

>[!note]-
>You basic bitch!

>[!success]- 
>I live still!
>>[!check]- 
>>I am alive, I'm not lying...

>[!warning]-
>Life is getting hard, be warned.

>[!caution]-
>Hey!
>There's a pit there!

>[!fail]-
>In life mostly...

>[!missing]-
>A life.
>>[!note]-
>>Haha
>>Missing a life while not having it - A PARADOX. WOW

>[!example]-
>Example for what?
>I know literally nothing

>[!question]-
>What is the meaning of life?

>[!help]-
>Im stuck in a pit :(
>A fucking pit would you believe it?
>You would think there would be a warning or a caution sign...

>[!quote]-
>"It's a dangerous business, Frodo, going out your door, if you don't keep your feet there is not knowing where you might be sept of too." -Billbo Baggins-
>>[!cite]-
>>Lord of the Rings
>
>>[!note]-
>>Its a nice quote you know, adventures and stuff.
>>pretty fun...

>[!info]-
>For youtrinformation, there was a pit there, just so you know...

>[!abstract]-
>My whole life is one big abstract.

>[!todo]-
>1. Get a life.
>2. Do something with it.

>[!tip]-
>Be careful of pits.
>And look at signs, they are there mostly.

>[!bug]-
>Sometimes there are no signs and you just have to look WITH YOUR FUCKING EYES!!!