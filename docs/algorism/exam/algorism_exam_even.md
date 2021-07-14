---
layout: default
title: 입국검사 - 이분검색
nav_order: 30
description: "algorism"
parent: 예제
grand_parent: 알고리즘
permalink: /algorism/exam/even/01
has_children: true
---

## [프로그래머스 입국검사](https://programmers.co.kr/learn/courses/30/lessons/43238)
해당 문제는 이분검색을 통한 최대걸리는 시간을 토대로 시간별로 처리 가능한 입국심사수를 구해 점차 줄여나가는 방식이다.<br>
코드에서 가장 중요점은 형변환을 주요로 봐야한다.

```java
import java.util.*;

class Solution {
    public long solution(int n, int[] times) {
        Arrays.sort(times);
        long start = 0;
        long end = (long)times[times.length-1] * n;
        long mid = 0;
        long cnt = 0;
        long answer = Long.MAX_VALUE;
        while ( start <= end ) {
            mid = (start + end) / 2;
            cnt = getCnt(times,mid,n );
            if ( cnt >= n ) {
                answer = Math.min(answer,mid);
                end = mid - 1;
            } else {
                start = mid + 1;
            }
        }
        
        return answer;
    }
    public static long getCnt(int[] times, long time, long num) {
        long cnt = 0;
        for ( int t : times) {
           cnt += time / t;
           if (cnt >= num) {
               return cnt;
           }
        }
        return cnt;
    }
}
```