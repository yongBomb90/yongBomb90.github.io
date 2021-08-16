---
layout: default
title: Spring Transaction 
nav_order: 2
description: "스프링"
parent: spring
grand_parent: 백엔드
permalink: /backend/spring/002
---
# @Transactional
트랜잭션을 database 카테고리에서 정의한적 있다. 이를 스프링에서 적용하도록 설정을 할때 쓰는 어노테이션이다.
데이터 소스등 여러 설정이 끝나고 사용시 어떠한 고립설 및 원자성을 나눌지에 대해 옵션을 줄수있는대 이는 아래와 같이 처리할수 있다.

---
## isolation
고립성 수준 옵션을 주는 방식이다.

1. READ_UNCOMMITTED (level 0)
- 트랜잭션에서 처리중인 혹은 아직 커밋되지 않은 데이터를 읽는 것을 허용한다 ( 격리성 미보장 )
- dirty read : 다른 트랜잭션에서 커밋되지 않은 데이터도 읽은 행위

2. READ_COMMITTED (level 1) - oracle 기본
- dirty read가 방지되는 단계로 커밋된 데이터만 읽을수 있다.
- A라는 트랜잭션이 데이터'ㄱ' 을 'ㄴ' 으로 수정하고 있다면 B라는 트랜잭션에서는 아직 'ㄱ' 이라고 읽는다.
- Non-repeatable read 가 발생한다. 만약, B가 첫번째에 ㄱ 이라 데이터를 가져왔지만 A 트랜잭션이 완료된후 조회시 ㄴ 이라는 데이터를 얻게 됨에 따라 같은 쿼리가 다른 의미를 가져온다.

3. REPEATABLE_READ (level 2)  - mysql 기본
- MVCC(Multi Version Concurrency Control) 를 사용하여 선행 트랙잭션이 종료 될때까지 똑같은 데이터를 읽을수 있도록 지원해준다.
> 데이터 조회시 데이터 버전으로 관리하여 데이터 일관성을 높여준다. undo 영역에 트랜잭션이 수정하는 데이터를 백업해두어 다른 트랜잭션에서 undo영역을 읽게 만드는 방식이다.
- 트랜잭션이 완료될때까지 SELECT한 모든 데이터에 Lock을 걸어 수정이 불가능 하도록 한다.
- Phantom Read 현상이 일어난다. 즉, undo 와 현재 데이터가 상이 다를경우 SELECT UPDATE 같은 쿼리에서는 다른 결과가 초래 될수있다.

4. SERIALIZABLE (level 3)
- 읽기 일관성이 완벽하게 적용된다.
- MVCC(Multi Version Concurrency Control) 불가
- 모든 작업 에 Lock을 걸어 다른 어떠한 레코드의 변화가 없다. SELECT도 LOCK을 걸어 현재 사용중은 데이터의 모든 접근을 불허한다.

## propagation 
원자성의 단위를 동적으로 처리하게 해주는 옵션이다

1. REQUIRED 
- 부모 트랜잭션이 내에서 실행 없을경우 새로 생성한다,
2. REQUIRES_NEW
- 항상 새로운 트랜잭션을 생성한다. 부모에서 오류가 나도 자식은 커밋 자식이 오류가나도 부모는 커밋
3. SUPPORT 
- 부모 트랜잭션 내에서만 실행 가능하면 부모가 없을경우 nontransactionally로 진행한다.
4. NOT_SUPPORT
- nontransactionally로 실행 되며 부모가 있을경우 일시정지한다.
5. MANDATORY 
- 부모 트랜잭션 내에서만 실행 가능하면 부모가 없을경우 에러는 생성한다.
6. NEVER 
- nontransactionally로 실행되며 부모가 있을경우 에러가 생성된다.
7. NESTED 
- 부모내에서 진행될경우 부모와는 별개로 커밋 및 롤백이 이루어진다. 부모에서 오류가 나면 자식은 롤백 자식이 오류가나도 부모는 커밋
