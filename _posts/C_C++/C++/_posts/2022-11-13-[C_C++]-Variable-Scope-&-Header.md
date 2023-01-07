---
title: "[C++]-Variable-Scope-&-Header"
date: 2022-11-13 16:32:00+0900
categories: [C_C++, C++]
tags: [Study, Basic]
math: true
---

# Basic C/C++
    지금까지 배운 C와 C++를 완전 바닥부터 다시 복습 + 공부하고 그걸 기록하기 위한 포스트입니다.


## 종류 & 메모리 영역

| Variable 종류 | 사용영역                 
|:--------------|:-------------------------
| Local Variable |   (Stack 영역)
| Global Variable|   (Data 영역)
| Static Variable|   (Data 영역)
| extern Variable|   (Data 영역)

|  메모리 영역   
|:--------------
|  Stack       
|  Data         
|  ReadOnly (ROM)
|  Heap          


## 전역변수 ==> Data 영역
프로그램이 시작하면 생성되고 프로그램 종료 시 지워진다.

```c
#include <stdio.h>

//  global variable
int g_num = 0;

int Test(){
    ++g_num;
}


int main(int argc, char** argv){
    int a = 10;
    Test();
    Test();
    Test();    
    return 0;
}

```

## Header Files
Before we go deep into static & extern vairable, we will take a look at what header files are and how to use them.  

`#include "target"` is just a preprocessor that copies(this happens before compile time) the target inside destination. We typically seperate implementation and declaration. Declaration written inside the header file, implementation written inside header files's cpp counterpart.

#### func.h
```c
int Test_h(int num){}

```
#### func.ccp
```c
int Test_h(int num){
    global_num = 1;
    return num + 1;
}

```
#### main.ccp
```c
#include <stdio.h>
#include "func.h"

int Test();
int global_num=0;

int main(int argc, char** argv){
    Test();
    Test();    
    Test();    
    //
    printf("from header func:%d\n", Test_h(global_num));
    
    return 0;
}

//  int Test(){++global_num;} 
//  -> If this function that was declared above is not defined,
//  it returns a linking error

```
`func.h` only tells us(and the compiler) that we have a function called `Test_h`. The actual implementation is done inside `func.c`. `func.c` also only know the functions existence from `#include "func.h"`  
Now we want to use that function inside `main.c`. We will then have to include `func.h` into `main.c` just like `func.c`. When we call `*Test_h()*` from `main.c` **main** check `func.h` to see if we have that function. `main.c` does not know how its implemented. Its the `linker`'s job to link the function implemenation.  

Why do we do this. Header files are used to manage and organize your code base. Techincally using tons of header files connecting to each other hits performance(not much.. but still), human just can't manage one giant massive main.cpp file.   


### Things to keep in mind
Why can't we just put both the implementation **and** declaration inside the header file?. We need to keep in mind that `#include` just copies the content inside. During the linking stage, linker will notice that there are 2 copies of the same content(one inside header and one inside some file that `#include`ed the header ).  

Using header files brings up new problems. ***Global Variable can't be detected inside the header file***. For example, the code given above, while compiling `func.c` the compiler will have no clue what `global_num` is if it was used inside. When its running the linking stage everything comes together but comile happens before that and compiler will definitely see it as an error.  

How do we solve this? Naive idea would be putting the *global variable* inside the header. **HOWEVER**, if you think about what `#include` does, if multiple source includes that header, the same variable will get copied that amount of times. That means inside the **Data memory space** we have N amount of the same global variable.

`static` **&** `extern` is used *(extern solves it)* to solve our *global variable among multiple file including the header* problem.


## Static Variable
`static` varaibles are stored inside **`Data Memory Section`**. What `static` so different from `Global`? Static is actually a *restricted* version of global(with some extra traits). Static can only be accessed from the scope where its declared. If you declare a *static* variable inside a function , header file, or any translation, that variable can only be accessed from that spot alone.  
(class is little bit different but shares the same idea; only access from that classInstance(or name))

staticFunc.h
```c
#include <stdio.h>
void staticFunc(){
    static int cnt = 0;
    cnt++;
    printf("%d\n", cnt);
}
```
```c
#include <staticFunc.h>
int main(){
    staticFunc();
    staticFunc();
    //  cnt--; ==> Error: Can't do this
    return 0;
}
```
This approach hides the *cnt* variable form others so no other function(translation) can change it. You might wonder what happens to *cnt* when its called twice. Are we declaring cnt = 0 twice and reseting it everytime? No, static variable assignment only gets runned once and is ignored after that. This can be proved when looking at its assembly code generated. 

