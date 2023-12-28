---
title: 깃허브 빌드 에러
author: mini
date: 2023-05-30 11:50:00 +0800
categories: [Etc, Git]
tags: [github, jekyll]
toc : true
---

## 깃허브 빌드 에러
![GithubActionError](/assets/img/posts/GithubActionError.png)
빌드하려는데 실패했다. Actions를둘러보니 Test site에서 위와같은 에러가 났다.

HTML-Proofer은 HTML 출력이 유효한지 테스트하는 프로그램이다. disk 관련 포스트에서 **>**를 썼던게 문제였다. 태그로 인식한듯 하다. \이스케이프를 추가해주니 정상 빌드됐다.


