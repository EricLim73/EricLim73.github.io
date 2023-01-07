---
title: "[C++]-Starting-with-Basics"
date: 2022-11-10 13:42:00+0900
categories: [C_C++, C++]
tags: [Study, Basic]
math: true
---

# Basic C/C++
    지금까지 배운 C와 C++를 완전 바닥부터 다시 복습 + 공부하고 그걸 기록하기 위한 포스트입니다.


### [ Basic syntax & info ]

- Comment   
Opening and closing a line with **" // "** will turn that line into a <span style="color:yellow">`*Comment*`</span>

```c++
// This is how you put comment in C/C++
```

- Data type / Variable name

```c
#include <stdio.h>
//  argc    = argument count
//  argv[N] = arguments 
int main(int argc, char** argv){

    // Data type = int(4byte)
    // Variable name = "i"
    int i = 0;


    return 0;
}
```

For Data type we can group them to two groups => Integer type / Real Number type

| Integer (byte)    | RealNumber (byte) | Logical (byte)
|:------------------|:------------------|:---------------
| char (1)          | float (4)         | bool (1)
| short (2)         | double (8)        |
| int (4)           |                   |
| long (4)          |                   |
| long long (8)     |                   |

<!--<span style="color:green">**[ TIP ]**</span>-->

 >  **1 Byte = 8 bit   
    1 KB = 1024 byte   
    1 MB = 1024 KB
    1 GB = 1024 MB   
    and it goes on ... {: .prompt-tip }
 
 >  Choose wisly what variable to use. 
    If for example lets say you choose "int" as HP_data storage.  
    when an update increases some monsters hp above 4byte boundary, it insta-kills that sucker... 
 {: .prompt-tip }


> **int** 와 **long** 둘다 4byte인걸 알 수 있다. 사실 long을 쓸 생각이였는데 int를 만들어서 쓰다보니 이게 더 예뻐보여서 자주 쓰다보니 퍼졌다고 한다...  
 그래서 int의 경우 *운영체제에 따라 크기를 다르게 인식할 수 있다*... long을 어딜가도 4 byte라고 한다. 
 {: .prompt-info }
 
 <br></br>


- if statment

```c
#include <stdio.h>
int main(int argc, char** argv){
    int a = 0;
    char c = 'A';
    //  Condition based on set rules
    if(c == 65)             //  Ascii : A = 65(10), 0x41(16)
        printf("c is A");   //  can ignore {} if one line
    
    //  can branch on with different conditions using if-else & else
    if(a == 0){
        printf("a is 0\n");
    }
    if else(a == 1){
        printf("a is 1\n");
    }
    else{
        printf("a is smth else\n");
    }
    return 0;
}
```

- switch/case

```c
#include <stdio.h>
int main(int argc, char** argv){
    int a;
    switch(argc){
        case 1:
            printf("1 arg");
            break;              //  without break, if argc == 1 than
        case 2:                 //  we run everything bellow in order, so we need to "break" after a case( sometime ignore for niche usecase )
            printf("2 arg");
            break;
        case 3:
            printf("3 arg");
            break;
        default:                //  For out bound conditions
            printf("more than 3 arg");
            break;
    }
    
    return 0;
}
```

- For / While/ do-while  
Basic looping following certain condition

```c
#include <stdio.h>
int main(int argc, char** argv){

    for(int i = 0; i < 10; ++i>){
        printf("%d\t", i);      //  \t for tab. prints out "1   2   ..."
    }

    int condition = 10;
    while(condition > 0){

        if(condition%2==0)      //  짝수인 경우 "continue"로 인해 
            continue;           //  이번 루프를 그냥 넘긴다.(for에서도 사용가능)
        
        printf("condition = %d\t", condition--);
        if(condition == 2){
            printf("no getting out during condition == 2\n");
            break;              //  using break gets you out of loop
        }
        printf("%d\n",condition);
    }

    //  unlike "while", "do-while" will run at least once then check for while
    int condition_2 = 0;
    do{
        printf("looping do-while\n");
    }while(condition_2 == 0);

    return 0;
}
```

- Macro  
Anything strting with **#** gets computed first during compiling. **#define** substitutes given context to target.

