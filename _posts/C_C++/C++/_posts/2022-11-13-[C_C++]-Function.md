---
title: "[C++]-Function"
date: 2022-11-13 15:42:00+0900
categories: [C_C++, C++]
tags: [Study, Basic]
math: true
---
# Basic C/C++
    지금까지 배운 C와 C++를 완전 바닥부터 다시 복습 + 공부하고 그걸 기록하기 위한 포스트입니다.

## Basics
 >Function == Command we write
  
- 함수는 부른 순서대로 실행된다. 이걸 *스택* 이라고 표현할 수 있다. FIFO(First In First Out)의 개념이다. 함수들이 호출되면서 사용하는 메모리 영역을 그래서 **스택영역** 이라고 한다.  

- 함수는 하나의 scope로 본다. 다른 함수끼리 똑같은 변수이름을 써도 오류로 인식하진 않는다.(근데 굳이 똑같게 하진 말자...)

- Function != Memory Space. 함수에서 썼다고 해서 그 결과가 전부 그대로 남아있는건 아니다. 이건 scope때문이기도 하고 애초에 명령이 실행되고 있을 때 다른 곳에서 돌다가 *return* 보고 결과 반환하는지라 결과 이외의 내용은 저장 안된다. (물론 포인터로 저장해서 사용하면 남길 수 있다) 

***예제***

```c
#include <stdio.h>

//	Return value of function is stored in cpu register when function is popped out of stack
// 
//	Factorial
unsigned long long factorial(int _step) {
	unsigned int res = 1;
	for (int j = 0; j < _step - 1; ++j) {
		res *= (j+2);
	}
	return res;
}

//	Function
int main(int argc, char** argv) {
	int input = 0;
	unsigned long long res = 0;
	while (1) {
		printf("Input step for factorial (-1 to exit): ");
		scanf_s("%d", &input);
		if (input == -1) break;
		res = factorial(input);
		printf("%d Factorial : %llu\n", input, res);
	}
	return 0;
}
```

## Recursive Function
> Function A calls itself, itself calls itself, ...

재귀함수가 자기자신을 다시 호출하며 함수스택에서 기존 함수 스택 위로 새로운 함수를 계속 쌓는다. 이걸 계속 반복하면 스택이 터지고 내 프로그램도 터진다(**StackOverFlow**). 그래서 사용에 있어서 무조건 탈출조건이 필요하다.  
터진다는 사실을 제외하면 제귀함수가 도움이 될때가 많다. 일단 동일 동작을 구현할때 좀 더 직관적이고 쉽다. 계층구조나 반복적인 동작같은 기능을 깔끔하게 처리가능하다. 물론 메모리를 갈가먹어서 성능이 좋지 않다.    

밑에 코드에서는 `RecFibonnachi`가 RecFibonnachi(N-1) + RecFibonnachi(N-2)를 계속 수행한다. 언젠간 if에 걸려서 나오게 되면 그때부터 스택에서 *return*을 계속 받아오면서 지금까지 부른 함수들의 결과를 합친다.

```c
#include <stdio.h>

//	Return value of function is stored in cpu register when function is popped out of stack
// 
//	Factorial
unsigned long long factorial(int _step) {
	unsigned int res = 1;
	for (int j = 0; j < _step - 1; ++j) {
		res *= (j+2);
	}
	return res;
}

//	Factorial Recursive
//	Easy to understand, but performance -> can use tail-recursion if needed
unsigned long long RecFibonnachi(int _step) {
	if (_step == 1 || _step == 2) {
		return 1;
	}

	unsigned long long res = RecFibonnachi(_step - 1) + RecFibonnachi(_step - 2);
	return res;
}


//	Function
int main(int argc, char** argv) {
	int input = 0;
	unsigned long long res = 0;
	while (1) {
		printf("Input step for factorial (-1 to exit): ");
		scanf_s("%d", &input);
		if (input == -1) break;
		res = factorial(input);
		printf("%d Factorial : %llu\n", input, res);    //  %llu for unsigned long long
	}

	printf("%llu", RecFibonnachi(5));

	return 0;
}

```
## Tail Recursion
재귀함수의 변형이다. 재귀함수를 그냥 쓰기에는 불필요한 과정을 너무 많이 실행한다. 각 단계별로 함수를 계속 **call** 하고, 종료조건에 도달하면 **return**을 또 모든 단계마다 실행한다. 위에서 사용한 피보나치의 경우  함수 호출 횟수는 입력 N일 경우
***(입력이 N-1인 경우와 N-2인 경우의 합) + 1*** 이다. N=6이면 25회, N=100인 경우 일단 단위가 *해* 부터 시작한다. 100이 입력이면 속도가 문제가 아니라 스택범위를 그냥 뚫어버려서 계산 도중에 진행이 안된다.  
만약 이전단게의 결과를 갖고가면 굳이 스택이 한바퀴 돌아서 결과를 리턴할 때 까지 기다릴 필요도 없지 않을까? 

```c
#include <stdio.h>

//	Factorial Recursive
//	Easy to understand, but performance -> can use tail-recursion if needed
unsigned long long TailFibonnachi(int _step, int prev, int NextPrev) {
	int tempResult = 0;
	if (_step < 2) {
		return _step * prev;
	}
	//	미리 (N-1) + (N-2)을 계산한다
	tempResult = prev + NextPrev;
	// 계산내용 업데이트
	NextPrev = prev;
	prev = tempResult;
	//	그결과를 그대로 가져간다.
	return RecFibonnachi(_step - 1, prev, NextPrev);
}

//	Function
int main(int argc, char** argv) {
	int input = 0;
	unsigned long long res = 0;

	printf("%llu", TailFibonnachi(100, 1, 0));

	return 0;
}

```

기존 방식인 *RecFibonnachi(_step - 1) + RecFibonnachi(_step - 2)*의 경우 앞에 값이 리턴되도 뒷부분을 리턴받아야지 진행된다. 굳이 이렇게 하지 말고 (N-1)+(N-2)가 마지막 단계가 되는 (0 + 1)에서부터 시작하고, 계산한 결과값을 함수파라미터로 들고 재귀를 돌다가 *_step*이 더이상 안남은 시점에서 리턴하면 바로 답이 나온다. 물론 리턴을 줄줄이 하겠지만 리턴 중간중간에 나머지 N-2값을 구하기 위해 함수 call을 계속하지 않으니깐 이득이 생기는 거다. 


## End
>   [Reference]   
    *80%* [아소트락 2021 C/C++ 강의](https://www.youtube.com/playlist?list=PL4SIC1d_ab-aOxWPucn31NHkQvNPHK1D1)  
    *10%* [모두의 코드](https://modoocode.com/138)  
    *10%* [The Cherno Youtube Channel](https://www.youtube.com/channel/UCQ-W1KE9EYfdxhL6S4twUNw)

