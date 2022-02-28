---
title: "[Data Structure] Linked List(연결 리스트)"
categories:
  - Data-Structure
tags:
  - 💼Data-Structure
  - ☕Java
---

> 연결 리스트(Linked List) 1️⃣0️⃣1️⃣

<a href="https://github.com/dev-ujin/java-lab/tree/main/linked-list/src/main" class="btn btn--github"><i class="fab fa-github"></i> 구현코드</a> <a href="https://github.com/dev-ujin/java-lab/tree/main/linked-list/src/test" class="btn btn--success">✅ 테스트코드</a>


# [1] Linked List 구조
![Linked List]({{site.url}}{{site.baseurl}}/assets/img/data-structure/linked-list.jpg)

- **node**: 연결 리스트의 각 아이템
  - **data field**: 값을 저장
  - **link field**: 다음 노드를 가리키는 포인터
- **head**: 연결 리스트의 첫 노드
- **tail**: 연결 리스트의 마지막 노드를 종종 `tail`라 칭하기도 하는데, 공식적으로 갖춰야하는 포인터는 아닌 것 같아 그림에는 생략하였다.

# [2] Linked List 종류
![Linked List]({{site.url}}{{site.baseurl}}/assets/img/data-structure/type-of-linked-list.jpg)

- **단일 연결 리스트(Singly Linked List)**
  - 일반적으로 종류를 논하는 것이 아니면 연결 리스트는 단일 연결 리스트를 일컫는다.
- **이중 연결 리스트(Doubly Linked List)**
  - 이전 노드를 가리키는 포인터와 다음 노드를 가리키는 포인터를 가진다.
  - 역방향으로 탐색이 가능하다.
  - 포인터가 2개이기 때문에 단일 연결 리스트에 비해 메모리 공간도 더 요구된다.
- **원형 연결 리스트(Circular Linked List)**
  - 마지막 노드의 포인터가 처음 노드, 즉 `head`를 가리킨다.

# [3] Linked List 특징
> 배열와 비교하여 연결 리스트의 특징을 알아본다.

![Linked List]({{site.url}}{{site.baseurl}}/assets/img/data-structure/array-and-linked-list.jpg)
- 배열은 메모리에 연속적으로 공간이 할당된다. 반면에, 연결 리스트는 공간이 연속적일 필요 없이 메모리에 흩어져 분포되어 있다.

## 장점

###### 동적 크기를 가진다
- 배열은 크기가 고정되어 있지만, 연결리스트는 그렇지 않다.

###### 삽입 및 삭제가 쉽다
- 새로운 원소를 중간에 추가하거나 중간에 위치한 원소를 삭제하려면 뒤에 위치하는 원소들의 위치를 한칸씩 옮겨줘야하는 배열에 비해 연결리스트는 비교적 삽입, 삭제가 쉽다.(자세한 방법은 아래에서 설명한다.)

## 단점

###### 임의 접근이 불가능하다
- 배열은 인덱스를 통해 임의 접근(Random Access)이 가능하지만, 연결 리스트는 `head` 노드에서부터 시작하여 원하는 원소에 접근해야한다.

###### 포인터를 위한 메모리가 필요하다
- 연결 리스트에서는 다음 노드를 가리키는 포인터를 위해 추가적인 메모리 공간이 필요하다.

###### 캐싱에 적합하지 않다
- 배열은 연속적인 공간을 할당하기 때문에 원소들이 인접해 있어 공간적 지역성(Space Locality)을 통해 캐싱을 할 수 있지만, 연결 리스트는 메모리에 분포되어 있기 때문에 캐싱에 적합하지 않다.

# [4] Linked List 메서드
## 노드 삽입
![Linked List]({{site.url}}{{site.baseurl}}/assets/img/data-structure/insertion-in-linked-list.jpg)
- `addFirst(Node node)`: 연결 리스트의 맨 처음에 새로운 노드 추가
- `addLast(Node node)`: 연결 리스트 맨 마지막에 새로운 노드 추가
- `add(Node node, int position)`: 특정 위치에 새로운 노드 추가

## 노드 삭제
![Linked List]({{site.url}}{{site.baseurl}}/assets/img/data-structure/deletion-in-linked-list.jpg)
- `removeFirst()`: 연결 리스트의 맨 처음 노드 삭제
- `removeLast()`: 연결 리스트 맨 마지막 노드 삭제
- `remove(int position)`: 특정 위치에 새로운 노드 삭제

# [5] Linked List 구현
- 노드 삽입, 삭제에 대해 위에서 언급한 메서드를 구현하고 테스트해보았다!😇

🔽 단일 연결 리스트에서의 노드
```java
public class Node {
    public int value;
    public Node next;

    public Node(int value) {
        this.value = value;
        this.next = null;
    }
}
```

🔽 단일 연결 리스트
```java
public class LinkedList {
    private Node head;

    public void addFirst(Node newNode) { ... }
    public void addLast(Node newNode) { ... }
    public void add(Node newNode, int position) { ... }

    public void removeFirst() { ... }
    public void removeLast() { ... }
    public void remove(int position) { ... }

    public int getSize() { ... }
}
```
 
# 참고
- <https://www.geeksforgeeks.org/linked-list-vs-array/?ref=lbp>
- <https://docs.oracle.com/javase/7/docs/api/java/util/LinkedList.html>