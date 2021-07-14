---
layout: default
title: 여행경로 - DFS
nav_order: 10
description: "algorism"
parent: 예제
grand_parent: 알고리즘
permalink: /algorism/exam/ticket
has_children: true
---

## [프로그래머스 여행경로](https://programmers.co.kr/learn/courses/30/lessons/43164)
해당 문제는 깊이우선 탐색으로 각각의 티켓을 모두 사용 가능한 방법의 노드 탐색중 우선순위를 구하는 문제 이다.<br>
해당 문제 풀이는 티켓을 객체로 두고 구현 하는 방식이다

```java
import java.util.*;


class Solution {
    public static String[] solution(String[][] tickets) {

        boolean[] checkArr =  new boolean[tickets.length];
        Arrays.fill(checkArr,false);
        Ticket.dfs(checkArr,"","ICN",tickets);
        List<String> list =  Ticket.PATH;
        list.sort(
                 (o1, o2) -> o1.compareTo(o2)
        );
        return list.get(0).split(",");
    }




    public static class Ticket {

        public static List<String> PATH = new ArrayList<>();

        public static void dfs( boolean[] checkArr, String path , String currentPort, String[][] tickets) {

            path += path.isEmpty() ? currentPort : ","+currentPort;

            if (Arrays.toString(checkArr).indexOf("false") == -1) {
                PATH.add(path);
                return;
            }

            for(int x =0; x < tickets.length; x++) {
                String pathTemp = new String(path);
                String[] ticket = tickets[x];
                String start = ticket[0];
                String end = ticket[1];
                if (!checkArr[x] && currentPort.equals(start)) {
                    checkArr[x] = true;
                    dfs(checkArr,pathTemp,end,tickets);
                    checkArr[x] = false;
                }
            }
        }

    }
}
```