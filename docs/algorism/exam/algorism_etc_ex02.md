---
layout: default
title: 괄호변환 - 문자치환
nav_order: 61
description: "algorism"
parent: 예제
grand_parent: 알고리즘
permalink: /algorism/exam/etc/2
has_children: true
---

## [프로그래머스 괄호변환](https://programmers.co.kr/learn/courses/30/lessons/60058)
해당 문제는 문자의 () 에 맞게 괄호를 변경시키는 방식이다.
문제 풀이는 이는 꼭 짝수가 맞아야 한다. 어렵지 않는 방식이라 코드만 보면 이해가 가능하다

```java
class Solution {
    public String solution(String p) {
       if ( p == null || "".equals(p.trim())) {
            return "";
        }
        String u = "" , v = "" , answer = "";
        int idx = 0 , length = p.length() ;
        int startIdx = 0 , endIdx = 0;

        for ( idx = 0 ; idx < length  ; idx ++) {
            String tmp = p.substring(idx,idx+1);
            u += tmp;
            if ( "(".equals(tmp)) {
                startIdx ++;
            } else {
                endIdx ++;
            }
            if ( startIdx == endIdx ) {
                break;
            }
        }

        if (idx != length - 1 ) {
            v = p.substring(idx+1,length);
        }
        if ( !u.startsWith("(") ) {
             u = u.substring(1,u.length()-1);
             u = u.replaceAll("\\(","1");
             u = u.replaceAll("\\)","2");
             u = u.replaceAll("1",")");
             u = u.replaceAll("2","(");
             answer = "(" + solution(v) + ")" + u;
         } else {
             answer = u + solution(v);
         }

        return answer;
    }
}
```