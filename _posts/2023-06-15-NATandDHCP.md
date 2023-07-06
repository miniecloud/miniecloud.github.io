---
title: NAT, DHCP
author: mini
date: 2023-06-15 11:50:00 +0800
categories: [Network] 
tags: [study, network]
toc : true
---


## 네트워크 통신을 도와주는 기술
### NAT
IP주소를 다른 IP주소로 변환하는 기술로 IPv4 부족 문제를 해결하기 위해 많이 사용했다. 

#### 동작방식
1. 송신자가 패킷을 보내면 NAT는 외부 통신이 가능한 공인 IP로 변경 후 변경 전후의 IP를 NAT 테이블에 저장  
2. 수신한 서버는 응답을 보내면 NAT는 NAT테이블에 적힌 원래 IP로 패킷을 전송  

※ NAT는 주소 변환 후 역변환이 정상적으로 수행되어야만 통신이 가능하다. 

※ PAT은 NAT가 포트까지 확인하고 기록한다. 


### DHCP
IP를 동적으로 할당하는데 사용되는 프로토콜.  
사용자가 작성해야할 IP주소, 서브넷마스크, 게이트웨이, DNS 정보 등 자동으로 할당받아 사용 가능  

#### DHCP 동작 방식  
1. DHCP Discover  
클라이언트는 브로드캐스트로DHCP 서버를 찾기위해 DHCP 메시지를 전송(UDP사용)
2. DHCP Offer  
DHCP 서버는 클라이언트에게 할당할 IP 주소 및 기타 정보 를 전송  
3. DHCP Request    
제안받은 IP주소와 DHCP 서버 정보를 포함한 DHCP요청 메시지를 브로드캐스트로 전송. 
4. DHCP Acknowledgement  
요청을 받으면 DHCP 서버에 해당 IP와 클라이언트 사용 시작 정보를 기록하고 클라이언트에게 메시지를 정상적으로 수신했다는 응답을 전송  


<br/>
## VirtualBox 네트워크 설정
VM에는 DHCP서버와 NAT 엔진이 내장되어 있다.

### Not attached 
네트워크 연결이이 없다. 테스트에 유용하다. 

### NAT
외부 네트워크로 연결할 때는 NAT 모드를 사용한다. NAT모드는 DHCP를 통해 IP 주소를 할당받는다.  단, Host나 LAN에서 VM으로의 통신은 포트포워딩을 해야한다.   

### host-only adapter
VM끼리 연결을 위해서는 Host-only adapter을 사용한다. Host-only adapter은 host operating 시스템을 만들어 사용한다. host-only 네트워크는 외부 장비와 연결되는것을 허용하지 않기때문에 게이트웨이는 없다.
host-only network의 기본 주소는 192.168.56.0/24이고 host machine은 192.168.56.1이다. DHCP서버 부분을 체크하고 사용할수 있다.   


<br/><br/><br/>
------------------------------------------------
참고자료  
IT 엔지니어를 위한 네트워크 입문    
[VirtualBox Network Setting](https://www.nakivo.com/blog/virtualbox-network-setting-guide) 
