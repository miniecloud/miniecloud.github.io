---
title: 데이터 파일럿 프로젝트 환경 구축1
author: mini
date: 2023-06-20 11:50:00 +0800
categories: [Data, Data Engineering]
tags: [data engineering]
toc : true
---


## 가상환경을 이용해 분산 서버 만들기
➕ 교제는 CentOS6 기준인데 버전 7부터 바뀐부분이 있으니 주의해야한다.
- 시스템 데몬 설정할때 : service \> systemctl
- 부팅 런레벨 변경 : /etc/inittab \> systemctl set-default multi-user.target
- hostname 변경 : /etc/hosts \> /etc/hostname
- 방화벽 : iptables \> firewalld


### 1. IP 설정하기
1. 외부와 통신을 위해 ifcfg-enp0s3의 ONBOOT=yes로 변경해준다.
2. Host pc와 통신을 위해 eth0을 만들어준다. 이전에 ip 설정에 관해 포스팅했기때문에 생략한다.

※ ifconfig 없을 때  `yum install net-tools`

### 2. ssh 설정
1. `yum install openssh-server openssh-clients openssh-askpass`
2 ./etc/ssh/sshd_config : Prot22 주석을 제거한다.
3. `firefirewall-cmd --permanent --zone=public --add-port=22/tcp`
4. reboot

※ 패키지 설치 확인
`rpm -qa | grep [패키지 이름]`
<br/>
※ 포트 상태확인
`netstat -nlpt `
l : 연결가능 상태
n : 포트넘버
t/u : tcp/udp
p : PID.

 ❗️ ssh 연결을 할때 비밀번호를 맞게 입력해도 'Authentications that can continue: publickey,password,keyboard-interactive'와 같은 문구가 나오며 연결이 되지않았다. 사실 이 부분은 해결하지 못했다. 그래서 대신 ssh 키 로그인으로 바꿨다.ㅠㅠ
ssh key를 생성해서 로그인할 서버에 보내면된다.

#### ssh key 생성하기
1. `ssh-keygen -t rsa -b 4096 `
2. `ssh-copy-id user@[서버 주소]`

### 3. 기타 변경이 필요한 설정
- udev : /dev 하위의 장치들을 관리하는 daemon
- selinux  : 관리자 시스템 엑세스 권한을 효과적으로 제어할수 있게하는 linux시스템용 보안 아키텍처
- vm.swappiness : 스왑활용도를 나타냄. (0: 사용안함, 1: 사용 최소화, 60: 기본값, 100: 적극적으로 활용)
 swap : 시스템에 메모리가 부족할 경우 하드디스크의 일부 공간을 활용하여 작업을 도와주는 영역으로 하드디스크를 일부 RAM처럼 사용할 수 있음
- rc.local : 부팅시 자동실행 명령어 스크립트를 수행. 서버 부팅시 자동 실행되길 원하는 명령어 입력
- security/limits.conf : 한 프로세스가 문제가 생겨도 다른 프로세스에 영향이 덜가도록 방패가 되어주는 설정
	- nproc : 프로세스 최대 개수
	- nofile : 파일 열기 최대 개수

### Failed to load SELinux policy. frezzing

위 파일들을 변경하고 재부팅을 했는데 에러가 발생했다.
![FaledSELinux](/assets/img/posts/FailedSELinux.png)

1. 재부팅
2. 커널 선택할 때 e를 눌러 command prompt 실행
![첫번째](/assets/img/posts/1.png)
![두번째](/assets/img/posts/2.png)
Ctrl + x 누르면 정상적으로 재부팅된다.
3. selinux-policy를 제거한 후 다시 설치한다.
```
yum remove selinux-policy
yum install selinux-policy
```


<br/><br/><br/>
------------------------------------
출처
⌜실무로 배우는 빅데이터 기술⌟
