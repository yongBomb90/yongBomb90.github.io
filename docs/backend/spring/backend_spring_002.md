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

2. READ_COMMITTED (level 1)
- dirty read가 방지되는 단계로 커밋된 데이터만 읽을수 있다.
- A라는 트랜잭션이 데이터'ㄱ' 수정시 다른 트랜잭션에서는 접근이 불가능하다.

3. REPEATABLE_READ (level 2)
- 트랜잭션이 완료될때까지 SELECT한 모든 데이터에 Lock을 걸어 수정이 불가능 하도록 한다.
- 선행 트랙잭션이 종료 될때까지 똑같은 데이터를 읽을수 있도록 지원해준다.

4. SERIALIZABLE (level 3)
- 읽기 일관성이 완벽하게 적용된다.
- MVCC(Multi Version Concurrency Control) 불가
> 데이터 조회시 데이터 버전으로 관리하여 데이터 일관성을 높여준다.
- 읽는 작업 조차도 Lock을 걸어 다른 어떠한 레코드의 변화가 없다.

## propagation 
원자성의 단위를 동적으로 처리하게 해주는 옵션이다

1. REQUIRED 
- 부모 트랜잭션이 내에서 실행 없을경우 새로 생성한다,
2. REQUIRES_NEW
- 항상 새로운 트랜잭션을 생성한다.
3. SUPPORT 
- 부모 트랜잭션 내에서만 실행 가능하면 부모가 없을경우 nontransactionally로 진행한다.
4. NOT_SUPPORT
- nontransactionally로 실행 되며 부모가 있을경우 일시정지한다.
5. MANDATORY 
- 부모 트랜잭션 내에서만 실행 가능하면 부모가 없을경우 에러는 생성한다.
6. NEVER 
- nontransactionally로 실행되며 부모가 있을경우 에라가 생성된다.
7. NESTED 
- 부모내에서 진행될경우 부모와는 별개로 커밋 및 롤백이 이루어진다.