```c
#include <stdio.h>

#define MAX_INT 100

int main(int argc, char** argv){
    printf("%d\n", MAX_INT);    //  prints 100
    return 0;
}

```

### [ Variable / Data type ]
> Every data has its name & type explaining what it is.

```c
#include <stdio.h>
int main(int argc, char** argv){

    // Data type = int(4byte)
    // Variable name = "i"
    int i = 0;
    
    // 2^8 = 256 가지  ==> 0 ~ 255까찌 양의 정수 표현가능
    unsigned char c = 0;    

    //  Once declared, you can use this variable and
    // assign(=) it with various data
    c = 0;
    c = 25;
    c = 255;

    c = 256;
    //  output function: printf();
    // %d: for integer variable 
    // \n: equivalent to new_line
    printf("(A) %d\n", c);  // (A)

    //  When not specified, variables are considered as "Signed"
    //  1byte range for signed char : -128 ~ 0 ~ 127 
    //  Total 256가지 경우
    char sc = 0;
    sc = -1;
    printf("%d\n", sc);  // prints out -1
    sc = 256;            // (B)
    printf("%d\n", sc);  // prints out -1 ?!

    return 0;
}
```

**(A) :** If you think about how bits are stored, *256* exceeds one bit making it `1 0000 0000`. *char* can store 8 bits... so what do we do with that "1" at the front.  
Simple! We throw it away. Printing *c* will give you "0" as a result.


**(B) :** How does this work? Well we use the first bit to identify + / -.   
    
    EX) <10 base> 11            <10 base> -11        
        <2  base> 0000 1011     <2  base>  1000 1011

The leftmost side of the bit indicates **+** with **0** and **-** with **1**.
We call this ***MSB (Most Significant Bit)***

***BUT*** computer DOES NOT store negative values like this(but uses this concept).
To understand this, you need to understand how electronics calculate negative number and whats known as ***2's Complement.***


### [ 2's Complement ]
> Subtraction is just addition with - symbols in them.

This is exactly how machine calculate negative numbers, or subtraction itself.  
Lets say we have a number, something like 127. If we want *-127*, the addition between bit representing *127* and *-127* must result in *0*.

    EX)     0111 1111               @ (A) seems to have a pattern with its counter part 127
            1000 0001   (A)
        +)____________
          1 0000 0000   = 0000 0000  
          # We dont care about "1", its just a carry that is out of bound

The pattern is that you flip the original bit, and add 1 bit at the end! This is how you calculate ***2's Complement***.

```c
#include <stdio.h>
int main(int argc, char** argv){

    // Data type = int(4byte)
    // Variable name = "i"
    int i = 0;
    
    // 2^8 = 256 가지  ==> 0 ~ 255까찌 양의 정수 표현가능
    unsigned char c = 0;    
    c = 255;            // (A)
    printf("%d\n", c);  // prints 255  

    char c1 = 0;        // (B)
    c1 = 255;
    printf("%d\n", c1); // prints -1

    // same goes to "unsigned char c"
    // c = -1 will make "c" store 255

    return 0;
}
```

(A) and (B) at its core are the same, meaning that bit wise its the same. What differentiates between the two is the perspective(aka DataType) that we take when using them in our program.  
If this doesn't make any sense, just think about your family member. *i.e)* To you, that kid running around the house is reconized as "little bastard" aka your little brother. Your mom however sees *that thing* as her "son".    

<br>

### [ Floating point ]

> Computers war equally dumb as human. They can't caluculate 4.12 + 0.34 with 100% accuracy

```c
#include <stdio.h>

int main(){
    int num = 4 + 4.0;      //  (A)
    printf("%d\n", num);    // prints 8
    return 0;
}
```

The code above is not just simple 4+4.0=8 problem. computer sees *4* and *4.0* as totally different type of value. Our computer understands the above program as 
> "Oh! Looks like this dumb human is going to store an integer data through some caculation. I first need to  ***cast*** *4.0* into an integer then add it with *4*."

