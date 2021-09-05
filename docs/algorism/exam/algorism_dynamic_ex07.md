---
layout: default
title: 스킬트리 - 동적계획법
nav_order: 7
description: "algorism"
parent: 예제
grand_parent: 알고리즘
permalink: /algorism/exam/dp/7
has_children: true
---

## [프로그래머스 스킬트리](https://programmers.co.kr/learn/courses/30/lessons/49993)
해당 스킬을 배워야만 다음 스킬을 배울수 있다
이때 주어진 스킬의 가능여부를 판단하게 되는 문제이다 난이도가 어렵지는 않다
스킬의 인덱스가 현재까지의 최대 스킬인덱스보다 적으면 실패이다.
어렵지않으니 코드로 보자.


```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

class Solution {
    public int solution(String skill, String[] skill_trees) {
        
        List<String> possibleSkills = new ArrayList<>();
        StringBuffer stf = new StringBuffer(skill);
        String skillRev = stf.reverse().toString();
        char[] skillRevChar = skillRev.toCharArray();

        for (  String tempSkill : skill_trees) {
            boolean isPossible = true;
            boolean isInSkill = false;
            int idx = 0;
            for ( char sk : skillRevChar) {
                idx ++;
                if (tempSkill.indexOf(sk+"") > -1 ) {
                    String uponSkills = tempSkill.split(sk+"")[0];
                    isInSkill = true;
                    if ( idx < skillRevChar.length && uponSkills.indexOf(skillRevChar[idx]) == -1 ) {
                        isPossible = false;
                    }
                } else  if ( isInSkill && tempSkill.indexOf(sk+"") == -1 ) {
                    isPossible = false;
                }
            }
            if (isPossible) {
                possibleSkills.add(tempSkill);
            }
        }

        
        
        int answer = possibleSkills.size();
        return answer;
    }
}
```