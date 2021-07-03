---
layout: default
title: Jvm과 메모리구조
parent: 자바
nav_order: 2
permalink: /java/jvm
---

## JVM이란?
{: .fs-9 }
java의 가장 큰이점인 슬로건 "write once run anywhere"를 실현시켜주는 기술이라고 할수있다.<br>
'java virtual machine' 명칭이 말하듯 자바를 실행시키기 위한 가상 기계이다. 자바를 실행시키기 위한 소프트웨어로 생성된 하드웨어라고 이해하면 될것 같다.<br>
JVM은 자바를 실행시키기 위해서는 반드시 필요하다. JVM은 운영체제와 자바 어플리케이션 사이에 위치하여
자바로 만들어진 프로그램을 해당 하드웨어가 해석 가능한 바이트 코드로 변환시켜 실행이 가능하도록 한다.<br>
이로 인해 속도가 느려진다는 말도 있지만 이는 JIT(just-in-time compilation)이라는 실행 시점 컴파일하는 방법으로 극복했다.<br>

![](/assets/images/jvm.png)

1. Class Loader ? 
> java소스는 바이트코드(class) 파일로 변환된다. 이를 엮어서 운영체제의 메모리 영역(Runtime Data Area)로 적제 하는 역할을 한다. 이는 자바 프로그램이 실행중에 이루어진다
2. Execution Engine ? 
> 말그대로 실행 시켜준다. Class Loader를 통해 전달받은 바이트 코드를 기계어로 바꿔주며 지정된 단위로 실행하는 역할이다.
  이때, JIT방식을 이용중이다. JIT는 컴파일러와 인터프리터를 혼합한 방식으로 실행시점에 인터프리터 방식으로 기계어코드를 생성하며 이를 캐싱하여 같은 함수를 부릴때 다시 기계어로 바꿔주는 단계를 생략하여 진행된다.
3. Garbage Collector ? 
> Garbage Collector(GC)는 Heap메모리에 적재된 객체들중 참조되지 않는 객체를 제거 해주는 역할을 실행한다.
GC가 실행되어 객체가 사라지는 시간은 여러가지 환경에 영향을 받기때문에 정확한 시점을 알수가 없다. 이는 자바 프로그램 실행시 반드시 고려해야 할점이다.
Garbage Collector의 구동 방식은 추후 더 자세하게 알아보자.
{: . }
4. Runtime Data Areas? 
{: .text-green-000}

> JVM의 메모리 영역이며 Java 프로그램 실행시 OS로 부터 메모리를 할당받는다. 
  이는 크게 Method Area, Heap Area, Stack Area, PC Register, Native Method Stack로 나눈다.

---
## JAVA 메모리(Runtime Data Areas) 구조?
{: .fs-8 }
<br>
![](/assets/images/javaArea.png)

1. Method area (메소드 영역)
> 클래스의 변수의 타입 이름 접근제어정보같은 필드 정보와 메소드의 이름 타입 파라미터등의 메소드 정보 그리고 타입 정보 상수 정보와 static 변수, final class 등
  한번 올라간후 계속 참조가 가능하도록 설계한 모든 변수및 클래스의 설계도면이 올라가 저장된 영역이라고 할수있다.
2. Heap area (힙 영역)
> new 로 생성된 오브젝트들의 영역이라고 한다. 비번하게 생성되어 GC(garbage collector)가 확인하여 메모리관리를 한다.
3. Stack area (스택영역)
> 임시로 생성되는 지역변수, 파라미터, 리턴값, 연산에 사용되는 값등이 여기에 속한다. <br>
  예로 들자면, 하나의 메소드 안에서 int idx = 100; 이라할경우 스택에 idx 라는 이름으로 100이 생성된다. 하지만 Integer A = new Integer() 일경우 Integer A는 스택에서 생성되나 new Integer라는 실제 값은 힙 영역에 속하게 된다. 이로인해 스택의 A는 힙의 포인트 값을 가지고 있는것이다.
4. PC register (PC 레지스터)
> Thread(쓰레드) 관련 영역으로 쓰레드가 생성될때마다 해당 영역의 주소값과 명령어가 저장되어 실행된다. 이는 쓰레드 관리에 사용되는 메소드 영역이라고 할수있다.
5. Native Method stack
> 자바가 아닌 이외에 자바코드를 실행시키기 위한 환경조성에 사용되는 영역이다 (JNI - 자바 코드가 C/C++ 라이브러리 호출 및 호출 되는것을 가능케 해줌) 

<div class="text-delta" markdown="1">
*** 자바의 쓰레드는 메소드 영역과 힙 영역은 같이 참조하면 사용하지만 나머지 영역은 각자 사용한다.
{:.bg-yellow-100 .fs-3}
</div>
---
<div class="code-example text-delta" markdown="1">
출처 
{: .text-grey-dk-000}

>  https://jeong-pro.tistory.com/148 [기본기를 쌓는 정아마추어 코딩블로그]
>  https://hoonmaro.tistory.com/19 [훈마로의 보물창고]
</div>

