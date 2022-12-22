---
title: Linux - 리다이렉션
author: mini
date: 2022-12-15 10:00:00 +0800
categories: [OS, Linux]
tags: [linux]
math: true
toc : true
---

## 리다이렉션
 : 출력의 방향을 바꾼다.

ex) example.py >> example.log 2>&!

 > 0 표준 입력  
   1 표준 출력  
   2 표준 에러  

 > \>  overwirte  
   \>> append  

 > 2>&1 오류를 출력으로 내보냄

<br/>
### 기타
#### ➕ 날짜 추가
 example_$(date +\%m\%d).log


#### ➕ 로그 파일 보관 기간 정하기 
 ```bash
 find /home/log/ -type -f -mtime +30 -exec rm {} \;
 ```

 ※ 찾은 파일에 대해 특정 명령 실행할때   
 find ... -exec ... {} \;





