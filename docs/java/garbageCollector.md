---
layout: default
title: Garbage Collector?
parent: 자바
nav_order: 3
permalink: /java/gc
---
##  Garbage Collector?
{: .fs-9 }
영화나 드라마에서 컴퓨터관련 내용이 나올때 자주 등장하는 단어가 있다. "서버 메모리가 부족합니다."
이말은 무엇일까? 이뜻은 컴퓨터 용량 즉, C드라이브의 GB가 모자르다라는 말도 되지만 주로 프로그램이 실행될때 사용되는 메모리의 부족을 말해준다.
프로그램을 돌린다면 해당 프로그램의 소스코드를 실행하기 위하여 하드웨어에서 할당해주는 공간이 필요하다. 해당 메모리는 유한하여 부족한일이 생긴다.
그러면 이러한 메모리를 관리하는 소스코드나 기능이 필요하지않을까? 자바에서는 이러한 메모리 관리를 위해 Garbage Collect(GC)를 사용하게 된다.
이러한 메모리 관리로 개발자는 소스코드를 작성시 메모리관리에 크게 신경쓰지 않아도 되는 환경이 구축되었다.
하지만 GC의 처리방식 및 종류에 관하여 무지한 상태로 코드를 짠다면 메모리 누수로 인하여 프로젝트가 엉망이 되지않을까?
GC는 대규모 프로젝트에서 절대 무시못하는 기능으로 제대로 알고 사용할수 있도록 해야한다.


## stop-the-world
GC발생시 모든 프로그램의 스레드는 멈추가 GC가 실행되는 스레드만 실행되어야만 한다.
해당 이유는 GC시 객체의 검사가 끝난후 다른 스레드가 동시에 사용하고 있다면 이는 객체를 검사했던 의미가 없어지게 된다. 여러 이유상  GC스레드 외의 모든 스레드는 멈춰야 한다. 이러한 상태를 **stop-the-world** 라 칭한다.


## Heap Area
자바에서는 런타임 메모리라 칭하는 공간이 있다. 이들중 가장 빈번히 사용되는 메모리가 Heap 메모리이다. 그리하여 GC는 Heap 메모리 관리에 사용된다.
Java 8 version 으로 보았을때 아래의 그림과 같다.
![](/assets/images/javaHeapMem.png)
영역을 나누는 이유는 GC가 만들어진 가정 때문이다.
> 1. 대부분 객체는 접근불가 상태가 된다
> 2. 오래된 객체가 젊은 객체로의 참조는 아주 적게 이루어진다.

이러한 가설로 영역을 크게 3가지로 나누게 된다.

> 1. **Young** 영역..<br>
     새롭게 생성된 객체들이 존재한다. 가설에서 처럼 많은 객체들이 생성되고 사라진다. Minor GC가 발생한다.
> 2. **Old** 영역..<br>
     Young 영역에서 살아남은 객체들이 존재한다. Young 영역보다 크게 설정되며 Major GC(혹은 Full GC)가 발생한다.
> 3. **Metaspace** 영역..(이전 Permanent 영역)<br>
     Class, Method의 Meta Data, Static Object 변수, 상수 JVM,JIT 관련 데이터가 존재하며 이는 JVM이 아닌 OS가 관리하는 Native메모리 영역에 속한다.

## Minor GC
Young 영역에서 일어나는 GC를 Minor GC라 칭한다.
Young 영역은 3개의 영역으로 나뉜다.
> Eden 영역<br>
> Survivor 영역(2개)<br>

이렇게 나누고 해당 영역들을 아래와 같이 관리한다.

> 1. 새로 생성된 객체는 Eden에 저장된다
> 2. Eden 에서 GC실행이 이루어지고 이후 살아남은 객체는 Survivor-1 으로 이동한다.
> 3. Survivor-1이 가득찬다면 Eden이 참조하는 객체만 Survivor-2로 이동후 모두 삭제된다.
> 4. 이를 반복하다가 어느횟수 이상이 된다면 이 객체를 Old 영역으로 이동된다.

Young영역에서 메모리 할당기술로 2개를 들수있다.
> 1. **bump-the-pointer** <br>
     Eden은 마지막 객체가 가장 위에 있다 이를 통해 새로 생성된 객체는 Eden의 넣기 적당한지 확인후 적당할시 Eden에 가장 맨위의 넣는다 이를 통하면 새로운 객체가 생길때 마다 마지막 으로 추가된 객체만 점검하면 되므로 빠른 할당이 가능하다.
