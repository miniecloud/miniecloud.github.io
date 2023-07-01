---
title: 운영체제 기본 개념정리 - Process
author: mini
date: 2023-01-05 11:10:00 +0800
categories: [OS]
tags: [os, process]
toc : true
---

## 프로세스  
 실행을 위해 시스템(커널)에 등록된 작업, 커널에 의해 관리 받고 메모리를 할당 받음  
=> 자원들을 요청하고 할당 받을 수 있는 능동적인 개체 

### ※ 프로그램
실행 요청 전의 상태, 디스크에 올라가있는 실행 파일


## Process Control Block(PCB)
OS가 프로세스 관리를 위해 필요한 정보를 저장  
[PID, 프로세스 상태, 메모리 관리정보, 입출력 상태정보, 문맥저장 영역(레지스터, 계정 정보)]

## Process Status
![ProcessStatus](/assets/img/posts/processStatus.jpeg)
 - ready : 프로세서(CPU) 외에 모든 자원을 할당 받은 상태로 즉시 실행 가능 상태
 - running : 프로세서와 모든 자원을 할당 받음(실행)
 - asleep(=block) : 프로세스가 특정 이벤트 또는 필요한 자원을 기다리는 상태  
 - terminated : 프로세스 수행이 끝난 상태로 모든 자원을 반납하고 커널에 일부 PCB만 남아있는 상태  
 - suspended : 메모리를 뺏겨 프로세스가 중지 상태, memory image를 swap device에 보관

## 문맥 교환(Context Switching)
Context saving : CPU에서 메모리에 저장. 
Context restoring : 메모리에서 CPU로 북구.  
Context saving과 Context restoring 두 과정을 합쳐 문맥교환이라고 한다.  
 __OS 성능에 큰 영향을 주기때문에__ 불필요한 Context Switching은 줄이는 것이 중요하다. ex) thread 사용

## Interrupt
예상치 못한, 외부에서 발생한 이벤트 ex) I/O interrupt  

### 처리 과정
1. Interrupt 발생
2. 프로세스 중단 (+커널 개입, Context saving 
)
3. 인터럽트 처리
	- Interrupt Handling  
		인터럽트 발생장소, 원인 파악 -> 인터럽트 서비스 할 것인지 결정
	- Interrupt Service  
		인터럽트 서비스 루틴 호출
		


 유튜브HPC Lab. KOREATECH님의 운영체제 강의를 공부한 내용입니다.   
[HPC Lab. KOREATECH 운영체제](https://www.youtube.com/watch?v=EdTtGv9w2sA&list=PLBrGAFAIyf5rby7QylRc6JxU5lzQ9c4tN)
