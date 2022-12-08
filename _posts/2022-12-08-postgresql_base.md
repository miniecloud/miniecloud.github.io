---
title: SQL 기본 정리(PostgreSQL)
author: mini
date: 2022-12-08 11:00:00 +0800
categories: [DB, PostgreSQL]
tags: [postgresql]
math: true
toc : true
---


## DDL(Data Definition Language)
### CREATE
```sql
CREATE TABLE table_name();
```

### ALTER
```sql
-- 테이블 이름 변경
ALTER TABLE table_name RENAME TO new_table_name ;
-- 컬럼 추가
ALTER TABLE table_name ADD COLUMN column_name type;
-- 컬럼명 변경 
ALTER TABLE table_name RENAME COLUMN column_name TO new_column_name;
-- 컬럼 타입 변경
ALTER TABLE table_name ALTER COLUMN column_name TYPE type;
-- 컬럼 제거 
ALTER TABLE table_name DROP COLUMN column_name;
```

### DROP
```sql
DROP TABLE table_name; 
```
<br/>

## DML(Data Manipulation Language)
### INSERT
```sql 
INSERT INTO table_name(column1, column2) VALUES(value1, value2);
```

### UPDATE
```sql
-- 특정 컬럼을 변경할 때
UPDATE table_name SET column='변경내용' WHERE '조건'; 
```
##### ➕ 특정 문자만 변경
```sql
UPDATE table SET column=replace(column, "변경할 문자", "변경") WHERE column like '%변경할문자%'
```
 ※ 데이터를 넣을때 **작은따움표**를 넣으려면 작은따움표 두개를 한번에 넣어주면된다
<br/>
ex) mini's -> mini''s
<br/>


### DELETE & TRUNCATE
DELETE는 데이터만 지워지고 테이블의 용량은 지워지지 않는다. 삭제 후 되돌릴수있다. TRUNCATE는 데이터가 삭제되면 테이블 용량이 초기화된다.   ROLLBACK할 수 없다. 

 - 테이블에서 자동적으로 시퀀스를 재시작
```sql
	truncate table table_name restrat identity
```
 - 테이블 데이터만 삭제(시퀀스 값은 그대로)
```sql
	truncate table table_name continue identity
```
 - 테이블의 데이터를 모두 삭제시 테이블에 연결된 다른 테이블의 데이터까지 모두 사제 
```sql
	truncate table table_name cascade
```
 - 테이블에 연결된 데이터가 하나라도 있으면 데이터를 삭제하지 않음
```sql
	truncate table table_name restrict
```
<br/>

## DCL(Data Control Language)
### GRANT
```sql
GRANT ALL PRIVILEGES ON DATABASE dbname TO newuser;
```
### REVOKE
```sql
REVOKE 권한 ON 대상 FROM user
```
<br/>

## DB 생성 & User 생성
```sql
CREATE DATABASE dbname;
CREATE USER newuser WITH ENCRYPTED PASSWORD 'pass';
```

<br/>
## 기타 
### Sequence 설정
- Sequence 생성
```sql
CREATE SEQUENCE seq_name;
```
- Sequence 시작값 변경
```sql
ALTER SEQUENCE seq_name RESTRAT WITH start_number;
```
- 컬럼 sequence 연결 끊기
```sql
ALTER TABLE table_name ALTER COLUMN column_name DROP default;
```
- 기존에 있던 컬럼에 sequence 적용하기
```sql
ALTER table table_name ALTER COLUMN column_name SET default nextval('seq_name')
```
 - sequence 재설정
```sql
SELECT MAX(id) FROM table;
SELECT pg_catalog.setval(pg_get_serial_sequence('table_name', 'id'), (SELECT MAX(id) FROM table_name)+1);
```


### 제약조건 설정
- 외래키 추가 
```sql
ALTER TABLE table ADD FOREIGN KEY(id) REFERENCE table(id);
```
- 제약조건 삭제
```sql
ALTER TABLE table DROP CONSTRAINT constraint_name;
```



