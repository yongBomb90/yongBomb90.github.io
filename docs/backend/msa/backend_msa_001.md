---
layout: default
title: MSA란?
nav_order: 1
description: "MSA"
parent: MSA
grand_parent: 백엔드
permalink: /backend/msa/001
---
# MSA !?
MicroService Architecture 의 줄임말이다. 소프트웨어 아키텍쳐중 하나의 기법이다.
간단히 말하자면 하나의 서비스를 최대한 독립적인 단위로 나누어 각각의 상호작용 하며 하나의 서비스를 구성하는 방식이라고 할수있다.
독립적인 단위는 모두 독립적으로 배포가 가능하여 의존성이 없어야 한다.
MSA를 이해하기 위해서는 기존의 서비스의 방식을 이해해 보아야 한다.

---

### Monolithic  vs SOA vs MSA 
<br>

#### - Monolithic
![](/assets/images/mono.png)

Monolithic Architecture는 모든 구성요소가 하나의 단위로 통합된 프로젝트 형식을 말한다. 해당 서비스의 모든 기능이 뭉쳐 있다고 생각하면 된다.
하나의 디비 하나의 서버 하나의 프로젝트로 진행이 된다. 주로 작은단위 혹은 빠른 개발이 필요시 해당 아키텍쳐 구조를 이용한다.

- 장점 : 
    1. 테스트가 용이하다
    2. 다양한 레퍼런스와 인프라 구조
    3. 서버가 한대이기 때문에 비용이 싸다.

- 단점 :
    1. 한기능의 이슈가 모든 서비스에 영향을 끼친다.
    2. Scale-out이 어렵다
    3. 서비스의 변경에 대한 사이드 이펙트 리스크가 크다.
    4. 배포시 긴시간이 걸린다.
    5. 개발환경이 하나로 닫쳐있다.


<br>

#### - SOA

![](/assets/images/SOA.png)


Service Oriented Architecture 약자 이다. 서비스 단위로 기능 단위를 나누어 서비스를 제공하는 방식이다.
여기서 말하는 서비스는 회사로 치면 하나의 부서라고 생각하면된다 재무, 인사, 마케팅 이런 식으로 큰단위의 로직들이 서로 동시적인 상호작용이 필요 없는 단위로 나눈다고 생각하면 된다.

- 장점 : 
    1. 서비스 단위로 개발되어 결합도를 낯출수 있다.
    2. 비지니스로직의 재사용이 가능하여 확장성과 유연성이 증가한다.
- 단점 :
    1. 하나의 DB사용으로 의존성이 존재한다.
    2. 레퍼런스가 부족하다.

#### - MSA

![](/assets/images/MSA.png)

위에서 설명하였듯이 하나의 서비스를 최대한 독립적인 단위로 나누어 각각의 상호작용 하며 하나의 서비스를 구성하는 방식이다. 
SOA와는 다르게 각각의 단위는 재사용성이 없이 완벽한 독립적으로 구성 되어야 하며 서비스단위가 아닌 비즈니스 단위로 나뉘어 진다. 회사로 치면 서류작성, 연차승인, 연봉계약 이렇게 일단위로 나눈다.
해당 방식에서는 단위별로 데이터 베이스 프레임 워크 등등 모두 독립적으로 개발하되 HTTP API로 주고 받을수만 있으면 된다.

- 장점 : 
    1. 최소한의 의존성만 가진다.
    2. 새로운 모듈 기능의 확장의 용이하다.
    3. 개별 단위의 오류가 다른 단위로 전이 되지 않는다.
    4. 개발자의 보다 심도 높은 기술이 가능하다.
    5. 개별 배포로 보다 빠른 배포가 가능하다.

- 단점 :
    1. 서비스간 통신을 위한 개발이 필요하며 이는 사용자의 응답시간이 늘어난다.
    2. 트랜잭션 처리등 오류에 대한 처리가 어렵다.
    3. 통합테스트가 어렵다
    4. 배포 파이프라인 설계 및 구성이 중요하다.


---

### MSA 기술의 가장 필요 능력은 현재 서비스 구조 파악에 따른 아키텍쳐 선택이다

<br>

현재 IT기업들은 서비스의 다양화와 트래픽 증가 및 프로젝트 확장에 따라 MSA구축으로 바뀌고 있는 상태이다. 복잡하고 설계가 어렵지만 이에 따른 결과가 있기 때문일겁니다.
하지만 무작정 MSA의 도입을 해당 프로젝트의 독이 될수도 있습니다. 잘못된 구축 설계와 에러전이 및 트랜잭션 오류로 크나큰 문제들이 생겨날수있기 때문입니다.
현재 프로젝트에서 고쳐나가야 하는점과 이에 따른 아키텍쳐를 선택하는 것이 보다 중요한 능력일것 같습니다.
이후 MSA 구성에 필요한 Spring cloud에 관해 공부해볼려고 합니다.