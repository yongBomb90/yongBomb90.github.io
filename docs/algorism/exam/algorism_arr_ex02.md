---
layout: default
title: 풍선터뜨리기 - 순열알고리즘
nav_order: 51
description: "algorism"
parent: 예제
grand_parent: 알고리즘
permalink: /algorism/exam/arr/2
has_children: true
---

## [프로그래머스 풍선터뜨리기](https://programmers.co.kr/learn/courses/30/lessons/68646)
해당 문제는 순열 알고리즘을 통하여 인데스를 점차 줄여가며 구하는 방식이다<br>
문제의 핵심은 해당 풍선 중심으로 왼쪽 오른쪽 모두 자기보다 낮은수가 있다면 해당 풍선은 터지지 않는다. <br>
이는 왼쪽이든 오른쪽이든 본인이 가장 낮은 숫자일경우 해당 풍선은 카운트된다.<br>
```java
import java.util.*;

class Solution {
    public int solution(int[] a) {
         int leftMin = Integer.MAX_VALUE;
        int rightMin = Integer.MAX_VALUE;
        HashSet<Integer> nums = new HashSet<>();

        for ( int idx = 0; idx < a.length; idx++ ) {
            leftMin = Math.min(a[idx],leftMin);
            rightMin = Math.min(a[a.length - (1 +  idx)],rightMin);
            nums.add(leftMin);
            nums.add(rightMin);
        }

        return nums.size();
    }
}
```