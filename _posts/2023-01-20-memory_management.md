---
title: 운영체제 기본 개념정리 - 메모리(주기억장치) 관리
author: mini
date: 2023-01-20 11:10:00 +0800
categories: [OS]
tags: [os]
toc : true
---

#### ※ Background  
---------------
### 메모리 종류
![memory](/assets/img/posts/memory_type.jpeg){: width="40%"}{: .left}  
<br/><br/><br/><br/><br/><br/>
### 메모리 계층 구조 
![memory_hierarchy](/assets/img/posts/memory_hierarchy.jpeg){: width="80%"}{: .left}
<br/><br/><br/><br/><br/><br/>
### Address binding
프로그램의 논리주소를 실제 메모리의 물리주소에 매핑하는 작업  
![address_binding](/assets/img/posts/address_binding.jpeg){: width="80%"}{: .left}
<br/><br/><br/><br/><br/><br/>
### Dynamic Loading
모든 루틴(ex. function)을 교체 가능한 형태로 디스크에 저장   
메인 프로그램만 메모리에 적재하여 수행  
루틴의 호출 시점에 address binding 수행  
장점) 메모리 공간의 효율적 사용  

### Swapping
프로세서 할당이 끝나고 수행이 완료된 프로세스는 **swap device**로 보내고(**swap-out**) 새롭게 시작하는 프로세스는 메모리에 적재(**swap-in**)

<br/><br/>
### < Memory Allocation > 
--------------------
### 1. Continuous Memory Allocation(연속할당)
#### &nbsp;&nbsp; 1) Uin-Programming  
#### &nbsp;&nbsp; 2) Multi-programming  
 - Fixed Partition Multiprogramming(FPM)  
 - Variable partition Multiprogramming(VPM)  


### 2. Non-continuous Allocation / Virtual memory
