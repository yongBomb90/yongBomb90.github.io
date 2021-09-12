---
layout: default
title: 하샤드 수 - 나머지연산
nav_order: 66
description: "algorism"
parent: 예제
grand_parent: 알고리즘
permalink: /algorism/exam/etc/7
has_children: true
---

## [프로그래머스 최고의 집합](https://programmers.co.kr/learn/courses/30/lessons/12947)

머리 풀기 좋은 코딩문제..
난이도는 가장 쉽다. 기존적은 나눗셈연산이 되는지에 대한 문제..
자존감 떨어졌을때 풀어보자...


```java
class Solution {
    public boolean solution(int x) {
        String[] arr = String.valueOf(x).split("");
        int sum = 0;
        for ( String c: arr) {
            sum += Integer.parseInt(c);
        }
        return x % sum == 0;
    }
}
```