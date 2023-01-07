---
title: "[C++]-Const & Void"
date: 2022-11-28 12:12:00+0900
categories: [C_C++, C++]
tags: [Study, Basic]
math: true
---

# Basic C/C++
    지금까지 배운 C와 C++를 완전 바닥부터 다시 복습 + 공부하고 그걸 기록하기 위한 포스트입니다.  

## Const

> Const == 상수

Any variable with `const` is considered ***`rvalue`***, aka constant.

```c
const int num = 100;
num = 10; ==> (X) bc this is interpreted as 100 = 10;
```
The keyword `rvalue` is used for values that are written on the rightside of given variable declaration. For `int num = 100`, **100** is considered as `rvalue`. **num** is refered as `lvalue` because its written on the leftside. 

>  **l-value** => 변수
   **r-value** => 상수  
{: .prompt-info }

</br>

## Const == Unchangable ?

If we think about it, `const` variable is still *variable*. Using `const` is just a grammer protecting labeled variable. This however does not imply that `const int num = 100` is exactly identical as `100`. What this means is that even though `num` is considered `const`, its still a **varaible**, which means that somewhere inside the memory there is a space for this variable. With this fact in mind, what we can do is access that memory space with pointer variable and change the value from pointer, which has nothing to do with `const`.


```c

    volatile const int num = 100;
    printf("const num = %d", num);  // prints 100

    int* iPtr = &num;
    *iPtr = 10;
    printf("const num = %d", num);  // prints 10

```
So using pointer can remove `const` from said variable. This is not good practice; your ripping off what might have been a intended protection from an important variable.

>  ***`volatile`*** is used to stop register optimization. Accessing variable with this keyword on it will force the program to actually look for that memory address.   
{: .prompt-info }


## Const Pointer

```c
    const int num = 100;
    int* iPtr = &num;
    *iPtr = 10;

    int cnum = 1, numc = 2;
    const int* c_iPtr = &cnum;  // (A)
    int* const iPtr_c = &numc;  // (B)

    *c_iPtr = 200;      //  X
    c_iPtr = &numc;     //  O

    *iPtr_c = 300;      //  O
    iPtr_c = &cnum;     //  X
```
Using `const` with `pointer` can be confusing. `const` for pointer can either (A): can't change data its pointing, or (B): can't change what its pointing at. `c_iPtr` from (A) can change where its pointing to but can not alter its destination's data. `iPtr_c` form (B) works vice versa. 

```c
int const* ptr = &num;
```
During your studies you may find this way of writing const pointers. While it is not a standard way of doing things, we can see that the `const` keyword is positioned before `*`. So this is exactly the same situation as (A) from the code prior to this one. 

## Why Const Pointer
One example would be function parameter. 
```c
void Output(const int* param){
    ...do something...
}

int main(int argc, char** argv){
    int a = 100;
    Output(&a);
    return 0;
}
```
We often use *pointer* for function inputs for (1)using address instead of needless copying, (2)to use the original variable and many more reasons. What if the function changes the variable that you made b accessing through pointer. The solution is to set function parameter as `const`. This sets the function parameter at grammer-level to not change the content where its pointing at. When using the function, `ctrl + shift + space` at the function shows how the function parameters are declared so that you can check if this function change its parameters or not.  

>  `const` function pointer **can** get altered using another pointer. Whoever those that can go hell and you should not work with anyone doing that.  
{: .prompt-info }

<br/>

## Void

> Void == No Type

Literaly means *no type*. Functions with `void` tpye don't need have to return anything.  
`void pointer` shares the same idea. Its a pointer with no specification on how to read its pointer memory address. Due to this fact, `void pointer` can point to **ANY** memory address. However it can not read (or access) the pointer and can not do numeric operations like +1 to traverse to the next address.

```c
void* vPtr = nullptr;
int inum = 10;
float fnum = 10; 
double dnum = 10; 
long long lnum = 10; 

vPtr = &inum;
vPtr = &fnum;
vPtr = &dnum;
vPtr = &lnum;

*vPtr = 100;        //  (X)  
vPtr = (vPtr + 1)   //  (X)

*((int*)vPtr) = 200;    // (O)
//  line above is ok
//  1. First we typeCast "void*" into "int*". So now we're lookin at vPtr as "int" pointer
//  2. Access vPtr (which is int* now) using "*" and change its data to "200"
```

>   ***TLDR***  
> Void *  
>   1) Not Type specified   
>   2) Can store any type of variable
>   3) Can't access through `*`
>   4) Can't calculate address using numeric operation




## End
>   [Reference]   
    *80%* [아소트락 2021 C/C++ 강의](https://www.youtube.com/playlist?list=PL4SIC1d_ab-aOxWPucn31NHkQvNPHK1D1)  
    *10%* [모두의 코드](https://modoocode.com/138)  
    *10%* [The Cherno Youtube Channel](https://www.youtube.com/channel/UCQ-W1KE9EYfdxhL6S4twUNw)
