---
layout: default
title: 모의고사 - 완전탐색
nav_order: 68
description: "algorism"
parent: 예제
grand_parent: 알고리즘
permalink: /algorism/exam/etc/8
has_children: true
---

## [프로그래머스 모의고사](https://programmers.co.kr/learn/courses/30/lessons/42840)
포스팅을 할까말까 고민한 문제..
자바의 기초문제이다.


```java
import java.util.*;

class Solution {
    public final static int[] FIRST = {1,2,3,4,5};
    public final static int[] SECOND = {2,1,2,3,2,4,2,5};
    public final static int[] THIRD = {3,3,1,1,2,2,4,4,5,5};

    
    public int[] solution(int[] answers) {
        int[] daps = {0,0,0};
        for ( int idx = 0; idx < answers.length; idx++) {
            int dap = answers[idx];
            daps[0] = FIRST[idx%FIRST.length] == dap ?  daps[0] + 1 : daps[0] ;
            daps[1] = SECOND[idx%SECOND.length] == dap ?  daps[1] + 1 : daps[1] ;
            daps[2] = THIRD[idx%THIRD.length] == dap ?  daps[2] + 1 : daps[2] ;
        }
        int[] temp = daps.clone();
        Arrays.sort(temp);
        int max = temp[2];
        List<Integer> list = new ArrayList<>();
        int idx = 0;

        for ( int dap :daps) {
            if (max == dap ) {
                list.add(idx + 1);
            }
            idx ++;
        }
        return list.stream().mapToInt(i->i.intValue()).toArray();
    }
}
```