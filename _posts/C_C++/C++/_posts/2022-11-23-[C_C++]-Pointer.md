---
title: "[C++]-Pointer"
date: 2022-11-23 10:12:00+0900
categories: [C_C++, C++]
tags: [Study, Basic]
math: true
---

# Basic C/C++
    지금까지 배운 C와 C++를 완전 바닥부터 다시 복습 + 공부하고 그걸 기록하기 위한 포스트입니다.  

## Pointer
> Pointer saves address

```c
int main(){
	
	int a = 10;
	int* iPtr = nullptr;    //  nullptr meaning its pointing to nothing 
    iPtr = &a;

	printf("Value in a: %d\n", a);
	printf("Address of a: %p\n", &a);

	printf("Value p is storing(=a): %d\n", *iPtr);
	printf("Value in p: %p\n", iPtr);
	printf("Address of p: %p\n", &iPtr);

    printf("Value of a from &a: %d\n", *(&a));
    printf("Size of pointer p: %d\n", sizeof(p));

}

```
    Value in a: 10
    Address of a: 000000E13E0FF864  

    Value p is storing(=a): 10
    Value in p: 000000E13E0FF864
    Address of p: 000000E13E0FF888
    Value of a from &a: 10
    Size of pointer p: 8

Every variable gets saved inside memory. Example above shaows what *a* have & where its stored. ***Pointer*** stores an address of given data. `dataType *` is used to declare a pointer of given type. Pointer variable stores the address, and if you want to access through the address inside you use `*` with the pointer variable. `*` operator can access value from given address, so `printf("Value of a from &a: %d\n", *(&a));` is valid and prints out *10* as result. `&` operator returns address of given target. The size of a pointer is determined by its running OS platform. Normally every computers nowaday runs in x64bit. Pointer stores memory, and memory address for x64bit uses 8 byte which is exactly the size for pointer.

Through pointer, you can access to its stored address and do what ever you want. 

```c
int a = 10;
int* iPtr = &a;
(*iPtr) = 20;
printf("%d\n", a);
```

`(*iPtr)` can be translated to `*(&a)` which is basiically just `a`. `(*iPtr) = 20;` stores the integer data *20*. What if we do `(*iPtr) = 100` when `(*iPtr)` is storing address from different dataType like `char` or `float`?  
A dataType that pointer is labeled does not indicate the type pointer stores(though it follows the type it stores for most cases). DataType for pointer is just a rule for pointer to use when accessing its stored address.  

For example, 

```c
int* iPtr = nullptr;
char num = 'c';
iPtr = &num;
``` 
What if we do `*iPtr = 100` because `iPtr` is an integer pointer? `iPtr = &num;` will make iPtr point a *char type variable*. Inserting a `100` which is a 4 byte integer data, 3 bytes of data will go right pass what `iPtr` is allowed to look. What if it was `*iPtr = 12.34f`? Event tough the byte size is the same, reading num after this line would return something totally different(Remember that *float* and *int* follows different rules when reading bit values). Good thing is that these kind of insertion are detected by the compiler(if not the IDE your using will likely do it). Bypassing that layer of protection is possible through type-casting, so be aware of what and where you are using casting on to prevent issues.  

>   **TLDR**   
>   Pointer is just variable that stores address. Datatype of said pointer tells how you are going to read value from that address.   
{: .prompt-info }

<br/>

```c
char* cPtr = nullptr;
short* sPtr = nullptr;
int* iPtr = nullptr;
```

 Address is stored as integer(so no floating points), and generally 1 memory
space is set as 1 byte. Then what is the output of `sizeof(cPtr)`, `sizeof(sPtr)`and `sizeof(iPtr)`? The answer is **It depends on what OS(configuration) the program is running**. If its x64bit environment, its going to be **8 bytes**, if its x86(which is 32bit), then its **4bytes**.   

If we consider pointer as integer value variable, what are the result when we perform basic math on it? Lets say we do `iPtr+1`. Given `iPtr` saves given address and interprets with its dataType. Adding **1** to it means we are going to step through **4byte** of memory. Why 4byte? Its because `iPtr` is an `int` type. This applies to other pointer variables above. `sPtr` adds **2byte**, `cPtr` adds **1byte**. Performing `+1` to a pointer increments to the next address stepping `sizeof(ptr dataType)` inside memory.

## Array part2

> Array => continuous memory storing values + Array_name == Starting Address

<br/>

