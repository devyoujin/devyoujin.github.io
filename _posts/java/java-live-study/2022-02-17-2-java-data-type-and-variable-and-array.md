---
title: "[Java Live Study] 2. 자료형(Data Type), 변수(Variable), 배열(Array)"
categories:
  - Java
tags:
  - ☕Java
  - Java-Live-Study
---

> ⚓[백기선 강사님의 live study](https://github.com/whiteship/live-study)에 나온 주제들을 혼자 공부하고 정리하여 작성한 글입니다.⚓

📌 **2주차 목표**: Java의 자료형, 변수 그리고 배열 사용하는 방법 익히기

# [1] 기본형(Primitive Type)
- Java의 자료형은 기본형과 참조형으로 나눌 수 있고, 기본형(8개)을 제외한 나머지는 모두 참조형이라 할 수 있다.
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

# [2] 참조형(Reference Type)
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

# [3] 리터럴(Literal)
리터럴은 기본형 변수에 값을 대입할 때 **대입연산자(`=`)를 기준으로 우변**에 사용되는 <u>고정 값</u>을 의미한다. 

```java
boolean result = true; // true가 리터럴
char ch = 'a'; // 'a'가 리터럴
int i = 100; // 100이 리터럴
```

## 숫자형 리터럴에 언더스코어(`_`) 사용하기
실생활에서 긴 숫자에 3자리씩 끊어서 콤마(`,`)를 찍듯이 **Java7**부터는 언더스코어(`_`)를 사용하여 **가독성을 높일 수 있다.**

- 숫자형 데이터 타입이면 사용 가능하다.
- 꼭 3자리씩 나누어야 하는 것은 아니다.
- 유효하지 않은 경우
  1. 숫자 리터럴 맨 앞이나 맨 뒤에 사용 불가능
  2. 소숫점 앞뒤에 사용 불가능
  3. 타입을 명시해주는 접미사(예. float에 F, long에 L) 앞에 사용 불가능
  4. 숫자를 String으로 입력하는 경우 사용 불가능

```java
// error: 1번에 해당
long l = _123000L;
int i = 456000_;

// error: 2번에 해당
float f = 12._345f;
float f = 12_.345f;

// error: 3번에 해당
double d = 89.000_d;

// error: 4번에 해당
int i = Integer.parseInt("650_000");

// ok 
int i = 9_____7;
```

# [4] 변수 선언(Variable Declaration)
- 변수 선언은 <u>메모리에 공간을 할당하는 것</u>을 의미한다.
- 선언 방법: `[데이터 타입] [변수명]`

```java
int i;
Person p;
```

# [5] 변수 초기화(Variable Initialization)
- 변수 초기화는 <u>할당한 메모리 공간에 처음으로 유의미한 값을 넣는 것</u>을 말한다.
- **지역변수는 반드시 초기화**해야한다.

```java
i = 100; // i가 위에서처럼 이미 선언한 변수라고 가정하면
p = new Person();
```

## 5-1) 명시적 초기화(Explicit Initialization)
- 명시적 초기화는 <u>선언과 동시에 초기화하는 것</u>을 의미한다.

```java
int i = 100;
Person p = new Person();
```

## 5-2) 생성자(Constructor)로 초기화
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

## 5-3) 초기화 블럭(Initialization Block)으로 초기화
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

# [6] 변수의 유효범위(Scope)와 수명(Lifetime)
- 변수의 유효범위는 <u>변수에 접근가능한 영역적 범위</u>를 의미한다.
- 변수의 수명은 <u>변수가 메모리에 생존해 있는 기간</u>을 의미한다.

|변수 종류|선언 위치|변수 유효범위|생성시기|소멸시기|
|---|---|---|---|---|
|인스턴스 변수(Instance Variable)|클래스 영역|인스턴스 내|인스턴스 생성 시|참조하는 변수 없을 시|
|클래스 변수(Class Variable)|클래스 영역|해당 클래스 내|메모리에 로드 시|프로그램 종료 시|
|지역변수(Local Variable)|메서드 영역|메서드 내|변수 선언 시|해당 메서드 끝날 시|


# [7] 형변환(Type Conversion)
- 형변환은 <u>데이터 타입을 변환시키는 것</u>이다.
- 크게 두 종류로 나눌 수 있는데 다양하게 불리고 있으니 동의어를 알아두는 게 좋을 것 같다.

![형 변환]({{site.url}}{{site.baseurl}}/assets/img/java-live-study/type-conversion.jpg)

## 7-1) Type Promotion
**= Widening Conversion**  
**= Upcasting**  
**= 자동 형변환**
**= 묵시적(Implicit) 타입 변환**

- 표현할 수 있는 값의 범위가 <u>작은 데이터 타입에서 큰 데이터 타입으로의 형 변환</u>
- 값의 손실 없이 변환된다.
- **컴파일러에 의해 자동으로 수행**된다.

## 7-2) Type Casting
**= Narrowing Conversion**
**= Downcasting**
**= 강제 형변환**
**= 명시적(Explicit) 타입 변환**

- 표현할 수 있는 값의 범위가 <u>큰 데이터 타입에서 작은 데이터 타입으로의 형 변환<u>
- **값의 손실이 발생할 수 있다.**
- 괄호 안에 변환되고자 하는 타입을 넣어 변환한다.

```java
int i = 128;
byte b = (byte) i;
```

# [8] 타입 추론(Type Inference)
- 타입 추론은 <u>컴파일러가 추론 알고리즘에 따라 타입을 결정하는 것</u>이다.
- 타입 추론은 Generics를 지원하는 용도로 사용되다가, Lambda를 도입하면서 개선되었다.

**🚧 Generics랑 Lambda 공부하고 돌아와서 타입추론 내용 보충하기 🚧**

## var
- var는 지역 변수로만 선언될 수 있으며, <u>지역 변수의 타입 추론</u>을 위해 사용된다.
- 컴파일러가 변수의 초기값으로 타입을 추론해 명시해두기 때문에 변수를 읽을 때마다 추론을 위한 연산을 하지 않는다.
- **명시적 초기화**(선언과 동시에 초기값을 부여하는 것)를 해야한다.
- **null, 배열, 람다 표현식으로 초기화할 수 없다.**

# [9] 1차 배열(1-Dimensional Array) 선언
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

# [10] 2차 배열(2-Dimensional Array) 선언
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
- <https://docs.oracle.com/javase/tutorial/java/nutsandbolts/datatypes.html>
- <http://net-informations.com/faq/general/valuetype-referencetype.htm>
- <https://docs.oracle.com/javase/specs/jls/se7/html/jls-5.html>
- <https://docs.oracle.com/javase/tutorial/java/generics/genTypeInference.html>
- <https://www.baeldung.com/java-10-local-variable-type-inference>
- <https://www.knowprogram.com/java/multidimensional-array-java/>

