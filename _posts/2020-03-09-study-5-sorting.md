---
layout: post
title:  "Sorting"
subtitle:   "정렬"
categories: Study
tags: Algo
---


# 대표적인 정렬 방식의 종류

```
1. 퀵정렬
2. 버블정렬
3. 선택정렬 
4. 카운팅정렬 
5. 삽입정렬
6. 병합정렬
```
<br>
<br>

## 1. 퀵 정렬(Quick Sort)
: 퀵정렬은 정렬할 전체 원소에 대해서 정렬을 수행하지 않는다. <br>
먼저 기준 값을 중심으로 전체 원소들을 왼쪽 부분집합과 오른쪽 부분집합으로 분할(Divide)한다. <br>
왼쪽 부분 집합에는 기준 값보다 작은 원소들을 이동시키고, 오른쪽 부분 집합에는 기준 값보다 큰 원소들을 이동시킨다. <br><br>
![quick](/assets/img/Study/algo/quick_sort.gif) 
 [출처-위키]

#### 시간복잡도
Quick Sort 로 오름차순 정렬을 한다고 하자. 그렇다면 Worst Case 는 partition 과정에서 pivot value 가 항상 배열 내에서 가장 작은 값 또는 가장 큰 값으로 설정되었을 때이다. 매 partition 마다 unbalanced partition이 이뤄지고 이렇게 partition 이 되면 비교 횟수는 원소 n 개에 대해서 n 번, (n-1)번, (n-2)번 … 이 되므로 시간 복잡도는 O(n^2) 이 된다.

#### 소스코드
~~~ java
import java.util.Arrays;
public class QuickSort {
       public static void main(String[] args) {
              int[] arr = { 5, 1, 9, 6, 7, 8 };
              quickSort(arr, 0, arr.length - 1);
              System.out.println(Arrays.toString(arr));
       }
       static void quickSort(int[] arr, int start, int end) {
              if (start >= end)
                     return;
              int pivot = parition(arr, start, end); //피봇 정하기
              quickSort(arr, start, pivot - 1);
              quickSort(arr, pivot + 1, end);
       }
       static int parition(int[] arr, int p, int r) {
              int x = arr[r];
              int i = p - 1;
              for (int j = p; j < r; j++) {
              // i와 j가 같이가다가 큰애가 있으면 i는  멈춤 j는 가다가 작은애 만나면 멈춤. 둘이 바꿈
                     if (arr[j] <= x) {
                           i++;
                           swap(arr, i, j);
                     }
              }
              swap(arr, i+1 , r);
              return i+1 ;
       }
       static void swap(int[] arr, int a, int b) {
              int tmp = arr[a];
              arr[a] = arr[b];
              arr[b] = tmp;
       }
}
~~~
