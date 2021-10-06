---
layout: default
title: SQL 유용한 문법
parent: 개발참조
nav_order: 0
permalink: /develop/00
---
# SQL 처리시 유용한 쿼리 문법 모음

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

```
