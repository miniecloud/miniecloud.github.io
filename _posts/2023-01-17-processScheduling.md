---
title: 운영체제 기본 개념정리 - 프로세스 스케줄링
author: mini
date: 2023-01-17 11:10:00 +0800
categories: [OS]
tags: [os]
toc : true
---

## 다중프로그래밍(Multi-Programming)
여러개의 프로세스가 존재할 때 자원을 할당할 프로세스를 선택해야함 => 스케줄링
자원관리 
- 시간 분할 관리  
ex) 프로세스 스케줄링 (프로세서 사용 시간을 프로세스들에게 분배)  
- 공간 분할 관리  
ex) 메모리

<br/>
## 스케줄링의 목적
시스템의 성능 향상  
- 대표적 시스템 성능 지표 : 응답시간, 작업 처리량(단위 시간동안 완료된 작업의 수), 자원 활용도(주어진 시간 동안 자원이 활용된 시간), ...  
 ※ 시스템 목적에 맞는 지표를 고려하며 스케줄링 기법 선택  
- 다중 프로그래밍에서의 시간   
 - 대기시간(Waiting time) : 도착 - 실행시작  
 - 실행시간(Burst time) :  실행시작 - 실행종료   
 - 응답시간(Response time) :  도착 - 첫번째 출력  
 - 반환시간(Turn-around time) : 도착 - 실행종료    

<br/>
## 스케줄링 기준(criteria)
- 프로세스의 특성  
	I/O bound : IO burst 작업이 많은 프로세스 ( CPU burst \< I/O burst )  
	CPU bound : CPU burst 작업이 많은 프로세서( CPU burst \> I/O burst )  
    ※ 프로세스의 수행 = CPU 사용 + I/O 대기  
- 시스템의 특성 (목적)  
   ex) 일괄처리 시스템(Batch system), interaction system, ...  
- 프로세스의 긴급성   
- priority  
- total service time  

<br/>
## 스케줄링 단계
발생 **빈도**에 따라
- Long-term scheduling(가끔)  
	- (스케줄링 단계) Job[device] -> created  
	- Job scheduling  
	- 다중 프로그래밍 정도 조절(시스템 내에 프로세스 수)  
- Mid-term scheduling(종종)    
	- (스케줄링 단계) Suspend ready -> read  
	- 메모리 할당 결정(swapping)   

- Short-term scheduling(자주)  
	- (스케줄링 단계) ready -> runnning   
	- 프로세스 스케줄링(프로세스 할당)  
	- 매우 빨라야함  
	
<br/>
## 스케줄링 정책
1. 선점 vs 비선점  
	※ 비선점의 경우 context switching overhead가 적지만 평균응답시간이 증가  

2. 우선순위  
- Static Priority : **생성시 결정**된 우선순위 유지     
   	장점) 구현이 쉽고 overhead가 적음  
	단점) 시스템 환경 변화에 대한 적응이 어려움   
- Dynamic Priority : 프로세스 상태 **변화에 따라** 우선순위가 변경  
	장점) 유연함  
	단점) 구현이 복잡, overhead가 큼  
	
<br/>
## 기본 스케줄링 알고리즘
### FCFS(First-Come-First-Service) = FIFO
Non-preemption scheduling  
기준) 도착 시간(ready queue 기준)   
자원을 효율적으로 사용 가능, overhead가 적음  
일괄처리 시스템(Batch system)에 적합 | 대화형 시스템(interaction system)에 부적합    
단점) 평균 응답시간이 김, Convoy effect    
※ Convoy effect : 수행시간이 긴 프로세스에 의해 다른(짧은) 프로세스들이 긴 대기시간을 갖게되는 현상


### RR(Round-Robin)
Preemption scehduling  
기준) 도착 시간(ready queue 기준)  
**자원 사용에 제한시간(time quantum)**이 존재. 할당시간이 지나면 반납해야함  
※ time quantum이 시스템 성능을 결정  
특정 프로세스의 자원 독점(monopoly) 방지  
context switching overhead가 큼  
대화형, 시분할 시스템에 적합  


### SPN(Shortest-Process-Next) = SJF(Shortest-Job-First)
Non-preemption scheduling  
기준) 실행 시간 - Burst time이 가장 작은 것 부터   
장점) 평균 대기시간(WT) 최소화  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
시스템 내 프로세스 수 최소화(=> 스케줄링 부하감소, 메모리 절약, 시스템 효율↑)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
빠른 응답
단점) 기아현상(무한대기) 발생  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
정확한 실행시간을 알 수 없음  
 

### SRTN(Shortest-Remaining-time-Next)
Preemptive scheduling(SPN변형)  
잔여 실행시간이 더 적은 프로세스가 생기면(ready) 선정됨  
장점) SPN의 장점 극대화  
단점) 프로세스 생성시 총 실행시간예측이 필요, 잔여시간 추적 필요(=> overhead)   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; => 구현및 사용이 비현실적   


### HRRN(High-Response-Ratio-Next)
Non-preemptive scheduling (SPN 변형: SPN + Aging concepts(기아현상 해결))  
기준) Response ratio가 높은 프로세스 우선  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;응답률 = (WT+BT)/BT =>  필요한 BT 대비 얼마나 기다렸는지  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;※ BT 예측 기법이 필요(overhead)


### MLQ(Multi-leve Queue)
작업(or 우선순위)별 별도의 **ready queue**를 가짐  
※ 최초 배정된 queue를 벗어나지 못함  
&nbsp;&nbsp;&nbsp; 각각의 queue는 자신만의 스케줄링 기법을 사용  
Queue 사이에는 우선순위 기반의 스케줄링 사용  
장점) 중요한 것은 빠른 응답  
단점) 여러개의 Queue 관리 등 스케줄링 overhead  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
우선 순위가 낮으면 기아현상 발생  


### MFQ(Multi-level Feedback Queue)
프로세스의 Queue간 이동이 허용  
Feedback을 통해 우선순위 결정   
특징) Dynamic priority   
 　　Preemptive scheduling   
 　　Favor short burst-time  
 　　Favor I/O bounded process   
 　　Improve adatability   
장점) 프로세스에 대한 사전정보 없이 SPN, SRTN, HRRN기법의 효과를 봄   
단점) 설계 및 구현 복잡, 스케줄링 overhead가큼, 기아현상 등  
변형) 각 큐마다 시간할당량을 다르게  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;I/O bounded 프로세스 상위 큐로 우선순위 높임(CPU를 짧게 쓰므로 빨리 처리하여)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;에이징 기법 

※ Parameters for MFQ scheduling : Queue 수, 최초 Queue배정 방법, ...


##### 마무리 
< ready queue 하나 >
- FCFS, RR  : 공평성
- SPN, SRPN, HRRN : 효율성, 성능  
=> 문제점) 실행시간 예측(힘듦) 부하  
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;👇 대안    

< raady queue 여러개 > 
- MLQ
- MFQ



<br/>
출처 )
[HPC Lab. KOREATECH 운영체제](https://www.youtube.com/watch?v=EdTtGv9w2sA&list=PLBrGAFAIyf5rby7QylRc6JxU5lzQ9c4tN)
