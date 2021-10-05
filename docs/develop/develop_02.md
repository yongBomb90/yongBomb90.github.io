---
layout: default
title: SQL 유용한 문법
parent: 개발참조
nav_order: 0
permalink: /develop/00
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
