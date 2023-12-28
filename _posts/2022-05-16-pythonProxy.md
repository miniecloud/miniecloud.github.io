---
title: Python Crawling - Proxy 사용하기
author: mini
date: 2022-5-16 11:50:00 +0800
categories: [Etc]
tags: [python-data]
toc : true
---

## requests에서 proxy 사용하기
```python
import requests
proxies = {'http':'http://' + proxy_ip,
		  'https':'https://' + proxy_ip}

requests.get('url', headers=headers, params=params, verify=False, proxies=proxies)
```
IP를 주기적으로 바꿔야한다면 무료 프록시 목록을 미리 받아놓는 것이 좋다.
