---
title: Windows 키 변경(Capslock-Ctrl)
author: mini
date: 2022-12-07 10:53:00 +0800
categories: [Etc]
tags: [WindowKeyMapping]
math: true
toc : true
---

 맥을 사용하면서 Ctrl키를 사용할 때가 많아 Ctrl과  Capslock을 바꿔서 사용해왔다. 맥북같은 경우에는 키보드 환경설정에서 보조키를 쉽게 변경할 수 있다. 하지만 일할때에는 윈도우를 사용하다보니 너무 불편했다. 그래서 결국 레지스트리를 통해 바꿔주었다.👍

## CapsLock - Ctrl 바꾸기

1.&nbsp;레지스트리 편집기 실행 ( window+r &nbsp; -> &nbsp; regedit 입력 )

2.&nbsp;HKEY LOCAL MACHINE/SYSTEM/CurrentControlSet/Control/Keyboard Layout 으로 이동

3.&nbsp;새로 만들기 &nbsp; -> &nbsp; 이진값(binary value) 생성

4.&nbsp;이진값 입력
> 00 00 00 00 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; => &nbsp; &nbsp;  Header
00 00 00 00 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; => &nbsp; &nbsp;  Version
00 03 00 00	&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; => &nbsp; &nbsp;  수정할 키 개수(+1)
1d 00 3a 00 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; => &nbsp; &nbsp;1d(CapsLock) 3a(Left Ctrl)
3a 00 1d 00 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; => &nbsp; &nbsp;CapsLock 안 쓸줄 알고 안했다가 뒤늦게 추가해줬다
00 00 00 00 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;=> &nbsp; &nbsp; 종료

5.&nbsp; 재부팅


<br/>
**완료**
 ![레지스트리화면](/assets/img/posts/key_setting.png)



