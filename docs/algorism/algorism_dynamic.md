---
layout: default
title: 동적계획법 - 피보나치수열 구하기
parent: 알고리즘
nav_order: 21
permalink: /algorism/ex/dp
---
## 동적계획법?
{: .fs-9 }
입력의 크기가 작은 문제들을 해결한후, 부분문제들의 해를 활용하여 보다 큰 문제를 해결한다. 이는 상향식 접근법으로 가장 최하위의 해답을 구한후 이를 저장하여 상위문제를 풀어가는 방식이라고 할수있다.

---

## 피보나치수열 구하기
 피보나치 수는 F(0) = 0, F(1) = 1일 때, 1 이상의 n에 대하여 F(n) = F(n-1) + F(n-2) 가 적용되는 수 입니다. <br>
 예를들어
   - F(2) = F(0) + F(1) = 0 + 1 = 1
   - F(3) = F(1) + F(2) = 1 + 1 = 2
   - F(4) = F(2) + F(3) = 1 + 2 = 3
   - F(5) = F(3) + F(4) = 2 + 3 = 5
 와 같이 이어집니다.

```java
    public static Integer fibo(int num) {
        if ( num < 0) {
            return null;
        }
        int currentNum = 1;
        int pastNum = 0;
        Integer sum = num == 1 ? currentNum : 0 ;
        for ( int idx =0; idx <= num; idx++) {
            if ( idx < 2 ) {
                continue;
            }
            sum = currentNum + pastNum;
            pastNum = currentNum;
            currentNum = sum;
        }

        return sum;
    }
```
[프로그래머스 예제 문제...](https://programmers.co.kr/learn/courses/30/lessons/12945?language=java) <br>
```java
    // 예제 문제 풀이...    
    public int solution(int n) {
        return fibo(n, 1234567);
    }

    public static Integer fibo(int num , Integer deno) {
        if ( num < 0) {
            return null;
        }
        int currentNum = 1;
        int pastNum = 0;
        deno = deno == null ? 1 : deno;

        Integer sum = num == 1 ? currentNum : 0 ;
        for ( int idx =0; idx <= num; idx++) {
            if ( idx < 2 ) {
                continue;
            }
            // (( 4 * 1234567) + 3 ) + (( 4 * 1234567) + 4 ) = (( 8 * 1234567) + 7 ) 
            sum = (currentNum + pastNum) % deno;
            pastNum = currentNum;
            currentNum = sum;
        }

        return sum;
    }
```