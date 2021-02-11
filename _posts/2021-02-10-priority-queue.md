---
layout: post
title: "STL: 우선순위 큐"
tags: [STL, 자료구조]
comments: true
---

> STL

* 우선순위를 가진 항목들을 저장하는 큐

우선순위가 높은 데이터가 먼저 나가게 된다.

### 구현방법
1. 배열을 이용한 우선순위 큐 `O(n)`
2. 연결리스트를 이용한 우선순위 큐 `O(n)`
3. 힙(heap)를 이용한 우선순위 큐 `O(logn)`

### 사용법 (c++)
<script src="https://gist.github.com/raeyoungii/cc13f9e8918e8b006b1abe596a404216.js"></script>

### 구조체 비교함수 선언
<script src="https://gist.github.com/raeyoungii/584e9db93ff205f2101321f18a07acf9.js"></script>