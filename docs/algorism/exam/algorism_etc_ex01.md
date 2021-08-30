---
layout: default
title: 키패드누르기 - 좌표
nav_order: 60
description: "algorism"
parent: 예제
grand_parent: 알고리즘
permalink: /algorism/exam/etc/1
has_children: true
---

## [프로그래머스 키패드누르기](https://programmers.co.kr/learn/courses/30/lessons/67256)
해당 문제는 위치를 좌표라 생각하고 각각 거리를 구해서 처리하는 방식이다.
피타고라스와 동적계산을 하는 형식으로 풀었다

```java
class Solution {
    public String solution(int[] numbers, String hand) {
        String Lposition = "*";
        String Rposition = "#";
        hand = hand.equals("right") ? "R" : "L";
        int[] lpos = getLocation(Lposition);
        int[] rpos = getLocation(Rposition);
        String touch = "";

        int inx = 0;
        for ( int num : numbers) {
            inx++;
            int[] pos = getLocation(String.valueOf(num));
            String touchPad = "";
            double ldix = getDistance(lpos,pos);
            double Rdix = getDistance(rpos,pos);
            if ( pos[0] == 0 ) {
                touchPad = "L";
            } else if ( pos[0] == 2 ) {
                touchPad =  "R";
            } else {
                if ( ldix == Rdix ) {
                    touchPad = hand;
                } else if ( ldix < Rdix ) {
                    touchPad = "L";
                } else {
                    touchPad = "R";
                }
            }
            if ( touchPad == "L") {
                lpos = pos;
                Lposition = String.valueOf(num);
            } else  {
                rpos = pos;
                Rposition = String.valueOf(num);
            }
            touch += touchPad;

        }
        return touch;
    }
    
    public static int[] getLocation( String s ) {
        int n = s.replaceAll("[1-9]","").equals("") ?   Integer.parseInt(s)  : s.equals("*") ? 10 : s.equals("#") ? 12 : 11;
        int x = n % 3 == 0 ? 2 : (n % 3 ) -1;
        int y = ( 12 - n ) / 3 ;
        int[] res = {x,y};
        return  res;
    }

    public static double getDistance( int[] pos1 , int[] pos2 ) {
        double dis = Math.pow( (pos1[0] - pos2[0]) , 2) + Math.pow( (pos1[1] - pos2[1]) , 2);
        return  Math.ceil(Math.sqrt(dis)) ;
    }

}
```