---
layout: default
title: 정수삼각형 - 동적계획법
nav_order: 5
description: "algorism"
parent: 예제
grand_parent: 알고리즘
permalink: /algorism/exam/dp/5
has_children: true
---

## [프로그래머스 정수삼각형](https://programmers.co.kr/learn/courses/30/lessons/43105)
해당 문제는 동적계획법을 통해 해결된다.
이전의 해당 값으로 이동될시의 최대값을 구해 계속 더해간다.


```java
import java.util.Arrays;
class Solution {
    public int solution(int[][] triangle) {
        for ( int i = 1; i < triangle.length; i++ ) {
            for ( int x = 0; x < triangle[i].length; x++ ) {
                if ( x == 0 ) {
                    triangle[i][x] += triangle[i-1][x];
                } else if ( x == triangle[i-1].length) {
                    triangle[i][x] += triangle[i-1][x-1];
                } else {
                    triangle[i][x] += Math.max(triangle[i-1][x-1],triangle[i-1][x]) ;
                }
            }
        }
        int[] last = triangle[triangle.length-1];
        Arrays.sort(last);
        return last[last.length-1];
    }
}
```