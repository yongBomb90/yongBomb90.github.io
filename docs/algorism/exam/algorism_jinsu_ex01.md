---
layout: default
title: 124 나라 - 진수변환
nav_order: 50
description: "algorism"
parent: 예제
grand_parent: 알고리즘
permalink: /algorism/exam/jinsu/01
has_children: true
---

## [프로그래머스 124나라](https://programmers.co.kr/learn/courses/30/lessons/12899)
해당 문제는 진수변환에 따른 처리로 해결이 가능하다 이때 주의 해야 할점은
나머지가 0일겨우 4로 치한한후 1을 빼줘야 한다 124로 인해 3도 4로 표현한다 그로인해 하나씩 제거 한다.

```java
class Solution {
    public String solution(int n) {
        
        
        StringBuilder stb = new StringBuilder();
        int rem ;

        while ( n > 0 ) {
            rem = n % 3;
            n = n / 3;
            if (rem == 0 ) {
                n -= 1;
                rem = 4;
            }
            stb.append(rem);
        }

        return stb.reverse().toString();
    }
}
```