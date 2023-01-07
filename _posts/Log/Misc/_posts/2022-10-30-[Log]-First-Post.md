---
title: First Post
date: 2022-10-29 19:00:00 -500
categories: [Log, Misc]
tags: [ranting]
---

# Testing
## Testing

### Testing
#### Testing 

- code block

```c++
#include <iostream>
#include <string>

int main(int argc, char** argv){
    std::cout << "Hello fellow yoda" << std::endl;
    return 0;
}
```

# Log

log
=====

log
----

# Markdown Syntax


- 제목 밑에 ==== 하면 #, ---- 하면 ## 랑 같다
- "#" 부터 "######"는 html로 h 부터 h6까지를 표현한다
- *로 감싸거나 _ 로감싸면 _이탈릭체_ 
- 두껍게 강조는 위에 표기를 **두번**
- **_둘을 같이 사용 가능_**
- ~~취소선은 물결(~) 두번으로 감싸면 된다~~
- <u>밑줄은 __&lt;u&gt;__ 로 감싼다 </u>
- html태그 표시할땐 __"&lt"__ 이랑 __"&gt"__ 를 ; 붙혀서 쓰면 된다
- 수평선은 *를 연속 3번 혹은 5번, 아니면 -을 한칸씩 띄우면서 3번, 아니면 연달아서 많이 쓰면 된다
    > Sample Text
    > - - -
    > Sample Text
    > * * *
    > Sample Text

- > (>) * N 으로 블록강조 가능, 그안에 추가로 마크다운 요소 삽입가능
    
    > This is a first blockqute.
    >   > This is a second blockqute.
    >   >   > This is a third blockqute.  
    >   >   > - 추가사항은 같은 레벨의 > 로 표현한다
- 순서 목록은 숫자순으로
    > 1.
    > 2.
    > 3.
- 순서 없는 글머리
    > * 빨강
    >   * 녹색
    >     * 파랑
    > 
    > + 빨강
    >   + 녹색
    >     + 파랑
    > 
    > - 빨강
    >   - 녹색
    >     - 파랑
- 혼합 가능
    > * 1단계
    >   - 2단계
    >     + 3단계
    >       + 4단계
- 블록처리는 한줄+탭으로 한다
    > This is a normal paragraph
    > 
    >     This is a code block. 1 line spacing + Tab do the trick
    > end code block.
- 링크는 [링크키워드][id] 작성 후 한줄 띄고 [id]: 에 주소를 입력한다.
    > Link: [Google][googlelink]
    > 
    > [googlelink]: https://google.com "Go google"

- 이미지는  **![제목]"(이미지 경로)"**로 입력한다

    > 이미지 크기 조정이 필요한 경우 아래와 같이 한다   
    > &lt;img src="경로" width="W%" height="H%" title="제목" alt="표시글"&gt;&lt;/img&gt;

- 띄어쓰기 3번은 줄바꿈이다