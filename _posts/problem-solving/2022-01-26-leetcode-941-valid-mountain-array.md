---
title: "[Leetcode/941] Valid Mountain Array 문제 번역/풀이"
categories:
  - Problem-Solving
tags:
  - Leetcode
  - 🟢Easy
  - Array
  - Java
---

<a href="https://leetcode.com/problems/valid-mountain-array" class="btn btn--primary"> 문제 바로가기</a> <a href="https://github.com/dev-ujin/java-problem-solving" class="btn btn--github"><i class="fab fa-github"></i> 문제 풀이 모음집</a>

# 🔥 문제
정수 배열 `arr`가 주어지고 이 배열이 산 모양 배열일 때 `true`를 반환하여라.

배열이 산 모양 배열이라는 것은 다음의 경우에만 해당된다.
- `arr.length >= 3`
- 아래 조건을 만족하는 i(`0 < i < arr.length - 1`)가 존재한다.
  - arr[0] < arr[1] < ... < arr[i - 1] < arr[i]
  - arr[i] > arr[i + 1] > ... > arr[arr.length - 1]

![](https://assets.leetcode.com/uploads/2019/10/20/hint_valid_mountain_array.png)

배열의 어느 원소를 기점으로 **좌측은 상승**하는 구간, **우측은 하강**하는 구간이어야한다. 상승하는 구간과 하강하는 구간이 **각각 1번씩 반드시 존재**해야한다.
{: .notice--primary}

# 🔥 풀이
## 풀이1: 나의 풀이
index `0`부터 배열끝까지 **한 방향으로** 탐색해나간다. 현재 값이 이전 값보다 크면 상승구간, 작으면 하강구간이 된다. 

중간에 탐색을 멈출 조건은 3가지가 있다. 
1. 평평한 구간(현재 값 = 이전 값)
2. 상승구간 없이 하강구간
3. 이미 하강구간 지났는데 다시 상승구간

이 경우를 제외하고는 배열 끝까지 탐색을 하고, 마지막에 상승구간과 하강구간이 둘 다 존재했을 경우에만 `true`를 반환한다.

```java
class Solution {
    public boolean validMountainArray(int[] arr) {
        if (arr == null || arr.length < 3) {
            return false;
        }
        int previous = arr[0];
        boolean uphill = false;
        boolean downhill = false;
        for (int i = 1 ; i < arr.length ; i++) {
            int current = arr[i];
            if (current == previous || (!uphill && current < previous) || (downhill && current > previous)) {
                return false;
            } else if (!downhill && current > previous) {
                uphill = true;
            } else if (uphill && current < previous) {
                downhill = true;
            }
            previous = current;
        }
        return uphill && downhill;
    }
}
```
```
Runtime: 5ms
Memory Usage: 51.5MB
```

## 풀이2: 다른 사람 풀이
[hi-malik님의 풀이](https://leetcode.com/problems/valid-mountain-array/discuss/1717377/JavaC%2B%2BPython-EASY-to-go-through-solution-and-EXPLANATION)를 가져와봤다.

배열을 탐색할 변수를 두 개 선언한다.
- `left`: index `0`부터 시작해서 `n-1`방향으로 진행한다.
- `right`: index `n-1`부터 시작해서 `0`방향으로 진행한다.

`left`는 상승구간일 경우에 `left++`하고, `right`은 하강구간일 경우에 `right--`한다. 마지막에 결국 `left == right`이면 산의 정상이 딱 하나 존재했다는 의미가 되므로 `true`를 반환한다.

```java
class Solution {
    public boolean validMountainArray(int[] arr) {
        if(arr.length < 3) return false;
        int left = 0;
        int right = arr.length - 1;
        while(left + 1 < arr.length - 1 && arr[left] < arr[left + 1]) left++;
        while(right - 1 > 0 && arr[right] < arr[right - 1]) right--;
        return left == right;
    }
}
```
```
Runtime: 3ms
Memory Usage: 51.7MB
```
