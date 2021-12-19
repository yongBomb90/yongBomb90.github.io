---
layout: default
title: SQL 유용한 문법
parent: 개발참조
nav_order: 0
permalink: /develop/00
---
# MY SQL 쿼리 문법 모음

---

### 메일 유효성 검증

```sql
-- 이메일 정규식
SET @EMAIL_REG = '^([-_.]?[0-9a-zA-Z가힣`~!@#$%^&*()-_=+|\\\'\";:/\?])([-_.]?[0-9a-zA-Z가힣`~!@#$%^&*()-_=+|\\\'\";:/\?])*@[0-9a-zA-Z]([-_.]?[0-9a-zA-Z])*.[a-zA-Z]{2,3}$';

SELECT trg
     , IF( trg  REGEXP  @EMAIL_REG , 'Y' ,'N') AS email_regexp
FROM (
		SELECT 'abc@gmail.com' AS trg 
		UNION ALL  SELECT 'abc#gmail.com' AS trg  
	 ) A
;
식
```

---

### MySQL Partition by 구현

```sql
-- FIELD 를 통해 파티션을 나누고 다음 우선순위로 처리 이떄 주의 점은 모든 경우의 수 처리 해야함
SELECT *
FROM   (
		SELECT 'R' AS CD , 0 AS SEQ 
		UNION ALL  SELECT 'E' AS CD , 1 AS SEQ 
		UNION ALL SELECT 'W' AS CD , 2 AS SEQ 
		UNION ALL SELECT 'Q' AS CD , 3 AS SEQ 
       ) A
ORDER BY FIELD(CD , 'Q', 'W' ,'E', 'R' ) ASC


-- 실제 파티션 바이 처리 ....
SELECT A.*
       , ROW_NUMBER() OVER (PARTITION BY A.CD , A.SEQ ORDER BY A.ORD ASC ) AS rn
				
FROM   (
		SELECT 'R' AS CD , 0 AS SEQ  , 0 AS ORD
		UNION ALL  SELECT 'E' AS CD , 1 AS SEQ , 3 AS ORD
		UNION ALL SELECT 'W' AS CD , 2 AS SEQ , 2 AS ORD
		UNION ALL SELECT 'Q' AS CD , 3 AS SEQ , 1 AS ORD
        UNION ALL  SELECT 'E' AS CD , 1 AS SEQ , 1 AS ORD
		UNION ALL  SELECT 'E' AS CD , 1 AS SEQ , 2 AS ORD
		UNION ALL SELECT 'Q' AS CD , 3 AS SEQ , 2 AS ORD
        UNION ALL SELECT 'Q' AS CD , 3 AS SEQ , 3 AS ORD
        
       ) A
;


```

---

### MySQL ROW TO JSON

```sql
-- 컬럼을 JSON으로 조회 한다 -> 에러 터지거나 외부 API 대량 파라미터 생성시 유용
SELECT JSON_OBJECT('seq',seq)
FROM   (SELECT 234 AS SEQ) TRG;
-- '{"seq": 234}'

```

---

### MySQL Conneted By

```sql
/******************************************
1 |'2021-08-18'|'수','1'
2 |'2021-08-19'|'목','2'
3 |'2021-08-20'|'금','3'
4 |'2021-08-21'|'토','3' -- 주말로 인한 워킹데이 추가 X
5 |'2021-08-22'|'일','3' -- 주말로 인한 워킹데이 추가 X
6 |'2021-08-23'|'월','4'
7 |'2021-08-24'|'화','5'
8 |'2021-08-25'|'수','6'
9 |'2021-08-26'|'목','7'
10|'2021-08-27'|'금','8'
******************************************/
SET @YYYMMDD = '2021-10-28' , @WRKDAY = 8 ;
SELECT MAX(TRG.START_DATE) AS START_DATE, -- 워킹데이 처리 기준일자 
	   MAX(TRG.DT) AS END_DATE, -- 워킹데이 마지막일자 
       MAX(TRG.CNT) AS CNT -- 워킹데이수
FROM   (
		WITH RECURSIVE A 
			AS ( 
				SELECT  STR_TO_DATE(@YYYMMDD,'%Y-%m-%d') AS START_DATE  
					 ,  STR_TO_DATE(@YYYMMDD,'%Y-%m-%d') AS DT  
					 ,  1 AS LEVEL  
					 ,  1 AS CNT  
					 ,  DATE_FORMAT( STR_TO_DATE(@YYYMMDD,'%Y-%m-%d'),'%w') AS DD 
				UNION ALL 
				SELECT  A.START_DATE AS START_DATE  
					 ,  DATE_ADD( A.START_DATE , INTERVAL  A.LEVEL DAY ) AS DT  
					 ,  1+A.LEVEL 
					 ,  IF ( DATE_FORMAT( DATE_ADD(A.START_DATE , INTERVAL  A.LEVEL DAY ),'%w') IN ( 6, 0 ) , A.CNT , 1+A.CNT ) AS CNT 
					 ,  DATE_FORMAT( DATE_ADD(A.START_DATE , INTERVAL  A.LEVEL DAY ),'%w') AS DD 
				FROM A 
				WHERE A.CNT < @WRKDAY 
		 ) SELECT START_DATE , LEVEL , DT , DD , CNT FROM A
       ) AS TRG
;
```

---







