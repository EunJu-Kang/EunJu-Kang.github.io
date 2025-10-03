---
layout: post
title:  "H Index"
subtitle:   ""
categories: Algorithm
tags: PROMS
---

## 프로그래머스 [H-Index]
[문제보기](https://school.programmers.co.kr/learn/courses/30/lessons/42747)  
![Alt text](/../assets/img/programmers/HIndex.png)

### 소스코드
~~~ java
import java.util.Arrays;

class Solution {
  public static int solution(int[] citations) {
       Arrays.sort(citations);

        int n = citations.length;

        int hIndex = 0;
        for (int i = n - 1; i >= 0; i--) {
            int thesisCnt = n - i;
            int citation = citations[i];

            if (thesisCnt <= citation) {
                hIndex = thesisCnt;
            } else {
                break;
            }
        }

        return hIndex;
    }
}
~~~
