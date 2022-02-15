---
title: "[Java Live Study] 2-5. 변수(Variable)"
categories:
  - Java-Study
tags:
  - ☕Java
  - Java-Live-Study
---

> ⚓[백기선 강사님의 live study](https://github.com/whiteship/live-study)에 나온 주제들을 혼자 공부하고 정리하여 작성한 글입니다.⚓

📌 **2주차 목표**: Java의 자료형, <u>변수</u> 그리고 배열 사용하는 방법 익히기

# [1] 변수 선언(Variable Declaration)
- 변수 선언은 <u>메모리에 공간을 할당하는 것</u>을 의미한다.
- 선언 방법: `[데이터 타입] [변수명]`

```java
int i;
Person p;
```

# [2] 변수 초기화(Variable Initialization)
- 변수 초기화는 <u>할당한 메모리 공간에 처음으로 유의미한 값을 넣는 것</u>을 말한다.
- **지역변수는 반드시 초기화**해야한다.

```java
i = 100; // i가 위에서처럼 이미 선언한 변수라고 가정하면
p = new Person();
```

## 1) 명시적 초기화(Explicit Initialization)
- 명시적 초기화는 <u>선언과 동시에 초기화하는 것</u>을 의미한다.

```java
int i = 100;
Person p = new Person();
```

## 2) 생성자(Constructor)로 초기화
```java
public class Person {
  private String name;
  private int age;

  Person() {}

  Person(String name, int age) {
    this.name = name;
    this.age = age;
  }
}
```

```java
Person p = new Person();
Person p = new Person("Alice", 20);
```

## 3) 초기화 블럭(Initialization Block)으로 초기화
### (1) 클래스 초기화 블럭
- <u>클래스 변수(static 변수)의 초기화</u>에 사용된다.
- **메모리에 로드될 때 딱 한 번**만 수행된다.

### (2) 인스턴스 초기화 블럭
- <u>인스턴스 변수(non-static 변수)의 초기화</u>에 사용된다.
- **인스턴스를 생성할 때마다** 수행된다.
- **생성자보다 먼저 수행**된다.
- 여러 개의 생성자에 공통되는 부분을 묶어서 처리하기에 유용하다.

```java
public class Person{
  static {} // 클래스 초기화 블럭
  {} // 인스턴스 초기화 블럭
}
```

🔽 Person 예제
```java
public class Person{
  // 인스턴스 변수
  String name;
  int age;
  boolean dead;

  // 클래스 변수
  static int total;

  // 클래스 초기화 블럭
  static{
    total = 0;
  }

  // 인스턴스 초기화 블럭
  {
    dead = false;
    total++;
  }

  Person() {
    age = 1;
    //dead = false; // 코드 중복 => 인스턴트 초기화 블럭으로
    //total++; 
  }

  Person(String name, int age) {
    this.name = name;
    this.age = age;
    //dead = false; // 코드 중복 => 인스턴트 초기화 블럭으로
    //total++; 
  }
}
```

# [3] Variable Scope(유효범위) & Lifetime(수명)
- 변수의 유효범위는 <u>변수에 접근가능한 영역적 범위</u>를 의미한다.
- 변수의 수명은 <u>변수가 메모리에 생존해 있는 기간</u>을 의미한다.

|변수 종류|선언 위치|변수 유효범위|생성시기|소멸시기|
|---|---|---|---|---|
|인스턴스 변수(Instance Variable)|클래스 영역|인스턴스 내|인스턴스 생성 시|참조하는 변수 없을 시|
|클래스 변수(Class Variable)|클래스 영역|해당 클래스 내|메모리에 로드 시|프로그램 종료 시|
|지역변수(Local Variable)|메서드 영역|메서드 내|변수 선언 시|해당 메서드 끝날 시|