func.h
```c
#pragma once

#include <stdio.h>
int Add(int a, int b);
int Sub(int a, int b);
int Mult(int a, int b);
```
func.cpp
```c
#include "func.h"

static int g_iStatic = 0;
//	데이터 영역에 상주하며 선언된 scope에서 접근 가능하다는 전제 아래에 움직인다.
//	함수의 시작/끝과 관계없이 프로그램시작하면 언제나 상주하며, 함수 안에서만 쓴다
//		=> 그럼 하는 짓은 전역변수랑 다른게 있나? 사용범위가 제한적인것을 제외하면 다른게 없긴 하다. 오히려 제한을 건 맞음
//	만약 전역변수로 특정함수의 실행횟수를 계산하면 다른 함수에서 그 전역변수 건드는 순간 ㅈ 된다 보면 된다.
//	정적변수변수로 하면 함수가 그걸 리턴한걸 로컬변수로 받으면 원본은 안전하잖음.
//	근데 예를 들어 함수 안에서 
//	...
//	static int func_call_cnt = 0;
//	func_call_cnt+=1;
//	...
//	라고 하고 이 함수를 10번 돌려도 0이 아니라 10이 나옴. 정적변수 선언문은 함수 호촐 처음했을때 1번 실행되고 다음은 실행X
//	이건 어셈블리단에서 확인해도 똑같음. 이건 정적변수의 특징

int Add(int a, int b) {
	printf("%d\n", g_iStatic);
	return a + b;
}

int Sub(int a, int b) {
	return a - b;
}

int Mult(int a, int b) {
	return a * b;
}
```
main.cpp
```cpp
#include "func.h"

static int g_iStatic = 0;

int main() {
	g_iStatic = 10;
	printf("%d\n", g_iStatic);
	g_iStatic = Add(1,2);
	printf("%d\n", g_iStatic);
	g_iStatic = Add(1, 2);


	return 0;
}
```
Notice that both *main.cpp* and *func.cpp* has ***g_iStatic*** variable. Will it return an error? NO it doesn't. Both are inside the deta-memory section, but they are declared from different translation so we see them as different variables. This is not actua..y what we were looking for. We want a ultimate global variable that can be accessed from all translation that includes it, without error.

 >  [TIP]
    Declaring static inside one header file and multiple other cpp files including that does **NOT** solve the problem. *#include* is just copying whats inside, so execution above would just copy the ***static int whatever;*** to every cpp including it and make multiple static variable from different translation... Thats not what we want to do.
{: .prompt-tip }

![Desktop View](assets\img\2022-11-13-[C_C++]-Variable-Scope-&-Header_img\2022-11-13-[C_C++]-Variable-Scope-&-Header_img01.png){: width="972" height="589" }

 >  [WARNING]
    There is a bug inside Visual Studio intellisense that shows ***g_iStatic*** inside func.cpp has the same value as main.cpp. This is not right and you can see it by printing it out or looking at the memory space that it indeed has *0* inside. 
{: .prompt-warning }


## Extern Varialble
keyword `extern` is not for declaring a variable. Using it implies that  somewhere around the project(or solution) there exists a variable named X. If it doesn't exist, it will return an error crying that it can't find the *extern* variable.  
Using `extern` variable will allow all translation that uses it access target variable without copy & error issues. This is exactly what we want to do(One global variable for all)!  

common.h
```c
#pragma once
//  extern int g_iExtern = 0;  -> this is just worng usecase of "extern"
extern int g_iExtern;
extern int g_iExternFromMain;

```
data.cpp
```c
int g_iExtern = 10;
```

func.h
```c
#pragma once
int PrintExtern();
```
func.cpp
```c
#include "func.h"
#include "common.h"
int PrintExtern(){
    printf("From func g_iExtern: %d\n", g_iExtern);
    printf("From func g_iExternFromMain: %d\n", g_iExternFromMain);
}
```

main.cpp
```c
#include "common.h"
#include "func.h"

//  writing this inside main will give unresolved error.
//  bc func.cpp uses this and if its inside main() scope PrintExtern() inside 
//  func.cpp can't find it
int g_iExternFromMain = 10; 

int main(){
    PrintExtern();
    g_iExtern = 500;
    printf("From Main g_iExtern: %d\n", g_iExtern);
    printf("From Main g_iExtern: %d\n", g_iExternFromMain);
	g_iExternFromMain = 20;
    PrintExtern();
    
    return 0;
}
```

The source variable of an `extern` can exist all around the code. Just make sure that they are **actually** there and that the scope source variable is declared in is reachable from the using side as well. 


## End
>   [Reference]   
    *80%* [아소트락 2021 C/C++ 강의](https://www.youtube.com/playlist?list=PL4SIC1d_ab-aOxWPucn31NHkQvNPHK1D1)  
    *10%* [모두의 코드](https://modoocode.com/138)  
    *10%* [The Cherno Youtube Channel](https://www.youtube.com/channel/UCQ-W1KE9EYfdxhL6S4twUNw)
