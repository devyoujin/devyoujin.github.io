---
title: "[Java Live Study] 2-2. 형변환(Type Conversion)"
categories:
  - Java-Study
tags:
  - ☕Java
  - Java-Live-Study
---

> ⚓[백기선 강사님의 live study](https://github.com/whiteship/live-study)에 나온 주제들을 혼자 공부하고 정리하여 작성한 글입니다.⚓

📌 **2주차 목표**: Java의 <u>자료형</u>, 변수 그리고 배열 사용하는 방법 익히기

# [1] 형변환(Type Conversion)
- 형변환은 <u>데이터 타입을 변환시키는 것</u>이다.
- 크게 두 종류로 나눌 수 있는데 다양하게 불리고 있으니 동의어를 알아두는 게 좋을 것 같다.

![형 변환]({{site.url}}{{site.baseurl}}/assets/img/java-live-study/type-conversion.jpg)

## 1) Type Promotion
= Widening Conversion  
= Upcasting  
= 자동 형변환  
= 묵시적(Implicit) 타입 변환  

- 표현할 수 있는 값의 범위가 작은 데이터 타입에서 큰 데이터 타입으로의 형 변환
- 값의 손실 없이 변환된다.
- 컴파일러에 의해 자동으로 수행된다.

## 2) Type Casting
= Narrowing Conversion  
= Downcasting  
= 강제 형변환  
= 명시적(Explicit) 타입 변환

- 표현할 수 있는 값의 범위가 큰 데이터 타입에서 작은 데이터 타입으로의 형 변환
- 값의 손실이 발생할 수 있다.
- 괄호 안에 변환되고자 하는 타입을 넣어 변환한다.

```java
int i = 128;
byte b = (byte) i;
```


# 참고
- <https://docs.oracle.com/javase/specs/jls/se7/html/jls-5.html>