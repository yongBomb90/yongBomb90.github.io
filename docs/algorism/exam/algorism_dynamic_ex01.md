---
layout: default
title: 멀리뛰기 - 동적계획법
nav_order: 2
description: "algorism"
parent: 예제
grand_parent: 알고리즘
permalink: /algorism/exam/dp/2
has_children: true
---

## [프로그래머스 멀리뛰기](https://programmers.co.kr/learn/courses/30/lessons/12914)
해당 문제는 동적계획법으로 첫번째 행렬부터 문제에 맞는 계산을 진행하여 마지막 결과에서 가장 큰 수를 구하는 방식의 알고리즘을 이용하여 계산한다.

```java
class Solution {
    public long solution(int n) {
        return fibo(n);
    }

     public static long fibo(int n ) {
        int o1 = 1;
        int o2 = 1;
        if ( n == 1  ) {
            return o2;
        }
        for (int idx = 1; idx < n; idx ++ ) {
            int t = (o1+o2) % 1234567;
            o1 = o2;
            o2 = t;

        }
        return o2;
    }
}
```