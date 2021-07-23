---
layout: default
title: 하노이의탑 - 재귀함수
nav_order: 20
description: "algorism"
parent: 예제
grand_parent: 알고리즘
permalink: /algorism/exam/recursive/5
has_children: true
---

## [프로그래머스 하노이의탑](https://programmers.co.kr/learn/courses/30/lessons/12946?language=java)
해당 문제는 재귀함수을 통해 해결된다.
문제해결의 답은 n 은 n-1 의 탑을 중간에 옮긴후 n 을 3번째에 옮기구 n-1 탑을 옮기는 방식이다.
옮길때는 중간의 잠시 거쳐야할 거점이 필요하다 그로인해 이는 출발점 타겟 거점 이렇게 3개의 지점으로
탑을 움직이는 방식은 같으나 저 세지점이 계속 달라진다는 것만 다르다. 그로 인해 아래와 같이 구현이 가능하다


```java
import java.util.*;

class Solution {
    
    public static List<int[]> LIST = new ArrayList<>();
    
    
    public  int[][] solution(int n) {
        hanoi(1,3,2,n);
        int[][] answer = new int[LIST.size()][2];
        for ( int idx = 0; idx < LIST.size(); idx++) {
            answer[idx] = LIST.get(idx);
        }
        return answer;
    }

    public static void hanoi( int current, int target, int stopover, int size) {
        int[] move = {current,target};
        if ( size == 1 ) {
            LIST.add(move);
        } else {
            hanoi(current,stopover,target,size - 1);
            LIST.add(move);
            hanoi(stopover,target,current,size - 1);
        }
    }
}
```