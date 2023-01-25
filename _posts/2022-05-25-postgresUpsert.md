---
title: Postgresql update & insert
author: mini
date: 2022-05-25 11:50:00 +0800
categories: [DB, PostgreSQL]
tags: [postgresql]
math: true
toc : true
---

# postgres upsert
DB에 데이터를 넣을 때, 데이터가 있으면 업데이트, 없으면 새로 넣어야했다. 
처음에는 DB에서 값을 먼저 확인한 후 데이터를 update용 데이터, insert 데이터를 따로 나눠서 update와 insert 해줬다. 번거롭다 생각했는데 postgres에서 Upsert라는 기능이 있었다!😲

```sql 
INSET INTO table_name(pk_column, column1, column2, column3)
VALUES('a','b','c')
ON CONFILCT (pk_column) DO
UPDATE SET column1='가', column2='나'
```

# 참고자료
[PostgreSQL](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-upsert/)  
※ ON CONFLICT절을 사용하는 경우, unique 또는 exclude 제약조건이 있어야한다


