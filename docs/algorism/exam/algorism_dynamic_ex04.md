---
layout: default
title: 거스름돈 - 동적계획법
nav_order: 4
description: "algorism"
parent: 예제
grand_parent: 알고리즘
permalink: /algorism/exam/dp/4
has_children: true
---

## [프로그래머스 거스름돈](https://programmers.co.kr/learn/courses/30/lessons/12907)
해당 문제는 해당 덧셈을 분해하는 방식으로 진행된다.<br>
아래의 표를 참조해보자.<br>
 ![](/assets/images/moneyChangeImg.PNG)



```java
import java.util.*;
class Solution {
    
    public static int solution(int n, int[] money) {
        Arrays.sort(money);
        long [] table = new long[n+1];

        for( int idx = 0; idx <= n; idx++ ) {
            table[idx] = idx % money[0] == 0 ? 1 : 0;
        }

        for( int idx = 1; idx < money.length; idx++) {
            int curVal = money[idx];
            for( int v = curVal; v < table.length; v++ ) {
                table[v] += table[v-curVal];
            }
        }
        int anwer = (int) table[table.length-1] % 1000000007;
        return anwer;
    }
}
```