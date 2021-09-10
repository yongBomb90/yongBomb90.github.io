---
layout: default
title: 최고의 집합 - 배열
nav_order: 66
description: "algorism"
parent: 예제
grand_parent: 알고리즘
permalink: /algorism/exam/etc/6
has_children: true
---

## [프로그래머스 최고의 집합](https://programmers.co.kr/learn/courses/30/lessons/12938)

처음에는 어렵게 생각할수 있는 문제이나.
잠시 집중하면 크게 어렵지 않다.
배열을 가장 큰수로만 만들면 된다.
즉, 합이 8 이고 2개의 배열 이라면 나눈 몫에 가까울수록 가장 큰수의 배열이다.
따라서 {4,4} 가 되것다. 만약 딱떨어지지 않는다면 나머지를 공평이 더하면 될뿐...


```java
import java.util.*;

class Solution {
    public  int[] solution(int n, int s) {
        int mid = s/n;
        int[] answer = {-1};

        if ( mid == 0 ) {
            return answer;
        }
        answer = new int[n];
        Arrays.fill(answer, mid);
        int len = s % n;
        for (int x = 0; x < len; x++) {
            answer[answer.length-1-x] += 1;
        }

        return answer;
    }
}
```