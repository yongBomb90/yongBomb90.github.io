---
layout: default
title: Rest API 제약조건
nav_order: 1
description: "Rest"
parent: Rest
grand_parent: 백엔드
permalink: /backend/rest/001
---
# Rest API 제약조건!?
Rest는 클라이어트와 서버가 서로 몰라도 메세지만으로 충분히 대화가 가능하도록 하자가 목표이다.
Representational State Transfer 웹 서비스에서 많이 사용되는데 Application 사이에 결합도를 낮추게끔 설계하는 아키텍처 스타일이다.
결합도를 낮춰 클라이언트는 화면만 서버는 리소스만 제공하여 구축하는 방식이라고 할수있다.
이러한 아키텍쳐를 구성할떄 RestFul한 시스템 이라고 정의할려면 아래의 6가지 제약 조건이 필요하다.

1. Client-Server 클라이언트서버
- 클라이언트와 서버는 정확히 나뉘어져 있어야 한다. 서로 별도로 진행되 클라이언트쪽에서는 서버의 리소스 URL만 알면 된다
2. Stateless 무상태성 
- 클라이언트의 요청에는 그요청을 이해하기 위한 모든 정보가 포함되어 있어야 한다.(인증정보도 클라이언트에서 보내준다.)
- JWT 기술도 무상태성을 기본으로 하는 방식이다
3. Cacheable 캐시기능
- 요청에대한 응답시 해당 응답이 캐시가 가능한지 알려주어야 하며 캐시가능한 응답은 캐시처리하여 응답한다. (cache-control 헤더)
4. Uniform Interface 인터페이스 일관화
- 전체적인 시스템 아키텍처를 간단하고 잘 파악할 수 있도록 하기 위한 약속된 Interface 가장 지키기 어려워 하는 부분 이다
> 1. identification of resources : resource가 uri로 식별
> 2. manipulation of resources through representations : representation전송을 통해서 resource를 조작해야 한다.
> 3. self-descriptive messages : 메시지는 스스로를 설명해야 한다.
> 4. hypermedia as the engine of application state(HATEOAS) : 애플리케이션의 상태는 Hyperlink를 이용해 전이되어야 한다
5. Layered System 계층화 시스템
- 시스템 아키텍쳐를 계층화하여 각 구성들 간의 계층을 마음대로 상호작용 할 수 없도록 제한
- 중계서버 로드밸런싱 공유캐시 등 여러 가지 역할이 가능한 시스템을 구성해야 한다.
6. Code on demand 코드 온 디멘드 (선택적)
- code on demand라는 것은 client에 보내는 데이터를 바로 실행 가능한 코드를 보내서 이것을 Client에서 실행할수있어여 한다라는 의미이다

