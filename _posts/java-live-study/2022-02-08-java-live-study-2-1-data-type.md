---
title: "[Java Live Study] 2-1. 기본형(Primitive Type)과 참조형(Reference Type)"
categories:
  - Java-Study
tags:
  - ☕Java
  - Java-Live-Study
---

> ⚓[백기선 강사님의 live study](https://github.com/whiteship/live-study)에 나온 주제들을 혼자 공부하고 정리하여 작성한 글입니다.⚓

📌 **2주차 목표**: Java의 <u>자료형</u>, 변수 그리고 배열 사용하는 방법 익히기

# [1] 자료형(Data Type)
Java의 자료형은 기본형과 참조형으로 나눌 수 있고, 기본형(8개)을 제외한 나머지는 모두 참조형이라 할 수 있다.

# [2] 기본형(Primitive Type)
- 고정된 크기가 할당된다.
- **스택(Stack)**에 할당된다.
- 변수 안에는 **값 자체**가 저장된다.

```java
int i = 5;
System.out.println(i); 

===== 실행 결과 =====
5
```


## 기본형의 종류
Java 기본형 변수에는 **8가지**가 있다.

|Type|Size|Range|Default|
|:---:|:---:|:---:|:---:|
|byte|1 byte|[-128, 127]|0|
|short|2 bytes|[-32,768, 32,767]|0|
|signed int|4 bytes|[-2<sup>31</sup>, 2<sup>31</sup>-1]|0|
|unsigned int|4 bytes|[0, 2<sup>32</sup>-1]|0|
|signed long|8 bytes|[-2<sup>63</sup>, 2<sup>63</sup>-1]|0L|
|unsigned long|8 bytes|[0, 2<sup>64</sup>-1]|0L|
|float|4 bytes|[1.4E-45, 3.4028235E38]|0.0f|
|double|8 bytes|[4.9E-324, 1.7976931348623157E308]|0.0d|
|boolean|1bit|true / false|false|
|char|2 bytes|['\u0000'(0), '\uffff'(65,535)]|'\u0000'(공백 1칸)|

# [3] 참조형(Reference Type)
- 크기가 정해져 있지 않다.
- **힙(Heap)**에 할당된다.
- 변수 안에는 **메모리의 주소**가 저장된다.

```java
Person p1 = new Person("Alice", 25);
System.out.println(p1);

===== 실행 결과 =====
Person@245b4bdc
```

## 참조형 변수의 메모리 할당
```java
Person p1 = new Person("Alice", 25);
```
를 입력할 때 메모리 구조는 어떻게 되는지 그림으로 표현해보았다.

![참조형 변수의 메모리 할당1]({{site.url}}{{site.baseurl}}/assets/img/java-live-study/reference-variable-memory-1.jpg)
스택에 `p1` 변수가 생성되고, 초기화되지 않았기 때문에 아직 null 값을 가지고 있다.

![참조형 변수의 메모리 할당2]({{site.url}}{{site.baseurl}}/assets/img/java-live-study/reference-variable-memory-2.jpg)
힙에 `Person` 객체가 생성되고 `p1`에는 객체의 주소가 저장된다. (주소는 `1000`이라 가정했다.)

스택에 있는 변수 `p1`이 힙에 있는 `Person` 객체를 **참조**한다고 말하고, 가리킨다고 표현하기도 한다. 그림으로는 화살표로 표현한다.


# 참고
- <https://docs.oracle.com/javase/tutorial/java/nutsandbolts/datatypes.html>
- <http://net-informations.com/faq/general/valuetype-referencetype.htm>