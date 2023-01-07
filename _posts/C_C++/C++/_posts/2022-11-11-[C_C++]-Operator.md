---
title: "[C++]-Operator"
date: 2022-11-11 10:54:00+0900
categories: [C_C++, C++]
tags: [Study, Basic]
math: true
---

# Basic C/C++
    지금까지 배운 C와 C++를 완전 바닥부터 다시 복습 + 공부하고 그걸 기록하기 위한 포스트입니다.

### [ Operator - Arithmetic]
> Its faster to just look at it.

```c
#include <stdio.h>
int main(int argc, char** argv){
    //  Basic arithmetics
    //  +, -, *,  /, %(modulo)
    int data = 10 + 10;
    data + 20;          //  this is just wrong. Sure 20+20=40, but its not stored anywhere!
    data = data + 10;   // This works. resulting 30
    data += 10;         // Different syntax doing the same thing. resulting 40

    //  Division need extra care
    //  To find the remainder of division from int we use modulous %
    data = 10 / 3;
    printf("%d\n", data);   //  prints "3"
    float remainder = 10 % 3;
    printf("%f\n", remainder);   //  prints "0.3333..."

    // WE CAN"T USE MODULOUS on Floating Number!!
    float f1 = 10.0f;
    float f2 = 3.0f;
    f1 = f1 % f2;   //  WRONG!!!! Think about it. Real number division does not give remainder anyway...
    f1 = f1 % data; //  This is even worse.... type different + remainder from floating number? wtf...

    data = f1 / f2; //  "f1 / f2" results in 3.33333, so there is gonna be type-casting.
                    //  Compiler would give us a "warning" telling us that it did its type-casting 
                    //  but some data will get lost(numbers after the deciaml point)

    data = (int)(f1/ f2);   //  explicitly type-cast would help


    //  ++ --
    //  We don't need "assign" operator to store calculated result
    int num = 1;
    num++;
    printf("%d\n",num); // prints 2
    num--;
    printf("%d\n",num); // prints 1
    //  Basic data-type is easy, plus / minus 1. 
    // However used in other operands such as pointers or specific struct(class) can differ from just adding|subtracting one.

    //  ordering of ++,-- matters
    //  IT'S GOOD PRACTICE TO USE ++var instead of var++.(tldr; copy constructor)
    printf("%d\n",++num); // prints 2
    printf("%d\n",num++); // prints 2, num adds 1 to itself
    printf("%d\n",num); // prints 3

    return 0;
}
```
 >  [Important TIP]
    **Always check if you used your data-type as intended**       
    **CAN'T use Modulous % operator on float, double. It's meaningless anyway**   
    **It's GOOD PRACTICE to use (*++* or *--*)var rather than var(*++* or *--*)**   
 {: .prompt-tip }

<br>

### [ Operator - Logical]
> Its faster to just look at it.

```c
#include <stdio.h>
int main(int argc, char** argv){
    //  AND OR NOT
    //  &&  ||  !
    //  True False
    //  Anything else than 0 is true. ex) 1, 10,32,47
    //  0 is considered False
    true;   //  1
    false;  //  0

    int truefalse = true;   //  storing 1
    truefalse = false;   //  storing 0

    // bool is a data_type for boolean  
    bool result;
    result = 1;     // true
    result = 257;   // true.
    printf("%d\n", result); // prints 1...

    result = !result;   // result now stores False
    int True = 100;
    True = !True;       //  True now stores 0

    result = result && True;    //  T && F = F
    result = result || True;    //  T || F = T

    //  ==, !=, <=, >=, <, >
    //  if right returns "true" else 'false'
    int a = 10, b = 10;
    if(a == b)
        a+=10;
    else
        b+=10; 

    //  Compiler Optimization will remove this code part 
    //  bc in no way this will run.(a == 20) Only in "Debug" mode will this run
    //  If we are using dynamic value then this would get stored.
    if(a == 30){
        if(++b > a)
            printf("b+1 is bigger");
        else
            printf("NO");       //  This gets prints out
    }

    //  ternary operator
    //  condition ? run when true : run when false
    (a == b+10)  ? printf("a, b+10 are both 20") : printf("smth's wrong");


    return 0;
}
```
 >  [Important TIP]    
   **Anything else than 0 is true.**   
   **Ternary Operator => [Condition] ? [Run when True] : [Run when False ]**  
   {: .prompt-tip }

