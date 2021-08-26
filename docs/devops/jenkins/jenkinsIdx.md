---
layout: default
title: 젠킨스
parent: 네트워크 및 개발환경
nav_order: 1
permalink: /devops/jenkins
---

# 젠킨스?
{: .no_toc }

<div class="code-example text-delta" markdown="1">
*CI/CD 툴 중 가장 많이 쓰이고 접할수있는 툴이 바로 젠킨스이다. <br>
젠킨스 이전 개발자들은 nightly-build 라는 형식의 빌드 정책을 사용하였다. <br>
개발은 낮에 진행하여 git 이나 svn 같은 형상관리툴의 커밋을 진행하였고 <br>
이를 사용량이 적을때인 밤에 build 하는 형식의 정책을 nightly-build 라고 칭한다.<br>
이러한 nightly-build 는 여러 단점이 있었다.  개발자 각각 개인이 merge 전 먼저 테스트를 해보고 난후에  merge 작업을 해야 하며<br>
빌드된 소스를 직접 서버에 배포하여 반영 하는 반복된 작업이 필요하다.<br>
이러한 상황으로 인해 릴리즈 기한과 방식이 복잡하고 오래걸리는 단점이 있었다.<br>
이렇게 탄생한게 젠킨스 이다.<br>
젠킨스는 형상관리툴의 커밋과 같은 이벤트를 모니터링 하여 해당 version의 소스의 검증을 자동으로 실행해준다.<br>
이는 개인이 코드의 검증및 테스트의 진행이 필요치 않아 큰 이점을 제공해주며 코드의 신뢰성도 높아진다.<br>
또한 빌드후 처리 및  반영 또한 자동화 시켜 각 개인이 진행하던 반복적인 일을 <br>
통일화 획일화 시켜주는 이점을 가질수 있습니다.<br>
이외 수많은 플러그인과 파이프라인으로 빌드 및 배포에 기능을 추가하여 보다 개발자에게 개발에 집중할수 있는 환경을 제공해주는 역할을 한다.<br>
</div>

---

## 젠킨스 특징
<div class="code-example text-delta" markdown="1">
- 프로젝트 컴파일시 오류를 검출가능하다.
- 테스트 실행를 통한 신외성을 높일수 있다.
- 코딩 규약에 따른 코드 검증이 가능하다.
- 해당 프로젝트 테스트 환경의 배포를 보다 편리하게 할수있다.
- 프로파일링 툴을 통한 소스의 성능을 감시할수 있다.
- build 자동화를 통한 획일화가 가능하다.
- 빌드 파이프라인 구성을 통해 해당 레이어간의 빌드 구성이 가능하다.

젠킨스단점  
{: .label .label-yellow }
>   젠킨스는 설정이 복잡하다. <br>
>   단일 파일 배포 혹은 설정 변경시에도 불필요한 과정을 진행해야 한다. <br>

</div>
---

## 젠킨스 설치
<div class="code-example text-delta" markdown="1">
- 젠킨스 설치 하기위하여 yum 리파지토리를 설정합니다.

```bash
sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat-stable/jenkins.repo
sudo rpm --import http://pkg.jenkins-ci.org/redhat/jenkins-ci.org.key
```

- yum 으로 설치 합니다

```bash
sudo yum install jenkins
```

- 설치후 젠킨스 설정 파일을 열어 젠킨스 설정합니다

```bash
vi /etc/sysconfig/jenkins
```

젠키스 주요 설정
 - JENKINS_HOME="/var/lib/jenkins"  :  젠킨스 위치
 - JENKINS_USER="jenkins" : 젠킨스 사용자
 - JENKINS_PORT="8080" : 젠킨스 포트번호
</div>
---

## 젠킨스 명령어
<div class="code-example text-delta" markdown="1">
- 시작명령어

```bash
service jenkins start
```

- 종료명령어

```bash
service jenkins stop
```

- 재시작

```bash
service jenkins restart
```
</div>
---
<div class="code-example text-delta" markdown="1">
단어설명  
{: .label .label-blue }

>  CI/CD :  지속적 통합 / 지속적 제공 개발자들의 여러기능 개발을 지속적으로 통합하며 이를 통해 테스트 빌드및 릴리즈를 자동화하여 제공 및 배포 해주는 툴 <br>
>  파이프라인  : 2개 이상의 모듈로 이루어진 프로젝트에서 각각 모듈에 따른 빌드가 필요하며 이에따른 순차진행이 필요하다. 이를 정의해주는것을 파이프라인이라 한다. <br>
</div>