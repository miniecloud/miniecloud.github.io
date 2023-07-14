---
title: 데이터 파일럿 프로젝트 환경 구축2
author: mini
date: 2023-06-25 11:50:00 +0800
categories: [Data, Data Engineering]
tags: [data engineering]
toc : true
---

실무로 배우는 빅데이터 기술에 나와있는 파일럿 프로젝트를 진행하려는데 빅데이터 클러스터 구성에서 막혔다.🥲 이 책에서는 빅데이터 시스템 자동화도구인 CM(Cloudera Manager)을 사용했는데 유료로 바꼈다...
그래서 ambari와 Kubernetes 중 고민하다 Kubernetes로 진행하기로했다. 앞으로 상황에 맞게 아키텍처를 수정하며 진행해야겠다.
<br/>
마스터 서버 1대와 노드 서버 2대로 진행한다. 다행히 책에서 학습환경을 자동으로 구축할 수 있는 스크립트를 제공해줘서 쉽게 환경을 구축할 수 있었다. pssh로 하나하나 하려했는데 정말 다행이었다...ㅎ
<br/><br/>

## 가상환경 생성 및 시스템 구성관리
### Vargant
가상화 소프트웨어 개발 환경의 생성 및 유지보수를 위한 오픈 소스 소프트웨어
<br/>
#### 쿠버네티스 클러스터 운영
- vagrant init [name(url)]: Vagrantfile 생성하여 현재 디렉토리를 Vagrant 환경으로 초기화
- vagrant up [VM명] : 현 디렉토리의  Vagrantfile 에 기재된 내용ㅇ르 바탕으로 가상머신을 기동.
- vagrant halt [VM명] : VM 셧다운. 다시 기동하려면 vagrant up
- vagrant status : VM 상태 출력
- vagrant destroy [VM명] : VM 삭제. 데이터도 함께 삭제하여 복원 불가능
- vagrant ssh [VM명] : VM지정해서 로그인

### Ansible
오픈 소스 소프트웨어 프로비저닝, 구성관리, 애플리케이션 전개 도구. 인프라 구성을 기술하기 위해 선언형 언어를 포함하고 있다.


<br/>
### ※ pssh
#### CentOS7 pssh 설치
```
yum update
yum -y install epel-release
yum --enablerepo=epel -y install pssh
```
* EPEL(Extra Packages for Enterprise Linux) Repostory
소프트웨어의 설치 패키지에 쉽게 엑세스할 수 있는 추가 패키지 저장소
RHEL, CentOS, 사이언티픽 리눅스, 오라클 리눅스에서 사용할 수 있음

#### 사용방법
1. ssh 공개키 공유( 환경 구축 1 참고)
2. host 파일 생성
3. 연결확인
`pssh -i -h ~/.pssh_host_files date`
![pssh 결과](/assets/img/posts/psshConnect.png)




<br/><br/>
※ 출처 및 참고자료<br/>
⌜실무로 배우는 빅데이터 기술⌟<br/>
⌜15단계로 배우는 도커와 쿠버네티스⌟<br/>
[vagrant cli](https://developer.hashicorp.com/vagrant/docs/cli)
