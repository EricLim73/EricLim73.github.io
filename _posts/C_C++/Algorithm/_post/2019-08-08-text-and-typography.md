---
title: Text and Typography
author: cotes
date: 2019-08-08 11:33:00 +0800
categories: [C/C++, Algorithm]
tags: [Testing]
math: true
mermaid: true
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

- TO-Do list 작성 가능
    > ### ToDo list
    > 
    > - [ ] Job
    >   + [x] Step 1
    >   + [x] Step 2
    >   + [ ] Step 3

- 설명 리스트는 제목란에 : 를 붙이고 밑에줄에 설명 쓰면 된다
    > Sun
    > : the star around which the earth orbits

- 알림 프롬트는 다음고 같이 만든다 tip, info, waring, dager 순으로 색갈이 달라진다.
    > > An example showing the `tip` type prompt.
    > {: .prompt-tip }
    > 
    > > An example showing the `info` type prompt.
    > {: .prompt-info }
    > 
    > > An example showing the `warning` type prompt.
    > {: .prompt-warning }
    > 
    > > An example showing the `danger` type prompt.
    > {: .prompt-danger }

- 테이블
    > | Company                      | Contact          | Country |
    > |:-----------------------------|:-----------------|--------:|
    > | Alfreds Futterkiste          | Maria Anders     | Germany |
    > | Island Trading               | Helen Bennett    | UK      |
    > | Magazzini Alimentari Riuniti | Giovanni Rovelli | Italy   |

- 주석은 [] 안에 ^fn-nth-번호로 작성한다.
    > Click the hook will locate the footnote[^footnote], and here is another footnote[^fn-nth-2].

- 이미지 위치선정은 왼쪽정렬(normal), 왼쪽모서리(.left), 오른쪽모서리(.right)가 있다
    > - Left aligned
    > 
    > ![Desktop View](/assets/img/baby-yoda.jpg){: width="972" height="589" .w-75 .normal}
    > 
    > - Float to left
    > 
    >   ![Desktop View](/assets/img/baby-yoda.jpg){: width="972" height="589" .w-50 .left}
    >   Praesent maximus aliquam sapien. Sed vel neque in dolor pulvinar auctor. Maecenas pharetra,     > sem sit amet interdum posuere, tellus lacus eleifend magna, ac lobortis felis ipsum id >  sapien. Proin ornare rutrum metus, ac convallis diam volutpat sit amet. Phasellus volutpat, >    elit sit amet tincidunt mollis, felis mi scelerisque mauris, ut facilisis leo magna accumsan >     sapien. In rutrum vehicula nisl eget tempor. Nullam maximus ullamcorper libero non maximus. >   Integer ultricies velit id convallis varius. Praesent eu nisl eu urna finibus ultrices id nec >   ex. Mauris ac mattis quam. Fusce aliquam est nec sapien bibendum, vitae malesuada ligula >    condimentum. Phasellus a tortor aliquam, tristique felis sit amet, elementum enim. Integer >   vestibulum vitae nulla nec pretium.
    > 
    > - Float to right
    > 
    >   ![Desktop View](/assets/img/baby-yoda.jpg){: width="972" height="589" .w-50 .right}
    >   Praesent maximus aliquam sapien. Sed vel neque in dolor pulvinar auctor. Maecenas pharetra,     > sem sit amet interdum posuere, tellus lacus eleifend magna, ac lobortis felis ipsum id >  sapien. Proin ornare rutrum metus, ac convallis diam volutpat sit amet. Phasellus volutpat, >    elit sit amet tincidunt mollis, felis mi scelerisque mauris, ut facilisis leo magna accumsan >     sapien. In rutrum vehicula nisl eget tempor. Nullam maximus ullamcorper libero non maximus. >   Integer ultricies velit id convallis varius. Praesent eu nisl eu urna finibus ultrices id nec >   ex. Mauris ac mattis quam. Fusce aliquam est nec sapien bibendum, vitae malesuada ligula >    condimentum. Phasellus a tortor aliquam, tristique felis sit amet, elementum enim. Integer >   vestibulum vitae nulla nec pretiu

- mermaid를 통해 도표작성도 가능하다
    > ## Mermaid SVG
    > 
    > ```mermaid
    >  gantt
    >   title  Adding GANTT diagram functionality to mermaid
    >   apple :a, 2017-07-20, 1w
    >   banana :crit, b, 2017-07-23, 1d
    >   cherry :active, c, after b a, 1d
    > ```

- 수식 표현의 경우 math를 추가 해줘야된다.
    > The mathematics powered by [**MathJax**](https://www.mathjax.org/):
    > 
    > $$ \sum_{n=1}^\infty 1/n^2 = \frac{\pi^2}{6} $$
    > 
    > When $a \ne 0$, there are two solutions to $ax^2 + bx + c = 0$ and they are
    > 
    > $$ x = {-b \pm \sqrt{b^2-4ac} \over 2a} $$

- 짧은 코드표현은 작은 따음표로 감싸 작성한다.
    > This is an example of `Inline Code`.

- 코드 블록에 특정 파일경로를 통한 임포트나 구문을 표현하고 싶은 경우 코드블록 이후에 해당 파일의 경로를 {: file='경로'}로 명시해주면 된다
    > ### Specific filename
    > 
    > ```sass
    > @import
    >   "colors/light-typography",
    >   "colors/dark-typography"
    > ```
    > {: file='_sass/jekyll-theme-chirpy.scss'}

- 현재 작성한 문서 안에서의 주석의 링크는 주석[] 태그에 : 을 통해 설명을 적으면 된다.

    > [^footnote]: The footnote source
    > [^fn-nth-2]: The 2nd footnote source