Why is this a problem in the first place?  
Short answer, casting it implicitly might not be your intention in the first place + performance cost(not a big deal but still). 
Then why can't it just caluculate as *8* right away?. Its because computers with its binary system just can't figure out how to represent real numbers. To solve this dilema, we gave up accuracy(not much but still makes floating numbers not 100% accurate)

This is how floating numbers are stored

    <Floating Number>
        21.8125
        [Integer Part]      21      ->  0001 0101
        [RealNumber Part]   .8125   -> .0001 1010   
        (A)   .11010                    
                1 * 0.5                     
                1 * 0.25                (B) 0 000 0000 0000 0000 0000 0000 0000 0000
                0 * 0.125                   S|Integer-----------|RealNumber---------
                1* 0.0625  
                0 * 0.03125 
            +)______________ = .8125 

(A) might be little confusing. Think of 10 base decimals. we need *10* 0.1's to make it **1.0**. *10* of 0.01's will make **0.1**. So we can say that *0.1* as ***1/10*** and *0.01* as  ***1/100***. This rule can be applied to binary as well!. We need *2* 0.1's to make it **1.0**. we need *2* 0.01's to make it **0.1**. ***With the information above***, 0.1(2) can be represented as 0.5(10), 0.01(2) as (0.25), 0.001(2) as (0.125), and etc... This way of representing realNumber is what we call `Fixed Point Precision`. 32-bit representation for this is explained in (B).
Expression like (B) has its limitations(we can't express numbers over given boundary). Since most modern processors have fast **Floating-Point Unit (FPU)**'s, this way of representing floating number are now used for specific use case. We now use whats called ***Floating-Point Arithmetic***. 

    [Floating Point Arithmetic]
                21.8125(10) =   10101.11010(2)
        
        0.218125(10) * 10^2 =   0.1010111010(2) * 2^5

        0.1010111010(2) * 2^5  -->  [float] 0|000 0010 1|101 0111 0100 0000 0000 0000

        < IEEE 754 Standard >
            [32-bit] 0 000 0000 0000 0000 0000 0000 0000 0000
                     S|Exponent-|Mantissa--------------------
            bit  ->  1 8         23
            [64-bit] 0 000 0000 0000 0000 0000 0000 0000 0000 0000 0000 0000 0000 0000 0000 0000 0000
                     S|Exponent-----|Mantissa--------------------------------------------------------
            bit  ->  1 11            52

Either way of representing floating number has its flaw, mainly accuracy problems. **Floating Point Precision** or **Fixed Point Precision** occur because of how we calculate the numbers after the decimal point; by combining smaller numbers.   
Lets say we want to represent **0.724561**. Obviously we would need *0.1(2)* to start with, but what about *0.01(2)*?
Adding it would give us 0.75(10), which clearly seems like it went out of bound! So inorder to express **0.724561**, we need smaller decimal numbers(we dont even know if its possible...). This is the reason why when you do stuff like

```c
    ...
    float fn = 0.0f;
    // some trigonometry
    ...
    //end
    if(fn == 1.0f)
        printf("GOOD!");    // Can't confirm 100% this would work
    ...
```

*fn* can store something like ***0.99999999999999999981***. Even though calculation by hand shows that *some trigonometry* returns **1.0**, fn might store it differently.

> TLDR: binary representation for RealNumber follow set of rules depicted above. Our problem of **inaccuracy** is caused because of how we store decimal numbers. Looking at the format written above, we can easly see that larger bit-length can store more information, resulting in higher accuracy.   
 {: .prompt-tip }

Back to how C/C++, *float* values are written with **f** at the end. RealNumber without it is considered as *double*.
Try not to caculate different data type in one go. If needed, explicitly cast the operand to match the type.

```c
    int num = 4;
    float fn = 10.312f + (float)num;   
```


## End
Covered stuffs that i forgot over the years...

>   [Reference]   
    *80%* [아소트락 2021 C/C++ 강의](https://www.youtube.com/playlist?list=PL4SIC1d_ab-aOxWPucn31NHkQvNPHK1D1)  
    *10%* [모두의 코드](https://modoocode.com/138)  
    *10%* [The Cherno Youtube Channel](https://www.youtube.com/channel/UCQ-W1KE9EYfdxhL6S4twUNw)

