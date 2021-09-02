---
layout: default
title: 보행자천국 - 동적계획법
nav_order: 6
description: "algorism"
parent: 예제
grand_parent: 알고리즘
permalink: /algorism/exam/dp/6
has_children: true
---

## [프로그래머스 보행자천국](https://programmers.co.kr/learn/courses/30/lessons/1832)
처음 문제 접근을 그래프 방식의 넓이 우선 탐색을 진행하였으나 그건 멍청했다
이문제는 각각의 경우의 수를 교차점의 갯수 만큼 하나씩 구하는 방식으로 진행된다.



```java
class Solution {
     int MOD = 20170805;
	 public static int solution(int m, int n, int[][] cityMap) {

        long[][] step = new long[m][n];
        step[0][0] = 1;
        for ( int i = 0; i < n; i++ ) {
            step[0][i] = cityMap[0][i] != 1 ? 1 : 0;
        }
        for ( int i = 1; i < m; i++ ) {
            for ( int z = 0; z < n; z++ ) {
                long temp = z != 0 ? step[i-1][z-1] : 0;
                long num = 0;
                if ( cityMap[i][z] != 1 || ( i == m-1 && z == n-1)) {
                    long top  =  cityMap[i-1][z] == 2 ? (step[i-1][z] - temp) < 0 ? 0 : (step[i-1][z] - temp) : step[i-1][z];
                    long left =  z == 0 ? 0 : cityMap[i][z-1] == 2 ? (step[i][z-1] - temp) < 0 ? 0 : (step[i][z-1] - temp)   : step[i][z-1];
                    num = top + left;
                }
                step[i][z] = num % 20170805;
            }
        }
        int answer = (int)((step[m-1][n-1]) % 20170805);
        return answer;
    }
}
```