---
title: 정규표현식 - 괄호 안 글자
author: mini
date: 2022-12-15 10:20:00 +0800
categories: [-]
tags: [regular expression]
---

### 괄호 안 모든 글자 추출하기 

__\<[^>]*\>__

 \  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;: &nbsp;&nbsp; 다음 문자를 문자 그대로 인식    
 \\<  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;: &nbsp;&nbsp;< 부터  
 [^>]* &nbsp;: &nbsp;&nbsp; >가 아닌 문자가 0번 또는 그 이상 반복됨  
 \\> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;: &nbsp;&nbsp; > 까지

