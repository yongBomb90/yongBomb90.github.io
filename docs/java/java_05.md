---
layout: default
title: 람다식과 Stream
parent: 자바
nav_order: 5
permalink: /java/005
---

## 람다식과 Stream
{: .fs-9 }

---
## 람다식
- 하나의 식으로 메소드를 표현한다.
- 추상화된 객체를 코드에 선언 하지않고 메소드를 실행 (메소드도 결국 오브젝트).
- 함수지향프로그래밍이 가능하도록 도와준다.
- 간략한 표현이 가능하다.
- 익명함수라고도 한다.

> 표현식 <br>
> (parameters) -> expression <br>
> (parameters) -> { statements; } <br>


#### Functional Interface

| Interface	        | Function Descriptor         | Abstract method |
|:-------------|:------------------|:------|
| Predicate<T>           | (T) -> boolean | boolean test(T t);  |
| Consumer<T> | (T) -> void  | void accept(T t);  |
| Function<T,R>           | (T) -> R    | R apply(T t);   |
| Supplier<T>           | () -> T |  T get();  |
| UnaryOperator<T>          |  (T) -> T |  T apply(T t);  |

```java
// 예제
import java.util.function.Predicate;

public class MainTest {
    public static void main(String[] args) {
        LamdaInterface sample = () -> {
            System.out.println("사용자 람다 인터페이스");
        };
        sample.method();
        Predicate<String> sample2 = (str) -> {
            System.out.println(str);
            return true;
        };
        sample2.test("자바 람다 인터페이스");
    }
}

interface LamdaInterface
{
    public void method();
}
/**********************************************
OUTPUT>>
사용자 람다 인터페이스
자바 람다 인터페이스
***********************************************/
```

---

## Stream
- 기존 컬렉션연산처리는 반복문 (for , while) 등을 사용하였으나 이는 가독성과 불필요한 인스턴스 생성을 초래하였다.이러한 문제점을 해결하는 방식으로 자바에서는 stream을 내놓았다. 
- 스트림은 데이터의 연산흐름을 지원하도록 소스에서 추출한 연속된 오브젝트이다.
- 다수의 쓰레드를 통한 병렬처리가 가능합니다.

```java
        // 생성방식
        Stream<String> generatedStream = Stream.generate( () -> "test").limit(3);
        generatedStream.forEach(System.out::print);
        /****************************
         * OUT PUT >>
         * testtesttest
         *****************************/
        Stream<Integer> iteratedStream = Stream.iterate(10, n -> n + 5).limit(3);
        iteratedStream.forEach(System.out::print);
        /****************************
         * OUT PUT >>
         * 101520
         *****************************/

        List<Integer> list = Arrays.asList(1,2,3,4,5,6,7,8,9,10);
        Stream<Integer> parallelStream = list.parallelStream(); // 병렬 처리 스트림
        parallelStream.forEach( (o1) -> System.out.print(o1+","));
        /****************************
         * OUT PUT >>
         * 7,6,9,10,8,1,2,4,3,5,
         *****************************/

        Stream<String> stringStream = Pattern.compile(",").splitAsStream("하나,둘,셋");
        Stream<String> stringStream2 = Pattern.compile(",").splitAsStream("넷,다섯,여섯");
        Stream<String> concat = Stream.concat(stringStream, stringStream2);
        concat.forEach(System.out::print);
        /****************************
         * OUT PUT >>
         * 하나둘셋넷다섯여섯
         *****************************/


        // 기본 타입 형
        IntStream intStream = IntStream.range(1, 5); // [1, 2, 3, 4]
        LongStream longStream = LongStream.rangeClosed(1, 5); // [1, 2, 3, 4, 5]

        System.out.println(intStream.max().getAsInt()); // 최대값구하기
        System.out.println(intStream.min().getAsInt()); // 최소값구하기
        System.out.println(intStream.average().getAsDouble()); // 평균값구하기
        System.out.println(intStream.sum()); // 총합구하기
        System.out.println(intStream.count()); // 총갯수구하기

        Stream<Integer> filterStream = Stream.iterate(10, n -> n + 1).limit(3);
        filterStream.filter( o1 -> o1 % 2 == 0).forEach(System.out::print);
        /****************************
         * OUT PUT >>
         * 1012
         *****************************/
        Stream<Integer> orgStream = Stream.iterate(10, n -> n + 1).limit(3);
        Stream<String> mappingStream = orgStream.map(o1 -> o1+"mapping/");
        mappingStream.forEach(System.out::print);

        /****************************
         * OUT PUT >>
         * 11mapping/12mapping/
         *****************************/

        String[][] sample = new String[][]{
                {"a", "b"}, {"c", "d"}, {"e", "a"}, {"a", "h"}, {"i", "j"}
        };
        Arrays.stream(sample)
                .flatMap(o1 -> Arrays.stream(o1))
                .filter( o1 -> "a".equals(o1))
                .forEach(System.out::print);
        /****************************
         * OUT PUT >>
         * aaa
         *****************************/
        Stream<Integer> duplStream = Stream.iterate(10, n -> n).limit(3);
        duplStream.distinct().forEach(System.out::println);
        /****************************
         * OUT PUT >>
         * 10
         *****************************/

        Stream<Integer> listStream = Stream.iterate(10, n -> n).limit(3);
        List<Integer> arrList =  listStream.collect(Collectors.toList());
        /****************************
         * OUT PUT >>
         * [10, 10, 10]
         *****************************/
```