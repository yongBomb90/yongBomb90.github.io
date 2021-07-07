---
layout: default
title: 동적계획법 - 땅따먹기
parent: 알고리즘
nav_order: 22
permalink: /algorism/ex/dp/1
---
## 동적계획법?
{: .fs-9 }
입력의 크기가 작은 문제들을 해결한후, 부분문제들의 해를 활용하여 보다 큰 문제를 해결한다. 이는 상향식 접근법으로 가장 최하위의 해답을 구한후 이를 저장하여 상위문제를 풀어가는 방식이라고 할수있다.

---

## [프로그래머스 땅따먹기](https://programmers.co.kr/learn/courses/30/lessons/12913)
해당 문제는 동적계획법으로 첫번째 행렬부터 문제에 맞는 계산을 진행하여 마지막 결과에서 가장 큰 수를 구하는 방식의 알고리즘을 이용하여 계산한다.

```java
import java.util.Arrays;

class Solution {
    int solution(int[][] land) {
         int[] pastArr = {0,0,0,0};
        for ( int[] arr : land) {
            int idx = 0;
            for ( int t : arr) {
                int[] x = pastArr.clone();
                x[idx] = 0;
                Arrays.sort(x);
                arr[idx] += x[x.length-1];
                idx++;
            }
            pastArr = arr;
        }
        Arrays.sort(pastArr);
        int answer = pastArr[pastArr.length-1];

        return answer;
    }


}
```