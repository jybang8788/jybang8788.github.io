---
title: "[Oracle]find slow query"
date: 2018-11-08 15:47:28 -0400
categories: jekyll update
---

Oracle 오래 걸리는 Query 확인하기
=================

```
    SELECT ROWNUM NO,
       PARSING_SCHEMA_NAME,
       to_char(ELAPSED_TIME/(1000000 * decode(executions,null,1,0,1,executions)),999999.9999 ) 평균실행시간,
       executions 실행횟수,
       SQL_TEXT 쿼리 ,
       SQL_FULLTEXT
  FROM V$SQL
 WHERE  LAST_ACTIVE_TIME > SYSDATE-1
    AND ELAPSED_TIME >= 1 * 1000000 * decode(executions,null,1,0,1,executions)
   and PARSING_SCHEMA_NAME = 'SchemaName'
 ORDER BY 평균실행시간 DESC, 실행횟수 DESC;
```