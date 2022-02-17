---
title: "[Java Live Study] 2-6. 1차, 2차 배열(1D, 2D Array Declaration)"
categories:
  - Java-Study
tags:
  - ☕Java
  - Java-Live-Study
---

> ⚓[백기선 강사님의 live study](https://github.com/whiteship/live-study)에 나온 주제들을 혼자 공부하고 정리하여 작성한 글입니다.⚓

📌 **2주차 목표**: Java의 자료형, 변수 그리고 <u>배열</u> 사용하는 방법 익히기

# [1] 1차 배열(1-Dimensional Array)
## 선언
```java
int[] array1D; // valid
int array1D[]; // valid
```
## 초기화
```java
array1D = new int[5]; // {0, 0, 0, 0, 0}
array1D = {1, 2, 3}; 

// 물론 선언과 동시에 초기화도 가능
int[] array1D = new int[5];
```
![1D Array]({{site.url}}{{site.baseurl}}/assets/img/java-live-study/1d-array.jpg)

# [2] 2차 배열(2-Dimensional Array)
## 선언
```java
int[][] array2D; // valid
int[] []array2D; // valid
int[] array2D[]; // valid
int [][]array2D; // valid
int []array2D[]; // valid
int array2D[][]; // valid
```

🔽 동시에 2개의 변수를 선언할 때
```java
int[][] array1, array2; // 둘다 int[][]
int[] array1[], array2; // array1은 int[][], array2는 int[]
```

## 초기화
```java
array2D = new int[2][3]; // { {0, 0, 0}, {0, 0, 0} }
array2D = { {1, 2, 3}, {11, 22, 33} }; 

// 물론 선언과 동시에 초기화도 가능
int[][] array2D = new int[2][3];
```

![2D Array]({{site.url}}{{site.baseurl}}/assets/img/java-live-study/2d-array.jpg)

# 참고
- <https://www.knowprogram.com/java/multidimensional-array-java/>