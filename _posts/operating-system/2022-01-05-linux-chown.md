---
title: "[Linux] 소유자, 소유그룹 변경하기(chown)"
categories:
  - Operating-System
tags:
  - 🐧Linux
---

> 

# [1] 문법
```terminal
[root@system]$ chown [-옵션] 소유자[:소유그룹] 파일 경로
```

## 옵션 
`-R`(recursive): 모든 하위 디렉토리와 파일에 적용.

## 예시
- test.txt 파일의 소유자를 user로, 소유그룹을 admin으로 변경.
```terminal
[root@system]$ chown user:admin test.txt
```
- test_d 디렉토리 아래의 모든 파일과 디렉토리에 대해서 소유자를 user로 변경.
```terminal
[root@system]$ chown -R user test_d
```