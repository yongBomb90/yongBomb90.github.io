---
layout: default
title: 타겟넘버 - DFS/BFS
nav_order: 70
description: "algorism"
parent: 예제
grand_parent: 알고리즘
permalink: /algorism/exam/graph/1
has_children: true
---

## [프로그래머스 타겟넘버](https://programmers.co.kr/learn/courses/30/lessons/43165)

해당 문제는 가장 단순한 깊이 우선 탐색방식이다.
깊이우선 탐색방식을 이해하였다면 어렵지않게 풀수있다.

```java
import java.util.ArrayList;
import java.util.List;


class Solution {
    public int solution(int[] numbers, int target) {
       List<Integer> list = new ArrayList<>();
       dfs(0,numbers,0,list);
        
       return list.stream().filter(o1 -> o1 == target).toArray().length;
    }
    public static void dfs(int sum ,  int[] numbers , int idx , List<Integer> list) {
        if ( idx == numbers.length) {
            list.add(sum);
           return ;
        }

        dfs(sum+numbers[idx],numbers,idx+1,list);
        dfs(sum-numbers[idx],numbers,idx+1,list);
        return;

    }
}
```