---
layout: default
title: JWT 토큰?
nav_order: 2
description: "Oauth"
parent: Oauth
grand_parent: 백엔드
permalink: /backend/oauth/002
---
# JWT토큰 이란?
JSON Web Token 의 약자이다. 사용자의 인증을 위해 자가수용적인 방법으로 정보를 가지고있는 표준화된 암호화 토큰입니다.
모든 정보는 JSON 방식으로 이루어져 있습니다. 이러한 방식은 인증처리의 결합도을 낮춰주는 방식이된다.
주로 REST full 서버에서 사용하고 있고 이전에서 설명한 Oauth 방식에서 토큰을 JWT로 구성하는 방식이 많이 쓰이고 있습니다.

### JWS? JWE?
- JWS :  JSON Web Signature JSON으로 전자 서명을하여 URL-safe 문자열로 표현한 것.
- JWE :  JSON을 암호화하여 URL-safe 문자열로 표현한 것.

---

### JWT 구조?

<div class="code-example text-delta" markdown="1">
HEADER.PAYLOAD.SIGNATURE
</div>

JWT 구조는 header payload signature 로 나누면 각자 "." 으로 구별한다.

- header : JWT검증시 어떠한 알고리즘으로 암호화하였는지를 알려준다. alg는 서명 시 사용하는 알고리즘이고, kid는 서명 시 사용하는 키(Public/Private Key)를 식별하는 값이다.

```json
{
    "alg": "ES256",
    "kid": "Key ID"
}
-> 해시화
Base64URLSafe(UTF-8('{"alg": "ES256","kid": "Key ID"}')) -> eyJhbGciOiJFUzI1NiIsImtpZCI6IktleSBJRCJ9
```

- payload : 사용자의 정보를 가지고 있는 값이다.

```json
{
    "iss": "jinho.shin",
    "iat": "1586364327"
}
-> 해시화
Base64URLSafe('{"iss": "jinho.shin","iat": "1586364327"}') -> eyJpYXQiOjE1ODYzNjQzMjcsImlzcyI6ImppbmhvLnNoaW4ifQ
```

- Signature : 헤더와 페이로드를 합치고 해당 문자열을 서명한 값이다. 즉 위의 정보가 유효한지 알기위한 값이다.

```json
Base64URLSafe(Sign('ES256', '${PRIVATE_KEY}','eyJhbGciOiJFUzI1NiIsImtpZCI6IktleSBJRCJ9.eyJpYXQiOjE1ODYzNjQzMjcsImlzcyI6ImppbmhvLnNoaW4ifQ'))) 
-> MEQCIBSOVBBsCeZ_8vHulOvspJVFU3GADhyCHyzMiBFVyS3qAiB7Tm_MEXi2kLusOBpanIrcs2NVq24uuVDgH71M_fIQGg
```

이렇게 구해진 3가지 값을 "." 단위로 합치면 JWT가 된다
```json
eyJhbGciOiJFUzI1NiIsImtpZCI6IktleSBJRCJ9.eyJpYXQiOjE1ODYzNjQzMjcsImlzcyI6ImppbmhvLn
NoaW4ifQ.eyJhbGciOiJFUzI1NiIsImtpZCI6IktleSBJRC9.eyJpYXQiOjE1ODYzNjQzMjcsImlzcyI6Imp
pbmhvLnNoaW4ifQ.MEQCIBSOVBBsCeZ_8vHulOvspJVFU3GADhyCHyzMiBFVyS3qAiB7Tm_ME
Xi2kLusOBpanIrcs2NVq24uuVDgH71M_fIQGg
```

이를 통해 서버와 클라이언트는 인증처리를 하게된다.


---
### JWT 장단점?
- 장점
1. 무상태성의 확장이 가능하다. 인증 서버에서의 한번의 처리로 인해 이에 관련된 리소스 서버에서는 토큰의 검증만으로 인증이 가능하기 때문에 보다 결합도을 낮출수있다.
2. 트래픽에 대한 부담이 적어진다
3. 보안성 쿠키를 사용하지 않아 해당 약점이 사라진다.
4. 모바일 웹 등 클라이언트 기기의 종류에서 자유롭다

- 단점
1. 길이에 따른 데이터 크기의 증가
2. 탈취시 Paload의 크리티컬한 정보가 노출된다. 또한 토큰의 탈취만으로 서버의 인증을 통과할수 있다.

---
### JWT사용방향
현재 여러 플랫폼에서는 백엔드 아키텍쳐로 MSA를 가져가는 형상이 자주 보이고 있다. 이는 인증은 SSO방식을 필수적으로 가져갈수 밖에 없고 이때 JWT를 사용하고 있는 추세이다.
한번의 인증으로 여러 서버에서 인증이 가능하고 인증또한 효율적이고 간단하게 처리할수있어 안쓸수야 없는 아주 좋은 인증 방식이다.
하지만 이러한 방향을 선택했을시 JWT의 단점인 탈취시 어떠한 방식으로 처리해야 하는가는 아직도 의문점이다. JWE방식을 사용한다 한들 서버의 키가 노출된다면 모든 인증은 뚤리고
토큰이 하이재킹 된다면 이또한 인증의 구멍이 생길수 밖에없다. 그래서 만료시간을 짧게 준다는 방식을 사용하지만 이또한 큰 해결책은 아닌것 같다.
이러한 단점을 크게 생각해보고 이에 대한 해답을 제시하면서 해당 기술의 도입과 개발을 진행하는것이 좋을것같다.

