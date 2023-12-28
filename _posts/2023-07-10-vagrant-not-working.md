---
title: vagrant ssh - permission denied(publickey)
author: mini
date: 2023-07-10 11:50:00 +0800
categories: [Etc, Data Engineering]
tags: [data engineering]
toc : true
---

![vagrant ssh permission denied](/assets/img/posts/vagrant-permission-denied.png)

호스트끼리 통신하려고 ssh 키를 새로 만들었다가 vagrant ssh로 접속이 되지않았다. id_rsa값이 새로 생겨서 그런것 같다.

### 해결방법 - private_key 갱신
생성된 호스트의 id_rsa 값을 복사하여 [vagrant_home]/.vagrant/machines/[vm name]/virtualbox/private_key에 붙여넣기하면 된다.




