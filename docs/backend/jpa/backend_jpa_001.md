---
layout: default
title: ORM
nav_order: 1
description: "ORM"
parent: jpa
grand_parent: 백엔드
permalink: /backend/jpa/001
---
# ORM?
ORM(Object-relatinal mapping)은 단어 그대로 객체(Object)와 관계(RDB)간의 맵핑을 의미한다. 이를 조금더 개발적으로 풀어서 설명한다면, 
OOP적 프로그래밍을 해치지 않고 객체라는 개념으로 RDB에 저장하고 가져오고 수정 삭제하는 행동을 자동으로 가능하도록 지원을 의미한다고 할수있다.
객체의 개념과 RDB의 관계의 개념은 뿌리부터 불일치 하다. 이를 일치시켜준다 라고 짧게 기억해도 큰 문제는 없다.

## ORM 장점
 - OOP적 프로그래밍을 통하여 개발자에게 보다 SOLID하고 직관적인 개발이 가능하다. 
 - 재사용과 유지보수 리팩토리시 테이블간 관계를 보지않아도 문제가 없어 큰이점이 있다.
 - DBMS에 의존성이 없다
 
## ORM 단점
 - 개발자들의 진입장벽이 높다 즉, 어렵다
 - ORM만으로 모든 서비스 구현은 불가능 하다. 복잡성이 높은 구조에서는 불필요한 작업이 높아진다.
 - 프로시저 , 트리거 등등 데이터 베이스에서 제공하는 함수 구현시 리스크가 발생할수 있다.
 - 정확한 설계가 아니라면 큰 속도저하가 생겨난다.
 - 통계나 수많은 테이블을 통해 값을 가져오는 시스템에서는 ORM은 부적합할수도 있다.