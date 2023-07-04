---
title: Neovim - 파이썬 자동실행 단축키 만들기(input 가능하게) 
author: mini
date: 2022-05-30 11:10:00 +0800
categories: [-,Neovim]
tags: [nvim]
toc : true
---

알고리즘을 풀때 빠르게 값을 확인하는게 편한데 nvim을 쓰다보면 불편하다. 그래서 다른 IDE처럼 실행 키를 만들어 하단에 터미널이 떠서 실행이 되게 만들었다.   

## 방법1 

```
autocmd FileType python map <buffer> <F9> :w<CR> <c-z>python3 `ls -tr\|tail -1`<CR>
autocmd FileType python imap <buffer> <F9> :w<CR> <c-z>python3 `ls -tr\|tail -1`<CR>
```

※ 참고자료) [Running python code in Vim](https://stackoverflow.com/questions/18948491/running-python-code-in-vim){: width="350"}   
대부분의 코드 설명은 위 참고자료에 있다. 
없는 부분만 추가!


※ &#60;c-z> 단축키는 nvim 설정에서 nvim 에디터 아래에 작게 터미널을 열도록 설정한 단축키이다. 단축키를 실행하면 다른 IDE처럼 터미널이 열린다.   


##### ※ map vs imap 
map = normal, visual mode에서의 key map    
imap = insert mode에서의 keymap   

 ※ <c-z> 단축키는 내 nvim 설정에서 nvim 에디터 안에 작게 터미널을 여는 단축키이다. 단축키를 실행하면 다른 IDE처럼 터미널이 열린다.

```
Python3 `ls -tr\|tail -1`
``` 
ls -t　　　　　= 날짜순으로 파일을 보여준다.(최근 파일이 가장 위로)  
ls -tr　　　　&nbsp;= 역순으로 됨   
|(파이프라인)　=  결과를 다음 명령어에 넘겨줌  
tail -1　　　　&nbsp;= 끝에서 마지막행  
``(백틱)　　　= 안에 명령어를 실행한 후 결과값 출력  





##### 🛑  &#92;|   
처음에 Python3 `ls -tr|tail -1` 로 썼었다.
그런데 nvim 으로 파일을 열면 다음과 같은 문구가 나왔다.
![E492](/assets/img/posts/E492.png)


이것때문에 한참을 해맸는데!!! 알고보니 &#124;(파이프라인)이 다른 의미로 인식되는 것 같았다. 그래서 **&#92;**를 써서 &#124;을 그대로 인식하도록 해주면 된다.


##### 🛑  주의 사항  
이와같이 설정하고 단축키를 사용할 때, 파일 위치에 가서 nvim으로 켜야한다. 꽤 번거로울 수있다. ls 때문에 어쩔 수 없었다...😫

## 방법2
위 코드 중 **:w&#60;CR>** 뒤에 **:term python3 %&#60;CR>**로 고쳐주면 된다.  
방법1과 같은 주의사항은 없다.  
