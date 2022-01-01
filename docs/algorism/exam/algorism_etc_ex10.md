---
layout: default
title: N개의 최소 공배수 
nav_order: 69
description: "algorism"
parent: 예제
grand_parent: 알고리즘
permalink: /algorism/exam/etc/10
has_children: true
---

## [프로그래머스  N개의 최소 공배수](https://programmers.co.kr/learn/courses/30/lessons/12953)
최소 공배수를 구할때는 기존에는 곱하고 나누어서 구하였으나 손쉬운 방법인 "유클리드 호제법" 이라는 방법을 발견했다.  

> 유클리드 호제법  
> 기존 두수중에 큰수를 작은수로 나머지 연산한후 해당 값을 나우었던수 즉 작은수를 다시 나머지 연산한다. 이렇게 값이 0일 될때 까지 반복한후 0이되었을때의 수를 최대공약수이다. 
  
해당 문제는 위의 방식을 사용한후 이전에서 최대 공배수 구한것처럼 두수를 곱하고 최대공약수로 나누면 해당 최대 공배수가 된다.  
이때, 해당 주어지는 값이 배열이므로 첫번째 두수에서 최대공배수를 구하고 최대공배수와 세번째수의 최대공배수  
쭉 네번째 이렇게 마지막 수까지 최대 공배수를 구하면 해결된다

```java
class Solution {
    public static int solution(int[] arr) {
        int gcf = 0;
        for( int i = 0; i < arr.length; i++ ) {
            gcf = i == 0 ? arr[i] :  gcf * arr[i]  / getGcf(gcf,arr[i]) ;
        }
        return gcf;
    }

    // 최대 공약수 [유클리드 호제법]
    public static int getGcf(int a , int b) {
        int res = 0;
        int gcf = Math.max(a,b);
        int temp = Math.min(a,b);
        while ( temp != 0 ) {
            res = gcf % temp;
            gcf = temp;
            temp = res;
        }

        return gcf;
    }
}
```
