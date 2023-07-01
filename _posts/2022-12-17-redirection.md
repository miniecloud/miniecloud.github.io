---
title: 리눅스 명령어1[redirection, date, find, exec]
author: mini
date: 2022-12-15 10:00:00 +0800
categories: [OS, Linux]
tags: [linux commands]
toc : true
---

## Redirection
 : 출력의 방향을 바꾼다.

ex) `example.py >> example.log 2>&!`

 > 0 표준 입력  
   1 표준 출력  
   2 표준 에러  

 > \>  overwirte  
   \>> append  

 > 2>&1 오류를 출력으로 내보냄

<br/>
## Date
### format 지정
`date "+%Y-%m-%d %H:%M:%S" `
### time stamp
`date +%s`

### 특정 날짜 구하기
- 일주일전 
`date -d "-1 weeks"`
- 3일 후 
`date -d "+3 days"`


## find 
-type : d(디렉토리), f(일반파일),l(기호링크), s(소켓) ...  
-name : 이름 검색

### ➕ 로그 파일 보관 기간 정하기 
`find /home/log/ -type -f -mtime +30 -exec rm {} \;`
- exec : 앞의 명령어의 결과를 가지고 다음 명령을 실행    
- {} : 앞의 명령어의 결과가 위치할 곳   
- \ : 이스케이핑(뒤에 글자가 단순한 문자 하나로 해석되도록 한다.)  
- ; : -exec 명령의 끝

## wc
행(-l), 단어(-w), 문자수(-c) 세는 프로그램 







