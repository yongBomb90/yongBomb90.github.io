---
layout: default
title: 줄서는법 - 순열알고리즘
nav_order: 50
description: "algorism"
parent: 예제
grand_parent: 알고리즘
permalink: /algorism/exam/arr/1
has_children: true
---

## [프로그래머스 줄서는법](https://programmers.co.kr/learn/courses/30/lessons/12936)
해당 문제는 순열 알고리즘을 통하여 인데스를 점차 줄여가며 구하는 방식이다

```java
import java.util.*;
import java.util.stream.IntStream;

class Solution {
    
    public static long CNT = 0;
    
    public int[] solution(int n, long k) {
        
        List<Integer> nums = new ArrayList<>();
        for( int x = 0 ; x < n; x++) {
            nums.add(x+1);
        }

        CNT = k;
        int[] answer = new int[n];
        int idx = 0;
        while ( !( nums.isEmpty())) {
            long fac =  getFactory(n - (idx + 1));
            for (int s =0; s < nums.size();s++ ) {
                if ( 0 >= CNT - ( (s+1) * fac)) {
                    answer[idx] = nums.get(s);
                    CNT -= fac * (s);
                    nums.remove(s);
                    break;
                }
            }
            idx ++;
        }
        return answer;
    }
    public static long getFactory(long x) {
        long temp = 1;
        for ( long idx = 1; idx <= x; idx++) {
            temp *=  idx;
        }
        return temp;
    }
}
```