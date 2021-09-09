---
layout: default
title: 주식가격 - 스택/큐
nav_order: 65
description: "algorism"
parent: 예제
grand_parent: 알고리즘
permalink: /algorism/exam/etc/5
has_children: true
---

## [프로그래머스 주식가격](https://programmers.co.kr/learn/courses/30/lessons/42584)
해당 문제는 가장 기본적인 스택 큐 방식이다.
O(n^2) 방식이라.. 쓸수는 없을것 같지만 일단 가장 기본적인 방식의 풀이법을 기록해본다.


```java
class Solution {
    public int[] solution(int[] prices) {
        int[] answer = new int[prices.length];
        for ( int i = 0; i < prices.length; i ++ ) {
            int cur = prices[i];
            int cnt = 0;
            for ( int j = i+1; j < prices.length; j ++ ) {
                cnt ++;
                if ( cur > prices[j]) {
                    break;
                }
            }
            answer[i] = cnt;
        }
        return answer;
    }
}
```