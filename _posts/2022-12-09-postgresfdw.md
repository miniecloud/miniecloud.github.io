---
title: Postgresql foreign table 사용하기
author: mini
date: 2022-12-09 11:50:00 +0800
categories: [Etc, PostgreSQL]
tags: [postgresql]
math: true
toc : true
---


### postgres_fdw 설치
✔ target 서버에서 해야한다! 
```
CREATE EXTENSION postgers_fdw;
```
확인
```
\dx
```

### 서버 생성
```
CREATE SERVER server_name FOREIGN DATA WRAPPER postgres_fdw OPTIONS (host '원격db_ip', port '', dbname '원격db_name')
```

### user 매핑
```
CREATE USER MAPPING FOR user_name(targetDB) SERVER test_server OPTIONS(user 'user_name'(원격ib), password '')
```

### Foreign table 생성
```
create foreign table test_table(	
		test_id int,
		name varchar options (column_name 'test_name')
		)
server test_server
options (schema_name 'public', table_name '원격db_table_name');
```
컬럼 명을 다르게 하고 싶다면 options을 써주면 된다.


_foreign_table 확인_
```
select * from pg_foreign_table; 
```


