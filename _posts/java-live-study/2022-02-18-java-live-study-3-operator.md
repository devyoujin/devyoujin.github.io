---
title: "[Java Live Study] 3. 연산자(Operator)"
categories:
  - Java-Live-Study
tags:
  - ☕Java
---

> ⚓[백기선 강사님의 live study](https://github.com/whiteship/live-study)에 나온 주제들을 혼자 공부하고 정리하여 작성한 글입니다.⚓

📌 **3주차 목표**: Java의 다양한 연산자 학습하기

<a href="https://github.com/dev-ujin/java-lab/tree/main/operator" class="btn btn--github"><i class="fab fa-github"></i> 소스코드</a>

# [0] 용어
- 연산자: 특정한 연산을 수행하고 결과를 반환하는 기호이다.
- 피연산자: 연산의 대상
- 단항연산자: 피연산자 1개를 필요로 하는 연산자
- 이상연산자: 피연산자 2개를 필요로 하는 연산자
- 삼항연산자: 피연산자 3개를 필요로 하는 연산자

# [1] 산술 연산자(Arithmetic Operator)

|연산자|의미|
|---|---|
|`+`|더하기(Addition) 혹은 문자열 String concat|
|`-`|빼기(Subtraction)|
|`*`|곱하기(Multiplication)|
|`/`|나누기(Division)|
|`%`|나머지(Remainder)|

```java
public class ArithmeticOperator {
    private int i1 = 10;
    private int i2 = 50;
    private int i3 = 100;

    @Test
    public void numericAdditionOperator() {
        Assertions.assertEquals(60, i1 + i2);
    }

    @Test
    public void stringAdditionOperator() {
        Assertions.assertEquals("HelloWorld", "Hello" + "World");
        Assertions.assertEquals("HelloWorld1050", "Hello" + "World" + i1 + i2); // HelloWorld60이 아님에 주의!
    }

    @Test
    public void subtractionOperator() {
        Assertions.assertEquals(40, i2 - i1);
        Assertions.assertEquals(-50, i2 - i3);
    }

    @Test
    public void multiplyOperator() {
        Assertions.assertEquals(500, i1 * i2);
    }

    @Test
    public void divisionOperator() {
        Assertions.assertEquals(5, i2 / i1);
        Assertions.assertEquals(14, 100 / 7);
    }

    @Test
    public void remainderOperator() {
        Assertions.assertEquals(0, i2 % i1);
        Assertions.assertEquals(2, 100 % 7);
    }
}

```

# [2] 비트 연산자(Bitwise Operator)

|연산자|의미|
|---|---|
|`&`|AND|
|`|`|(Inclusive) OR|
|`^`|Exclusive OR|

|x|y|x&y|x\|y|x^y|
|:---:|:---:|:---:|:---:|:---:|
|0|0|0|0|0|
|0|1|0|1|1|
|1|0|0|1|1|
|1|1|0|1|0|

```java
public class BitwiseOperator {
    private int i1 = 14; // 1110(2)
    private int i2 = 3; // 0011(2)

    @Test
    public void andOperator() {
        Assertions.assertEquals(2, i1 & i2); // 8 = 0010(2)
    }

    @Test
    public void inclusiveOrOperator() {
        Assertions.assertEquals(15, i1 | i2); // 13 = 1111(2)
    }

    @Test
    public void exclusiveOrOperator() {
        Assertions.assertEquals(13, i1 ^ i2); // 5 = 1101(2)
    }
    
}
```

## 쉬프트 연산자(Bit Shift Operator)
🚧Unsigned Shift Operator🚧

# [3] 관계 연산자(Relational Operator)

|연산자|역할|
|---|---|
|x `==` y|x와 y가 같다|
|x `!=` y|x와 y가 같지 않다|
|x `>` y|x가 y보다 크다|
|x `>=` y|x가 y보다 크거나 같다|
|x `<` y|x가 y보다 작다|
|x `<=` y|x가 y보다 작거나 같다|

```java
public class RelationalOperator {
    int i1 = 1;
    int i2 = 10;

    @Test
    public void relationalOperator() {
        Assertions.assertFalse(i1 == i2);
        Assertions.assertTrue(i1 != i2);
        Assertions.assertFalse(i1 > i2 | i1 >= i2);
        Assertions.assertTrue(i1 < i2);
        Assertions.assertTrue(i1 <= i2);
    }
}
```

# [4] 논리 연산자(Logical Operator)
- Conditional Operator이라고도 한다.

|연산자|의미|
|---|---|
|`&&`|AND|
|`||`|OR|

🚧 비트 연산자의 **AND(`&`)** 혹은 **OR(`|`)**와 혼동하지 않도록 주의해야한다.
{: .notice--warning}

# [5] instanceof
- 타입 비교 연산자(Type Comparison Operator)로 <u>객체가 특정 타입인지 확인</u>할 수 있다..
- `true` 혹은 `false`를 반환한다.

```java
object_reference instanceof type
```

```java
public abstract class Creature { ... }
public abstract class Plant extends { ... }
public class Cactus extends Plant { ... }

public class TypeComparisonOperator {
    @Test
    public void typeComparisonOperator() {
        Cactus c = new Cactus(12, true);
        Assertions.assertTrue(c instanceof Cactus);
        Assertions.assertTrue(c instanceof Plant);
        Assertions.assertTrue(c instanceof Creature);
    }
}
```

# [6] 대입 연산자(Assignment Operator)
- 대입 연산자 `=`는 <u>피연산자에 값을 대입</u>할 때 사용한다.
- 다른 연산자와 결합하여 사용할 수도 있다.

```java
variable = value
```

🔽 다른 연산자와 결합된 형태

|연산자|의미|
|---|---|
|x `+=` y|x = x + y|
|x `-=` y|x = x - y|
|x `*=` y|x = x * y|
|x `/=` y|x = x / y|
|x `%=` y|x = x % y|
|x `&=` y|x = x & y|
|x `^=` y|x = x ^ y|
|x `|=` y|x = x \| y|
|x `<<=` y|x = x << y|
|x `>>=` y|x = x >> y|
|x `>>>=` y|x = x >>> y|

# [7] 화살표 연산자(Arrow Operator)
- 화살표 연산자 `->`는 Java 8에서 람다 표현식이 도입되면서부터 사용되기 시작했다.

```java
parameter -> expression                    // valid
(parameter1, parameter2) -> expression     // valid
(parameter1), parameter2) -> {code block}  // valid
```

```java
List<Integer> numList = new ArrayList<>();
numList.add(1);
numList.add(2);
numList.add(3);
numList.forEach((n) -> System.out.println(n));

---------- 실행 결과 ----------
1
2
3
```

# [8] 삼항 연산자(Ternary Operator)
- 삼항 연산자 `? :`는 경우에 따라 if문을 대신하여 간략하게 사용할 수 있다.

```java
conditional ? true_expression : false_expression 
```

```java
int score = 20;
Boolean passed = score >= 60 ? true : false;
System.out.println(passed);

// if문으로 표현하면
int score = 20;
Boolean passed;
if (score >= 60) {
    passed = true;
} else {
    passed = false;
}
```

# [9] 연산자 우선순위

|우선순위|연산자 종류|예시|
|---|---|---|
|1|후위 연산자|`v++`, `v--`|
|2|단항 연산자|`++v`, `--v`, `+v`, `-v`, `~`, `!`|
|3|산술 연산자(곱셈관련)|`*`, `/`, `%` |
|4|산술 연산자(덧셈관련)|`+`, `-`|
|5|관계 연산자(부등호)|`<`, `>`, `<=`, `>=`, `instanceof` |
|6|관계 연산자(등호)|`==`, `!=`|
|7|비트 연산자(AND)|`&`|
|8|비트 연산자(XOR)|`^`|
|9|비트 연산자(OR)|`|`|
|10|논리 연산자(AND)|`&&`|
|11|논리 연산자(OR)|`||`|
|12|삼항 연산자|`? :`|
|13|대입 연산자|`=`, `+=`, `-=`, `*=`, `/=`, `%=`, `&=`, `^=`, `!=`, `<<=`, `>>=`, `>>>=`|

# [10] Switch 연산자
- Switch 연산자는 기존에 존재하던 switch 조건문과 문법이 유사하며, Java 12부터 사용이 가능하다.
- `:` 대신 `->`를 사용할 수 있다. (statement가 여러개면 `{}`와 같이 사용한다.)
- `break`가 필요 없다.
- `yield`를 사용해 값을 대입한다.

🔽 switch 조건문
```java
int option = 1;
String language;
switch(option) {
    case 1:
        language = "KO";
        break;
    case 2:
        language = "EN";
        break;
    case 3:
        language = "DE";
        break;
    default:
        language = "N/A";
        break;
}
```

🔽 switch 연산자
```java
int option = 1;
String language = switch(option) {
    case 1:
        yield "KO";
    case 2:
        yield "EN";
    case 3:
        yield "DE";
}

// 혹은 이렇게도 표현 가능
String language = switch(option) {
    case 1 -> { yield "KO"; }
    case 2 -> { yield "EN"; }
    case 3 -> { yield "DE"; }
}
```

# 참고
- <https://docs.oracle.com/javase/tutorial/java/nutsandbolts/operators.html>
- <https://docs.oracle.com/javase/tutorial/java/nutsandbolts/switch.html>
- <https://docs.oracle.com/en/java/javase/13/language/switch-expressions.html>