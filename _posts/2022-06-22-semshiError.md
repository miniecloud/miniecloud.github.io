---
title: neovim - shemshi enable error
author: mini
date: 2022-06-22 11:10:00 +0800
categories: [OS, Linux]
tags: [nvim]
---

주로 python을 사용하다보니 semantic highligting 기능을 제공하는 Semshi 플러그인을 설치해봤다.
그런데 자꾸 'function <SNR>63_filetype_changed 수행중 에러 발견: 4 줄: E492: 편집기 명령이 아닙니다: Semshi enable' 이런 에러가 나왔다.  
Semshi README에는 `:UpdateRemotePlugins`를 실행하면 된다고 했지만 이와같은 방법으로는 해결이 안됐다.   

🧐 파이썬 경로 설정을 해주면된다.  
```
let g:python3_host_prog = substitute(system("which python3"), '\n\+$', '', '')
```
※ g:python3_host_prog : neovim에 대한 특정 인터프리터를 설정


