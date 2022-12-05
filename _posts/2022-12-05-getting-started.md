---
title: 블로그 시작하기 - 레이아웃 적용 안될때
author: mini
date: 2022-12-05 19:33:00 +0800
categories: [Blogging]
tags: []
pin: true
---

 블로그 이전~ 돌고돌아 다시 Chirpy 테마로 돌아왔다.😆 역시 이 테마가 가장 깔끔하고 좋은 것 같다.   
 그런데 새로 빌드하는데 css 가 적용이 안되고 계속 layout: home # Index page가 떴다. 로컬에서는 문제가 없어서 쫌 헤맸다.

![당시화면](/assets/img/posts/page.png){: width='900' height='354'} 
 깃 레파지토리에서 actions를 보면 ruby를 셋업할 때 문제가 생겼다. 우선 밑에 이미지를 보면 3.1로 되어있는데 찾아보니 2.7까지 지원하는 것같았다. 확실하지는 않다.
 ![SetupRuby](/assets/img/posts/build.png)

<br/>
###### **해결 방법**
 ```console
 bundle lock --add-platform x86_64-linux 
 ```
 위와같이 설정하면 된다! 



