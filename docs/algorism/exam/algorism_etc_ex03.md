---
layout: default
title: 문자열압축 - 문자치환
nav_order: 63
description: "algorism"
parent: 예제
grand_parent: 알고리즘
permalink: /algorism/exam/etc/3
has_children: true
---

## [프로그래머스 문자열압축](https://programmers.co.kr/learn/courses/30/lessons/60057)
해당 문제는 문자의 배열을 압축하여 나태내주는 문제이다.
가장 작은 단위의 글자부터 압축하여 하나씩 늘려가는 방식으로 문제 풀이하였다.
어렵지 않아 코드로 직접보고 해결 가능하다.


```java
class Solution {
    public int solution(String s) {
        int min = s.length();

    for (int i =1; i<=min; i++ ) {
        String temp = "";
        String t = "";
        int cnt = 1;
        StringBuffer stb = new StringBuffer();
        for ( int j=0; j<s.length(); j+=i) {
            t = s.substring(j,j+i < s.length() ? j+i : s.length());
            if (temp.equals("")) {
                temp = t;
                continue;
            }
            if ( temp.equals(t)){
                cnt++;
                continue;
            }
            if ( cnt > 1) {
                temp = cnt+temp;
            }
            stb.append(temp);
            temp = t;
            cnt = 1;
        }
        if ( cnt > 1) {
            temp = cnt+temp;
        }
        stb.append(temp);
        min = Math.min(min,stb.length());
    }
        return min;
    }
}
```