---
layout: default
title: 없는숫자더하기
nav_order: 68
description: "algorism"
parent: 예제
grand_parent: 알고리즘
permalink: /algorism/exam/etc/9
has_children: true
---

## [프로그래머스 없는숫자더하기](https://programmers.co.kr/learn/courses/30/lessons/86051)
알고리즘 생각이 줄어들어서 다시 풀어보기위해 가장 쉬운 문제를 골랐다.
Stream 을 사용하고 있다면 손쉽게 풀수있는 문제 이다.


```java
import java.util.*;
import java.util.stream.IntStream;

class Solution {
    public static int solution(int[] numbers) {
        int[] resultArr = Arrays.stream(numbers).distinct().toArray();
        IntStream intStream = IntStream.range(1, 10);
        return intStream.filter(o1 -> !Arrays.stream(resultArr).anyMatch(a ->  a == o1)).sum();
    }
}
```
