---
title: "[Java Live Study] 4. 제어문(Control Statements)"
categories:
  - Java-Live-Study
tags:
  - ☕Java
---

> ⚓[백기선 강사님의 live study](https://github.com/whiteship/live-study)에 나온 주제들을 혼자 공부하고 정리하여 작성한 글입니다.⚓

📌 **4주차 목표**: Java 제공하는 제어문을 학습하기

<a href="https://github.com/dev-ujin/java-lab/tree/main/java-live-study/control-statements" class="btn btn--github"><i class="fab fa-github"></i> 소스코드</a>

# [0] 개요
프로그램은 일반적으로 위에서부터 아래 방향으로 실행되는데, 제어 흐름문을 사용하면 실행 흐름을 분리하여 조건에 따라 특정 코드 블록을 실행하도록 할 수 있다.

3가지로 나눌 수 있다.
- 의사 결정문(Decision-Making Statements): `if-then`, `if-then-else`, `switch`
- 반복문(Looping Statements): `for`, `while`, `do-while`
- 분기문(Branch Statements): `break`, `continue`, `return`

# [1] 의사 결정문(Decision-Making Statements)
## if-then
- `if`절의 결과가 `true`이면 `then`절을 실행하고, `false`면 `then`절을 건너 뛴다.
- `then`절에 구문이 1개면 중괄호(`{...}`)를 생략할 수 있다.

```java
if (isDeleted) // if clause
    // then clause
    System.out.println("This is already deleted!");
```

## if-then-else
```java
if (isDeleted) // if clause
    // then clause
    System.out.println("This is already deleted!");
else {
    deleted = true;
    System.out.println("Successfully deleted!");
}
```

## if-then-elseif-else
```java
int score = 70;
char grade;

if (score >= 90) {
    grade = 'A';
} else if (score >= 75) {
    grade = 'B';
} else if (score >= 60) {
    grade = 'C';
} else {
    grade = 'F';
}
```

## switch
###### 사용가능한 자료형
- 기본형(Primitive Type)중에서 `byte`, `short`, `char`, `int`
- 래퍼 클래스(Wrapper Class)중에서 `Byte`, `Short`, `Character`, `Integer`
- Enum Types
- String (Java 7 이상)

- `case value:`: 각각의 경우를 나열
- `default:`: 어느 case에도 속하지 않는 경우 (선택사항)
- `break`: 이후의 `case`문을 실행하지 않고 `switch`문 종료

🔽 올바르게 작성된 switch문
```java
int dayNum = 2;
String dayString = "";
switch (dayNum) {
    case 1:
        dayString = "Monday";
        break;
    case 2:
        dayString = "Tuesday";
        break;
    case 3:
        dayString = "Wednesday";
        break;
    case 4:
        dayString = "Thursday";
        break;
    case 5:
        dayString = "Friday";
        break;
    case 6:
        dayString = "Friday";
        break;
    case 7:
        dayString = "Friday";
        break;
    default:
        System.out.println("Invalid number for day");
}
    System.out.println(dayString); // "Tuesday"
```

🔽 `break`를 생략하면...
- `break`를 만날 때까지 하위 `case`문을 거쳐 `default`문까지 모두 실행된다.

```java
int dayNum = 2;
String dayString = "";
switch (dayNum) {
    case 1:
        dayString = "Monday";
    case 2:
        dayString = "Tuesday";
    case 3:
        dayString = "Wednesday";
    case 4:
        dayString = "Thursday";
        break;
    case 5:
        dayString = "Friday";
        break;
}
    System.out.println(dayString); // "Thursday"
```

🔽 여러 `case` 묶어 표현하기
```java
int dayNum = 6;
String dayString = "";
switch (dayNum) {
    case 1: case 2: case 3: case 4: case 5:
        dayString = "Weekday";
        break;
    case 6: case 7:
        dayString = "Weekend";
        break;
    default:
        System.out.println("Invalid number for day");
}
    System.out.println(dayString); // "Weekend"
```
# [2] 반복문(Looping Statements)
## while
- `while`문의 조건이 `true`이면 반복 수행한다. 

```java
int count = 1;
while (count < 3) {
    System.out.println("The count: " + count);
    count++;
}
```
```terminal
The count: 1
The count: 2
```

## do-while
- `do`문을 먼저 실행한 후, `while`문의 조건이 `true`이면 다시 `do`문을 반복 수행한다. 
- **`do`문이 최소 1회 실행되는 것을 보장한다.**

```java
int count = 4;

// while문
System.out.println("========== while ==========");
while (count < 3) {
    System.out.println("The count: " + count);
    count++;
}

// do-while문
System.out.println("========== do-while ==========");
do {
    System.out.println("The count: " + count);
    count++;
} while (count < 3)
```
```terminal
========== while ==========
========== do-while ==========
The count: 4
```
## for
```java
for (initialization ; termination ; increment) {
    statements
}
```
- `initialization`은 최초 1회만 실행된다.
- `termination`가 `true`면 반복 수행한다.
- `increment`는 매 라운드 후에 실행된다. 

```java
for (int count = 3 ; count > 0 ; count--) {
    System.out.println("The count: " + count);
}
```
🔽 각각의 요소는 문법적으로 생략이 가능하다.
```java
int count = 3;
for (;;) {
    if (count > 0) {
        System.out.println("The count: " + count);
        count--;
    } else {
        break;
    }
}
```

```terminal
The count: 3
The count: 2
The count: 1
```
## Enhanced for
- `Collections`나 `배열([])`에 사용할 수 있다.

```java
int[] nums = {1, 2, 3};
for (int num : nums) {
    System.out.println("The number: " + num);
}
```
```terminal
The number: 1
The number: 2
The number: 3
```

## forEach
- Java 8 이상부터 사용 가능하다.
- `Collections`에 사용 가능하다.

```java
List<Integer> list = Arrays.asList(1, 2, 3);
list.forEach(n -> System.out.println("The number: " + n));
```
```terminal
The number: 1
The number: 2
The number: 3
```
# [3] 분기문(Branching Statements)
## break
- 반복문을 종료할 때 사용한다.
- `unlabeled break`와 `labeled break`가 있다.

예제로 비교해보면 이해가 쉽다.

### unlabeled break
- `break`를 하면 가장 안쪽에 위치한 `switch`, `for`, `while`, `do-while`를 종료한다.

```java
label:
    ... // statements
    break label;
```

```java
int[][] nums = { { 32, 87},
                 { 12, 1076},
                 { 622, 127 } };
int searchfor = 12;
int i;
int j = 0;
boolean isfound = false;

for (i = 0; i < nums.length; i++) {
    for (j = 0; j < nums[i].length; j++) {
        if (nums[i][j] == searchfor) {
            isfound = true;
            break;
        }
    }
}

if (isfound) {
    System.out.println("Found " + searchfor + " at " + i + ", " + j);
} else {
    System.out.println(searchfor + " not in the array");
}
```
```terminal
Found 12 at 3, 2
```
- 안쪽 `for`문만 종료되기 때문에 찾고자하는 값을 찾은 이후 `i = 1`에 대한 탐색은 건너뛰지만 `i = 2`는 실행된다. (예제에서 보면 32 -> 87 -> 12 -> 622 -> 127에 대해서 탐색함)

### labeled break
- `break label_name`를 하면 바깥쪽에 위치한 실행문을 종료한다.

```java
int[][] nums = { { 32, 87},
                 { 12, 1076},
                 { 622, 127 } };
int searchfor = 12;
int i;
int j = 0;
boolean isFound = false;

search:
    for (i = 0; i < nums.length; i++) {
        for (j = 0; j < nums[i].length; j++) {
            if (nums[i][j] == searchfor) {
                isFound = true;
                break search;
            }
        }
    }

if (isFound) {
    System.out.println("Found " + searchfor + " at " + i + ", " + j);
} else {
    System.out.println(searchfor + " not in the array");
}
```
```terminal
Found 12 at 1, 0
```
- `(1, 0)`에서 찾고자하는 값을 찾은 후 `for`문이 바로 종료되는 것을 확인할 수 있다.

## continue
- 반복문에서 현재 라운드를 넘길(skip) 때 사용한다.
- `unlabeled continue`와 `labeled continue`가 있다.

🔽 [oracle - labeled continue 예제](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/branch.html)

```java
String string = "search super substring";
String searchTerm = "sub";
boolean isFound = false;

int max = string.length() - searchTerm.length();

search:
    for (int i = 0; i <= max; i++) {
        int n = searchTerm.length();
        int j = i;
        int k = 0;
        while (n-- != 0) { // searchTerm의 길이 만큼 순회하면서
            if (string.charAt(j++) != searchTerm.charAt(k++)) { // searchTerm의 문자 하나하나씩 비교하여 다르면
                continue search; // 다음 i로 이동
            }
        }
        isFound = true;
        break search; // 바깥쪽 for문 종료
    }
    System.out.println(isFound ? "Found it" : "Didn't find it");
```

## return
- 값을 반환하거나

```java
return i;
```

- 계산 값을 반환하거나

```java
return i++;
```

- 아무것도 반환하지 않을 수 있다.(메서드 리턴타입이 `void`일 때 사용)

```java
return;
```

**🚧과제 추가중🚧**

# 참고
- <https://docs.oracle.com/javase/tutorial/java/nutsandbolts/flow.html>