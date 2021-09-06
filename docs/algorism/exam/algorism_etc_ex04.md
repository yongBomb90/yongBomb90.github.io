---
layout: default
title: 기능개발 - 스택/큐
nav_order: 64
description: "algorism"
parent: 예제
grand_parent: 알고리즘
permalink: /algorism/exam/etc/4
has_children: true
---

## [프로그래머스 기능개발](https://programmers.co.kr/learn/courses/30/lessons/42586)
해당 문제는 가장 기본적인 스택 큐 방식이다.
코드를 보고 이해하자


```java
import java.util.*;

class Solution {
    public int[] solution(int[] progresses, int[] speeds) {
         double[] doneDays = new double[progresses.length];

        for ( int i = 0; i < progresses.length; i++ ) {
            doneDays[i] = Math.ceil( (100 - progresses[i]) / (double)speeds[i] );
        }

        List<Integer> deployDays = new ArrayList<>();

        double cur = doneDays[0];
        int cnt = 0;

        for ( int i = 0; i < doneDays.length; i++ ) {
             if ( cur < doneDays[i]) {
                 deployDays.add(cnt);
                 cur = doneDays[i];
                 cnt = 0;
             }
             cnt++;
        }
        if ( cnt != 0 ) {
            deployDays.add(cnt);    
        }
        
        int[] answer =  new int[deployDays.size()];
        for ( int i = 0; i < deployDays.size(); i++ ) {
            answer[i] = deployDays.get(i);
        }
        
        return answer;
    }
}
```