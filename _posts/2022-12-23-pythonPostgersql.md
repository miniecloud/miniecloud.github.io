---
title: Python에서 PostgreSQL 사용하기
author: mini
date: 2022-12-23 11:50:00 +0800
categories: [Etc, PostgreSQL]
tags: [postgresql]
toc : true
---

## psycopg2
postgresql 을 쉽게 활용할수 있는 라이브러리다.
```
import psycopg2

db = psycopg2.connect(host='', dbname='', user='', password='')
cursor = db.curosr

cursor.execute(sql)

// DB 커밋
db.commit()

//데이터를 불러올때
cursor.fetchall()
```


## sqlalchemy
SQLAlchemy를 사용하면 해당 라이브러리에서 지원하는 DB를 사용할 수 있다.  
사용할 DB의 연결하여 con에 전달한다. 
```
from sqlalchemy import create_engine

engine = create_engine("db(postgres)://(db_user_name):(db_pw)@(ip):(port)/(db_name)")

df.to_sql(name=(table_name), con=engine, schema='public', if_exists='append', index=False)
```


<br/>

## ➕ pandas.io.sql.read_sql()
 DB 테이블에서 데이터를 데이터프레임 형식으로 읽어와 psycopg2와 함께 사용하면 편하다.



