---
title: "[C++]-Array-&-Struct"
date: 2022-11-12 11:32:00+0900
categories: [C_C++, C++]
tags: [Study, Basic]
math: true
---

# Basic C/C++
    지금까지 배운 C와 C++를 완전 바닥부터 다시 복습 + 공부하고 그걸 기록하기 위한 포스트입니다.

## Array

간단하게 문법적인 부분만 봅시다.

```c
#include <stdio.h>
int main(int argc, char** argv){
    int iArr[10] = {1,2,3}; //  나머지는 전부 0으로 초기화
    int dummy = 0;
    // 0 ~ 9 index 생성
    for(int i=0; i<=9;++i){
        printf("%d\t", i);
    }
    iArr[10] = 10;  //  WARNING !! -> This will definetly go somewhere else. Most of the time variable "dummy" would get altered

    return 0;
}
```
> 배열은 연속적인 메모리구조를 갖는다. 인덱스를 최대 인덱스 이상으로 접근하면 오류라고 잡지 않고 원래 접근할 필요 없는 메모리 영역에 접근해서 문제 생기는 경우가 은근 많다.  
{: .prompt-warning }


## Struct (C-style)
> User defined data_type 

```c
#include <stdio.h>

typedef struct _tagMyStruct{
    int a;      //  4 bytes
    float f;    //  4 bytes
}MYST;
//  adding keyword "MYST" to represent usecase inside C

int main(){
    MYST t;
    MYST t1 = {13, 3.14f};  // initialization

    printf("%d\n", sizeof(MYST));   //  prints out 8

    return 0;
}
```

`typedef` is used to *define a given type*. `typdef int i4;` will make **i4** an `int` type. C 스타일로 만들면 C & C++ 둘다 사용해도 문제 없어서 저런 형태로 선언하는 경우가 많다.


> 세부적인 내용은 포인터를 정리할 때 봅시다.  
{: .prompt-info }

## End

>   [Reference]   
    *80%* [아소트락 2021 C/C++ 강의](https://www.youtube.com/playlist?list=PL4SIC1d_ab-aOxWPucn31NHkQvNPHK1D1)  
    *10%* [모두의 코드](https://modoocode.com/138)  
    *10%* [The Cherno Youtube Channel](https://www.youtube.com/channel/UCQ-W1KE9EYfdxhL6S4twUNw)

