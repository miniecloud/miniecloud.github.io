---
title: 운영체제 기본 개념정리 - 프로세스 동기화 & 상호배제
author: mini
date: 2023-01-10 11:10:00 +0800
categories: [OS]
tags: [os]
toc : true
---

 병행 수행중인 비동기적 프로세스들이 공유자원에 접근할 때 __Race condition__ 문제가 발생할 수 있어 이를 막기위해 __동기화(Synchronize)__ 해야함

## 기본 개념
### Race Condition 
 여러 프로세스들이 동시에 데이터에 접근하여 실행 시간에 따라 결과가 달라짐

### Critical Section(임계영역)
 공유 데이터를 접근하는 코드 영역(Code segment)  
※ 기계어 명령은 Atomicity(원자성), Indivisible(분리불가능)의 특성상 실행도중 인터럽트를 받지 않음

<br/>
## Mutual exclusion(상호배제)
둘 이상의 프로세스가 동시에 critical section에 진입하는 것을 막는 것
### 기본연산
enterCS() : Critical section 진입전 검사(안에 있는지 확인)  
exitCS() : Critical section을 벗어날 때 시스템에 알림  
### 기본연산 필요조건  
1. CS(Critical Section)에 프로세스가 있다면 다른 프로세스의 진입 금지
2. Processs(진행) - CS에 안에 있는 프로세스 외에 다른 프로세스가 CS 진입을 방해해서는 안됨  
3. Bounded waiting(한정대기) - 프로세스의 CS진입은 유한시간내에 허용 되어야 함 

<br/>

## Mutual Exclusion solution
< Low-level mechanisms > (Flexible, 사용하기 까다로움)
### 1. SW solution 
Two Process ME를 보장 : Dekker's Algorithm[flag, turn]   
N-Process ME를 보장	: 다익스트라 알고리즘[flag[진입시도, 1단계, 2단계], turn ]     

단점) 속도가 느리고 구현이 복잡함, ME 실행 중 preemption될 수 있음, Busy waiting(Inefficient)  
※ Busy waiting - 권한을 얻을 때까지 확인   

### 2. HW solution
TestAndSet(TAS) instruction : Test와 Set을 한번에 수행  
=> 실행 중 interrupt 를 받지 않음(선점(preemption)이 일어나지않음)  

장점) 구현이 간단  
단점) Busy waiting 

### 3. OS supported SW solution 
1) **Spinlock(정수 변수)**  
	초기화, P(), V() 연산으로만 접근 가능 => indivisible (or atomic) 연산으로 OS가 보장함  
	단점 ) 멀티 프로세서 시스템에서만 가능, Busy waiting   

2) **Semaphore**    
Busy waiting 해결  
구성)  
음이 아닌 정수형 변수(S) + 초기화 연산, P(), V()으로만 접근 + 임이의 S변수 하나에 ready queue 하나가 할당됨(대기 queue에 들어감)     
※ P() : Probern(검사) / V() : Verhogen(증가)  

종류)  
 	(1) Binary Semaphore : S가 0 or 1 / 상호배제나 프로세스 동기화이 목적으로 사용  
	(2) Counting Semaphore : S가 0 이상 정수값 / Producer-Consumer 문제 등을 해결하기 위해 사용  

특징)   
No busy waiting(대기실에 있기 때문에 루프에 빠지지 않아도됨 => 기다리는 프로세스는 block(asleep)상태가 됨)   
※ semaphore queue에 대한 wake-up 순서는 비결정적으로 Starvation problem이 생길 수 있음  

➕ Semaphore 로 해결가능한 문제들
 - 상호배제(Mutual Exclusion)  
 - 프로세스 동기화 문제(Process synchronization problem) - Process들의 실행순서 맞추기   
 - 생산자 소비자 문제(Producer - Consumer problem)  
	※ 생산자 - 메시지를 생성하는 프로세스 그룹 / 소비자 - 메시지를 전달받는 프로세스 그룹
 - Reader-Writer 문제 : 데이터 무결성 보장 필요  
 						Reader끼리는 동시 접근 가능하지만 Writer들(또는 Reader와 Writer들)이 동시에 데이터 접근시 상호배제 필요 => Reader 또는 Writer에게 우선권 부여  
 - ...   

3) **Eventcount/ sequence**   
 은행번호표 비슷  
 [Sequencer, ticket(S), eventcount, read(E), advance(E), await(E, v)]  
 특징) No busy waiting, No starvation, Semaphore보다 더 low-level 제어 가능   
<br/>
<br/>

< High-levle mechanisms>
### 4 Language-Level solution
1) **Monitor**   
critical data와 critical section을 모아놓은 방(항상 하나의 프로세스만 진입가능(ME)) + 정보은폐   
[Condition variable, wait(), signal() operations]    
 
구성 큐)   
(1) Monitor entry queues : 모니터내의 procedure 수만큼 존재(function)  
(2) Condition queue : 특정 이벤트를 기다리는 프로세스 대기  
(3) Waiting signals queue(신호 제공자 큐) : signal() 명령을 실행한 프로세스가 임시 대기    

장점) 사용이 쉬움, Deadlock등 에러 발생 가능성이 낮음  
단점) 지원하는 언어에서만 사용가능.  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;컴파일러가 OS를 이해하고 있어야함(Critical section 접근을 위한 코드 생성)


<br/>
출처 )
[HPC Lab. KOREATECH 운영체제](https://www.youtube.com/watch?v=EdTtGv9w2sA&list=PLBrGAFAIyf5rby7QylRc6JxU5lzQ9c4tN)
