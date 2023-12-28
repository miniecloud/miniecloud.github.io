---
title: PostgreSQL - Copy
author: mini
date: 2022-12-23 11:50:00 +0800
categories: [Etc, PostgreSQL]
tags: [postgresql]
toc : true
---

## 테이블을 csv파일로 추출 
DB 테이블의 데이터를 csv파일로 저장하는 Query이다. 
```sql
COPY table_name TO (저장장소) WITH CSV DELIMITER ',' HEADER ENCODING 'UTF8'
```

## csv 파일을 테이블에 추가
```sql
COPY table_name(column1, column2, column3)
FROM 'C:/tmp/test.csv'
DELIMITER ','
CSV HEADER;
```
실행이 완료되면 사진처럼 **COPY (COPY된 행의 개수)**가 뜬다.

<br/>
## Error
### Encoding 관련
![error](/assets/img/posts/db_error.PNG)
위와같은 에러가 날때는 다음과같이 encoding 을 설정해주면 해결된다. 
```sql
COPY table_name TO (저장장소) WITH CSV DELIMITER ',' ENCODING 'UTF8';

```

### 권한문제 관련
![error_not_superuser](/assets/img/posts/copy_error.PNG)
위와같이 에러가 났을때는 copy 명령어 앞에 **\\**만 추가해주면 된다.😀