<br>

### [ Operator - Bit]
> Its faster to just look at it.

```c
#include <stdio.h>
int main(int argc char** argv){
    unsigned char byte = 1;
    byte = byte << 1;              //  shift 1 bit to the left
    //  0000 0001 << 1 = 0000 0010
    printf("%d\n", byte);   //  prints 2
    byte <<= 1;              //  shift 1 bit to the left again
    printf("%d\n", byte);   //  prints 4

    byte >>= 2;             //  shift 2 bit to the right == divide by 2^2
                            //  remainder gets ignored anyway so no problem  
    printf("%d\n", byte);   //  prints 1

    //  (곱) &, (합) |, (반전) ~
    unsigned char b = 0, b1 = 2, b1 = 1;
    b = b1 & b2;    //  0000 0010 & 0000 0001 => 0000 0000
    b1 = b1 | b2;   //  0000 0010 & 0000 0001 => 0000 0011
    //  XOR ^   => 같으면 0, 다르면 1
    b = b1 ^ b2;    //  0000 0011 & 0000 0001 => 0000 0010

    return 0;
}
```
 >  [Important TIP]  
    **Shifting *n* to the left => 곱하기 2^n**   
    **Shifting *n* to the right => 나누기 2^n**     
 {: .prompt-tip }

<h4>Use case for Bit-Operator</h4>

 Using bit information, we can express status info for games ! Bit operations in this case are very helpful.

```c
#include <stdio.h>
#include <player.h> //  Temporary example
/*
#define HUNGRY 1
#define THIRSTY 2
#define TIRED 4
#define DEPRIVED 8
*/
//  Represented in 16 base bit
#define HUNGRY       0x001
#define THIRSTY      0x002
#define TIRED        0x004
#define DEPRIVED     0x008
#define HOT          0x010
#define COLD         0x020
#define type1        0x040
#define type2        0x080
#define type3        0x100
#define type4        0x200
#define type5        0x400

int main(int argc char** argv){
    ...
    //  current player.status is "HUNGRY"
    if(player.saturated() < 20)
        player.status |= THIRSTY;   //  0000 0000 0000 0011
    ...
    if(player.getStamina() < 10)
        player.status |= TIRED;     //  0000 0000 0000 0111
    
    // 0000 0000 0000 0111 & 0000 0000 0000 0010 = true
    if(player.status & THIRSTY)
        printf("You should drink some water\n");
    
    //  removing status
    //  XOR is not the answer -> if status 0000 0001 and you want to remove THIRSTY with XOR, you end up adding it instead...
    //  So we use [ AND + ~ OPERAND ]
    player.Action.drink();
    player.status &= ~player.status
    //  EX) removing [ DEPRIVED ]
    //  status      => 0000 0000 0000 1011
    //  ~DEPRIVED   => 1111 1111 1111 0111  -> 어차피 없던놈은 and로 날라감
    //              &)____________________  => 0000 0000 0000 0011
    ...
    return 0;
}
```
 >  [Important TIP]   
    **Adding Bit => status |= status**  
    **Removing Bit => status &= ~status**  
{: .prompt-tip }

 <br>

## End
Covered stuffs that i forgot over the years...

>   [Reference]   
    *80%* [아소트락 2021 C/C++ 강의](https://www.youtube.com/playlist?list=PL4SIC1d_ab-aOxWPucn31NHkQvNPHK1D1)  
    *10%* [모두의 코드](https://modoocode.com/138)  
    *10%* [The Cherno Youtube Channel](https://www.youtube.com/channel/UCQ-W1KE9EYfdxhL6S4twUNw)

