---
layout: default
title: 땅따먹기 - 동적계획법
nav_order: 1
description: "algorism"
parent: 예제
grand_parent: 알고리즘
permalink: /algorism/exam/dp/1
has_children: true
---

## [프로그래머스 땅따먹기](https://programmers.co.kr/learn/courses/30/lessons/12913)
해당 문제는 동적계획법으로 첫번째 행렬부터 문제에 맞는 계산을 진행하여 마지막 결과에서 가장 큰 수를 구하는 방식의 알고리즘을 이용하여 계산한다.

```java
import java.util.Arrays;

class Solution {
    int solution(int[][] land) {
         int[] pastArr = {0,0,0,0};
        for ( int[] arr : land) {
            int idx = 0;
            for ( int t : arr) {
                int[] x = pastArr.clone();
                x[idx] = 0;
                Arrays.sort(x);
                arr[idx] += x[x.length-1];
                idx++;
            }
            pastArr = arr;
        }
        Arrays.sort(pastArr);
        int answer = pastArr[pastArr.length-1];

        return answer;
    }


}
```