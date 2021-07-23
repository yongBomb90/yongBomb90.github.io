---
layout: default
title: 2 x n 타일링 - 동적계획법
nav_order: 3
description: "algorism"
parent: 예제
grand_parent: 알고리즘
permalink: /algorism/exam/dp/3
has_children: true
---

## [프로그래머스 2 x n 타일링](https://programmers.co.kr/learn/courses/30/lessons/12900)
해당 문제는 동적계획법으로 첫번째 행렬부터 문제에 맞는 계산을 진행하여 마지막 결과에서 가장 큰 수를 구하는 방식의 알고리즘을 이용하여 계산한다.
기존 땅따먹기와 같은 방식으로 진행된다.
```java
class Solution {
    
    public int solution(int n) {
        return fibo(n);
    }
    
    public static int fibo(int n ) {
        int o1 = 1;
        int o2 = 1;
        if ( n == 1  ) {
            return o2;
        }
        for (int idx = 1; idx < n; idx ++ ) {
            int t = (o1+o2) % 1000000007;
            o1 = o2;
            o2 = t;

        }
        return o2;
    }
}
```