---
title: ubuntu 설치하기
author: mini
date: 2021-05-30 11:10:00 +0800
categories: [OS, Linux]
tags: [linux]
toc : true
---


 오래된 노트북이 있는데 window8이라 어떻게 처리할지 고민하다가 리눅스로 바꿔서 사용하기로했다. 오래된 똥컴이긴하지만 window8만 아니라면 괜찮을것 같다. 그래서 우분투를 설치했던 방법을 간단하게 정리한다.

----------------------------------

### 1. Ubuntu 설치 USB 만들기
1) Rufus
2) ubuntu iso 파일 다운로드

### 2 USB 디스크로 부팅설정
 ➕ 1에서 만든 USB를 연결한 후   
1) Bios로 진입  
    컴퓨터가 켜질때FN + F12를 연타해준다. (LG노트북)  
2) Boot Menu    
 Bios로 들어갔다면 Boot Menu로 들어간다.  
3) Edit Boot Order 수정    
	Edit Boot Order로 들어가서 보면 Windows Boot Manager가 가장 상단에 있는 것을 볼 수 있다. 이 순서를 수정해주면 된다. USB HDD를 첫번째로 이동시킨다.