> 2. **TLABs(Thread-Local Allocation Buffers)** <br>
     멀티 스레드 환경시 사용되는 기술이다. 이는 만약 여러 스레드에서 하나의 객체를 참조한다면 락되는 현상이 이루어질것이다. 이는 큰 성능저하를 가져오기 때문에 이를 극복하기 위하여 스레드당 각각의 작은 Eden을 사용하여 이를 극복하는 방식이다.

## Major GC
Minor GC 거처서 살아남은 객체들이 Old에 싸이게 된다. 하지만 Old 또한 유한하기 때문에 언젠가는 모두 차게될것이다 이떄 실행되는 GC를 Major GC라 칭한다.
Major GC에는 여러가지 방식이 있다
> 1. **Serial GC (-XX:+UseSerialGC)** <br>
     mark-sweep-compact이라는 알고리즘을 사용한다. 이는 먼저 Old 영역에 살아 있는 객체를 식별(Mark)한후 힙(Heap)의 앞부터 끝까지 살아남은 객체를 남긴후(Sweep)
     각 객체들이 힙의 가장 앞 부분부터 채워나간다(Compaction). 쓰레드가 하나로 이루어진다. 그러므로 작은 메모리나 CPU코어가 적을때만 사용한다. Minor GC와 Major GC모두 stop-the-world가 발생한다.
> 2. **Parallel GC (-XX:+UseParallelGC)** <br>
     Serial GC 방식을 Young 영역에 대해서만 다수의 쓰레드가 진행되는 방식이다.  Minor GC와 Major GC모두 stop-the-world가 발생한다.
> 3. **Parallel Old GC(-XX:+UseParallelOldGC)** <br>
     Parallel GC 방식에서  Old 영역도 다수의 쓰레드가 진행되는 방식으로 Mark-Summary-Compaction 단계를 거친다.  Minor GC와 Major GC모두 stop-the-world가 발생한다.
> 4. **CMS GC (-XX:+UseConcMarkSweepGC)** <br>
![](/assets/images/CMS_gc.png)
     Serial GC에서 mark하는 방식이 부터 다르다 초기 Initial Mark 단계에서 클래스 로더에 가장 가까운 객체중 살아있는 객체만 찾아 끝낸다. 이로 인해 멈추는 시간이 줄어든다. 이후 Concurrent Mark 단계에서는 살아있다고 확인된 객체들이 참조하는 객체를 확인한다. 이때는 stop-the-world가 진행되지 않는다. 이후 Remark 단계에서는 Concurrent Mark 단계에서 새로 추가되거나 참조가 끊긴 객체를 확인한후 Concurrent Sweep 단계에서는 메모리를 정리하는 작업을 실행하게 된다. Concurrent Sweep 또한 stop-the-world가 진행되지 않는다. 이러한 방식으로 stop-the-world시간을 줄이게 된다. 하지만 이에 단점또한 있다
     메모리와 CPU사용이 높으며 Compaction 단계가 진행되지 않는다 이후 따로 Compaction 단계 실행시 많은시간을 사용해야 할수도 있다.
> 5. **G1 GC** <br>
![](/assets/images/G1_gc.png)
Heap 영역이 4GB이상 사용하는 머신에서 적합하다. Java 9+ 의 default GC으로 선정되었다.
Young 영역과 Old 영역을 나누지 않고 Region이라는 일정한 바둑판 부분으로 나눠서 메모리를 관리한다. 각각의 Region이 Young, Old 역할을 모두 진행한다.
하나의 Region이 차면 GC를 실행한다 이때 CMS 처험 멀티스레드로 Minor GC, Major GC 모두 실행한다 이후 사용중인 객체는 다른 Region으로 이동시킨후 해당 Region 전체를 삭제해버린다 기존 객체만 삭제하던 방식에서 작은 메모리 영역전체를 삭제해버리는 방식으로 변경된것이다. 이는 Compacting또한 이루어 졌다고 할수있다.



<div class="code-example text-delta" markdown="1">
출처 
{: .text-grey-dk-000}

>  https://mirinae312.github.io/develop/2018/06/04/jvm_gc.html
>   https://d2.naver.com/helloworld/1329
</div>
