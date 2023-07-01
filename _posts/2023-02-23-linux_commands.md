---
title: 리눅스 명령어2[grep, xargs, sed]
author: mini
date: 2023-2-23 11:50:00 +0800
categories: [OS, Linux]
tags: [linux commands]
toc : true
---

## 파일 내 특정 글자 검색하여 변경하기 

```
grep -rl '\[linux\]' ./* | xargs sed 's/\[linux\]/\[OS\]/g'
```

### grep
`grep [옵션] [패턴] [파일명]`
하나 이상의 패턴과 일치하는 행을 선택하여 입력파일을 탐색  
- c : 선택된 행의 개수 출력  
- f : pattern_file(탐색 패턴이 들어있는 파일. 각 패턴은 개행문자로 분리) 사용  
- i : 대소문자 무시  
- v : 일치하지 않는 행  
- r : 하위 디렉토리 탐색 

### xargs
공백, 탭, 줄 바꾸기 및 파일의 끝으로 구분된 인수를 읽고 이를 인수로 사용하여 지정된 유틸리티를 실행
변수 목록을 여러 하부 목록으로 잘게 나누어 받음

### sed
지정된 파일 또는 표준 입력을 읽고 명령 리스트에 지정된 대로 입력을 수정  

🛑 **invalid command code** 에러  
-i 옵션에 ''를 넣어주면된다.

