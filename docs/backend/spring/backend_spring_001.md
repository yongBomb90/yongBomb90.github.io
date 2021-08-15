---
layout: default
title: IOC 와 DI 그리고 AOP
nav_order: 1
description: "스프링"
parent: spring
grand_parent: 백엔드
permalink: /backend/spring/001
---
# IOC 와 DI 그리고 AOP
스프링 하면 가장먼저 나오는 단어 DI 와 AOP 이 두개의 개념은 스프링의 가장 큰 특징이자 이념이라고 할수 있다.

## IOC (Inversion of Control )
- 제어의 역전이라고 한다. 프레임 워크의 라이프 사이클을 관리한다. 기존 개발자에게 객체의 생성과 의존관계 형성 처리를 했던 반면 스프링에서는 이를 프레임워크에서 직접 처리하게 되었다.

## DI (Dependency Injection)
- 의존성 주입 객체의 의존성이 있을경우 즉, B라는 객체를 생성할려면 A라는 객체가 필요할경우 B에게 A라는 객체를 주입해줌으로서 IOC를 가능하게 해주는 개념이다.

## AOP (Aspect Oriented Programming)
- 관점지향프로그래밍이라고 한다. 즉 어떠한 여러행동을 관점으로 보고 그 행동이 여러가지 관점에도 하나의 공통된 일을 한다면 이를 공통된 방식으로 처리할수 있도록 할수있다.

---
## DI annotation

### @Autowired
- Spring FrameWork가 지원해주는 어노테이션이다.
- 타입 방식으로 검색한다. 타입이 같은 다수의 빈이 존재시 @Qualifier 로 특정빈 선택한다.
- 해당 빈을 찾지 못하면 에러를 뱉어 낸다.

### @Resource
- java가 지원해주는 어노테이션이다.
- 이름 으로 검색한다. POJO가 여럿일 때 명확하게 가져온다.

### @Inject
- java가 지원해주는 어노테이션이다.
- 타입 방식으로 검색한다. 타입이 같은 다수의 빈이 존재시 @Qualifier 로 특정빈 선택한다.

### @RequiredArgsConstructo
- 스프링에서 추천 지향하는 어노테이션이다.
- 생성자를 통해 의존성을 주입하는 방식으로 final 이가능하다는 큰 이점이 있다.
- 주로 Lombok과 함께 쓰인다.