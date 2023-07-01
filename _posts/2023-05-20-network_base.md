---
title: 프로토콜 기본요소 
author: mini
date: 2023-05-20 11:50:00 +0800
categories: [Network]
tags: [study, network]
toc : true
---

## 2계층

이더넷 : 같은 네트워크 대역 내에서 사용, 네트워크 대역이 바뀔 때마다 새로 작성

<br/>
## 3계층
다른 네트워크 대역(LAN) 연결 - 장비 : 라우터   

IPv4 주소 : 현재 PC에 할당된 주소. 
서브넷 마스크 : IP주소에 대한 네트워크의 대역을 규정  
게이트웨이 주소 :  외부와 통신할 때 사용하는 네트워크의 출입구


### 사설IP와 공인IP 
➕ classlessIP
공인IP : 네트워크 통신망에서 통신할때 사용  
사설IP : 같은 네트워크 대역에서 사용  

#### NAT(Network Address Translation)
IP패킷에 있는 출발지 및 목적지의 IP주소와 TCP/UDP 포트 숫자 등을 바꿔 재기록하면서 네트워크 트래픽을 주고 받게 하는 기술

#### 포트포워딩
특정 IP주소와 포트 번호의 통신 요청을 특정 다른 IP와 포트 번호로 넘겨주는 네트워크 주소 변환(NAT)의 응용 기술
방법)
1. 공인 IP 2의 특정 포트로 전송   
2. 특정 포트로 들어온 요청을 다른 특정 IP의 특정포트로 전송

<br/>
### ARP 프로토콜
IP주소를 이용해서 MAC주소를 알아냄, ARP 캐시 테이블에 입력  
방법)   
IP주소만 알고있는 컴퓨터는 브로드캐스트로 ARP 요쳥 패킷을 보냄  -> IP주소가 자신의 IP주소인 컴퓨터만 mac주소를 입력하여 응답패킷을 보냄   

ARP 캐시테이블 확인
```
arp -a t
```

<br/>
### IPv4
네트워크 상에서 데이터를 교환하기 위한 프로토콜로 데이터가 정확하게 전달될 것을 보장하지 않음.  
※ IPv4 붙고 MTU로 거르고 이더넷 붙음

### ICMP
네트워크 내에서 데이터 전송과 관련된 문제를 전달하기 위해 사용
> 8 - 요청  
  0- 응답 
  3-Destination Unreachable
  11- Time eexceed 
  5-보안관련

### 라우팅 테이블
최적의 경로를 가지고있음(장비)
```
netstat -r
```
#### 다른 컴퓨터와 통신과정
ex) Ping 과정[Eth | IPv4 | ICMP요청]  
송신 컴퓨터는 이더넷에 게이트웨이를 목적지로 패킷을 보냄(Mac주소를 모르면 ARP 진행) -> 게이트웨이는 IPv4 패킷을 확인하여 최종 목적지가 자신이 아님을 확인 -> 최종 IP를 라우터테이블에서 확인 -> 라우터테이블의 결과에 따라 이더넷을 새로 작성 -> 보냄 -> 최종 목적지에 닿을때까지 반복 -> 최종 목적지에 도착하면 ICMP 패킷을 확인하여 응답을 함

 
## 4계층 
송신자의 프로세스와 수신자의 프로세스를 연결

### UDP
- 비연결지향형. 신뢰성이 낮음, 일반적으로 오류의 검사와 수정이 필요없는 프로그램에서 수행
- UDP 사용 프로그램 : DNS서버, tftp 서버(파일 전송), RIP프로토콜(라우팅 정보를 공유) 


### TCP
- 연결지향형. 안정적으로, 순서대로, 에러없이 교환
- 통신과정
	- 3way handshake(연결 수립)
	```sequence
	Client-->Server: SYN[S:100, A:0]
	Server-->Client: SYN+ ACK[S:2000(랜덤값), A:101(이전S +1)]
	Client-->Server: ACK[S:101(이전A), A:2001(이전 S+1)]  
	# ------ 연결 완료 후 데이터 전송 시 -----
	Client-->Server: PSH+ACK[S:101, A:2001] # 데이터 크기 : 100byte
	Server-->Client: PSH+ACK[S:2001, A:201] #데이터 크기 : 500byte
	Client-->Server: ACK[S:201, A:2501]
	```
> ※ 연결이 완료되고 요청을 보낼때 SEQ번호와 ACK번호가 그대로 사용됨, 단 데이터(페이로드)가 추가됨에 따라 ACK 번호는 받은 SEQ번호 + 데이터의 크기가 됨   
- TCP 상태전이도
	- LISTENING : 포트가 열려있는 상태 
	- ESTABLISHED : 연결이 서로 수립된 상태 


### 포트 번호 
하나의 포트는 하나의 프로세스만 1:1 연결이 된다. 특정 프로세스의 연결 다리가 된다. 그래서 다른 컴퓨터의 여러 프로그램으로부터 1:다 연결을 받을 수 있다. 

#### 포트 번호 종류(0~65535) 
- Well-Known 포트(0~1024) 
	- 전 세계적으로 정해진 포트(절대적인건 아님)
	- ex) FTP:20,21,  SSH:22, TELNET:23,  DNS:53, HTTP:80, HTTPS:443... 
- Registered 포트  
	- 조금 유명한. 
	- ex) 오라클 DB서버:1521, MySQL서버:3306, MS원격 데스크탑: 3389
- Dynamic 포트   
	- 일반 사용자들이 사용(아무거나)    
	- 범위) 49152 ~ 65535  


#### 연결정보 확인
```
netstat -ano
# mac OS
netstat -anv
```

## 7계층
※ 7계층 프로토콜은 소켓 통신 프로그램으로 데이터를 보내는 형식을 정해서 만들 수 있다. 

### HTTP(HyperText Transfer Protocol)
➕ SSL/TLS = HTTPS
- www에서 쓰이는 핵심 프로토콜. 문서의 전송을 위해 쓰이는데 오늘날 음성, 화상 등 여러종류의 데이터를 MIME로 정의하여 전송 가능

- 구조 [Request Line | Header | 공백 | Body]
	- Request Line = [ **요청 타입** | 공백 | **URI** | 공백 | HTTP 버전]
		- 요청 타입 :  GET(Header), POST(Body)
		- URI(Uniform Resource Identifier) : 인터넷 상에서 특정 자원(파일)을 나타내는 주소 
		scheme ://host[:port][/path][?query]	

		- 응답프로토콜 : [HTTP 버전 | 공백 | 상태코드 | 공백 | 상태문구]
			
- 요청 헤더 
	- Cookie : 서버로부터 받은 쿠키를 다시 서버에게 보내주는 역할. http1.1버전에서 요청할때 필수로 보내야함


<br/>
---------------------
출처 : [따라하면서 배우는 IT](https://www.youtube.com/watch?v=6f5lmOSfdsE&list=PL0d8NnikouEXVn9FfoX2XVlGgEArLDiLZ&index=44)
