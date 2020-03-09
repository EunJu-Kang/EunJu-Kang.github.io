---
layout: post
title:  "Sorting"
subtitle:   "정렬"
categories: Study
tags: Algo
---


# 대표적인 정렬 방식의 종류

1. 퀵정렬 :가장 빠름
2. 버블정렬
3. 선택정렬 
4. 카운팅정렬 
   : 특수한 상황에서는 가장 빠름/ 정수로 이루어진 데이터에 대해서만 가능(정수의 범위 한정)
5. 삽입정렬
6. 병합정렬



## 1. 퀵 정렬(Quick Sort)
: 퀵정렬은 정렬할 전체 원소에 대해서 정렬을 수행하지 않는다. <br>
먼저 기준 값을 중심으로 전체 원소들을 왼쪽 부분집합과 오른쪽 부분집합으로 분할(Divide)한다. <br>
왼쪽 부분 집합에는 기준 값보다 작은 원소들을 이동시키고, 오른쪽 부분 집합에는 기준 값보다 큰 원소들을 이동시킨다. <br><br>
![quick](/assets/img/Study/algo/quick_sort.gif) 
<br> [출처-위키]

- Partitioning
가장 마지막 원소를 pivot 으로 설정했다고 가정하자. 이 pivot 의 값을 기준으로 좌측에는 작은 값 우측에는 큰 값이 오도록 해야 하는데, 일단 pivot 은 움직이지 말자. 첫번째 원소부터 비교하는데 만약 그 값이 pivot 보다 작다면 그대로 두고 크다면 맨 마지막에서 그 앞의 원소와 자리를 바꿔준다. 즉 pivot value 의 index 가 k 라면 k-1 번째와 바꿔주는 것이다. 이 모든 원소에 대해 실행하고 마지막 과정에서 작은 값들이 채워지는 인덱스를 가리키고 있는 값에 1 을 더한 index 값과 pivot 값을 바꿔준다. 즉, 최종적으로 결정될 pivot 의 인덱스를 i 라고 했을 때, 0 부터 i-1 까지는 pivot 보다 작은 값이 될 것이고 i+1 부터 k 까지는 pivot 값보다 큰 값이 될 것이다.

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