```c
// Same as int(&iArr)[10] = iArr;
// Array types are defined as type(&arr_name)[size] = arr_name;
int iArr[10] = {};  
iArr[2] = 2;

*(iArr + 1) = 10;  // 배열 시작 주소 + sizeof(int)만큼 점프 후 접근 => iArr[1]
*(iArr) = 10;   // iArr[0]에 10 삽입


```
Code above shows a normal array. With the new knowledge of pointers, we can properly see how `Array` works under the hood. `Array` is just one big continuous memory block of given dataType. Name of said `Array` is considered as the starting point address. Pointer stores address, so we can easily deduce that by adding the index number to its name returns its corresponding memory location. Using `*` operator we can then access through that location and do various tasks. 


## Pointer Exercise

```c
#include <stdio.h>
//	type (byte)
// char(1) short(2) int(4)

int main(int argc, char** argv) {
	// Q1
	short sArr[10] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
	int* pI = (int*)sArr;	//	sArr is considered starting ADDRESS of an array
							//	So we type cast it with (int*) not (int) to save it inside "pI"
	
	int iData = *((short*)(pI + 2));
	// [int] : 12, 34, 56 => +0 +1 +2
	//	=> (short*)로 (pI+2)를 참조하면 "56" 에서 2바이트만 본다 => "5"의 주소만 본다
	//		=> 그 주소를 바탕으로 * 를 써서 값을 받아와 iData에 넣는다.
	
	// A1 => prints 5
	printf("iData = %d\n", iData);

```
First question. most of the explaination is written within the comments. We simply just lookup the array address using different type (= byte size) and print them.

```c
    // Q2
	char cArr[2] = {1, 1};		// [0] 0000 0001 [1] 0000 0001
	short* pS =	(short*)cArr;	//	[0][1]을 한번에 읽는다

	iData = *pS;	//	iData = 0000 0001 0000 0001 = 257
	
	//A2 - 257
	printf("iData = %d\n", iData);
```
Second question. Same logic use for the first one. This question shows how bit information can be interpreted with different type casting.

```c
	// Q3
	char cArr2[2] = { 1, 2 };		// [0] 0000 0001 [1] 0000 0010
	short* pS2 = (short*)cArr2;	//	[0][1]을 한번에 읽는다

	int iData2 = *pS2;	//	iData = [1][0] = 0000 0010 0000 0001 = 513

	//A2 - 513
	printf("iData2 = %d\n", iData2);
```
Third question. This is quite tricky. To understand why the result is not *258*, you should understand the concept of ***Little-Endian*** and ***Big-Endian***. *Little-Endian* read bits from **left to right**, *Big-Endian* read bits **right to left**. Due to how computers store and read bits using these *"Endian"* style method. `iData` actually gets ***[1][0]*** from `pS2`. Thats why we get `513`, so in order to print `258` we need cArr2[2] to be `{2, 1}`.

>   **TLDR**   
>   This happens because we are trying to read a 1byte data with 2byte type. This messes up the ordering of the original 1byte data. This is why you probably would like to match pointer type with its corresponding target variable type.   
{: .prompt-info }

## Pointer & Function Scope
```c
#include <stdio.h>
void Test(int a){
    a = 500;
}
int main(int argc, char** argv){
    int a = 0;
    Test(a);
    printf("a = %d\n", a); 
    return 0;
}
```
The code above prints `a = 0`. The `a` from **Test()** is located in a different memory space from **main()**'s `a`. What if we actually want to change `a` form **main()** after calling **Test()**? We use pointers.  **Test()** will take an integer pointer as its parameter, and inside **main()** we would give `&a` (=address) when calling **Test()**.

```c
#include <stdio.h>
void Test(int* a){
    a = 500;
}
int main(int argc, char** argv){
    int a = 0;
    Test(&a);
    printf("a = %d\n", a); 
    return 0;
}
```
This is not new to us. `scanf()` requires `&variable` to handle input. Thats because `scanf()` also takes a pointer parameter is its input as well.

## End
>   [Reference]   
    *80%* [아소트락 2021 C/C++ 강의](https://www.youtube.com/playlist?list=PL4SIC1d_ab-aOxWPucn31NHkQvNPHK1D1)  
    *10%* [모두의 코드](https://modoocode.com/138)  
    *10%* [The Cherno Youtube Channel](https://www.youtube.com/channel/UCQ-W1KE9EYfdxhL6S4twUNw)
