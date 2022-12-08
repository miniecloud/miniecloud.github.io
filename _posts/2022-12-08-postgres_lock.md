---
title: Postgresql Lock 걸렸을 때
author: mini
date: 2022-12-08 11:20:00 +0800
categories: [DB, PostgreSQL]
tags: [postgresql]
math: true
toc : true
---

## 세션확인
```sql
SELECT * FROM pg_stat_activity
```
 pg_stat_activity 컬럼 유형 &nbsp;&nbsp;&nbsp; ➡️  &nbsp;&nbsp;&nbsp; [pg_stat_activity columns](https://www.postgresql.org/docs/current/monitoring-stats.html#MONITORING-PG-STAT-ACTIVITY-VIEW)

## 특정 세션 종료
```sql
SELECT pg_cancel_backend(PID);
SELECT pg_terminate_backend(PID);
```
cancel - 해당 PID만 종료  
terminate - 해당 PID와 연계된 상위 쿼리 프로세스도 종료


