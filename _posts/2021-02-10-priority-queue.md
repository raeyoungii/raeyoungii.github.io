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
```c++
#include <queue>

// 선언
priority_queue<자료형, Container, 비교함수> pq;
// 선언한 자료형 변수들을 비교함수에 따라 정렬하는 priority_queue를 선언.

priority_queue<자료형> pq;
// 선언한 자료형 변수들을 내림차순에 따라 정렬하는 priority_queue를 선언.

// 추가 및 삭제
pq.push(element) // 원소를 삽입. (비교함수에 따라 내부적으로 정렬됨)

pq.pop() //맨 앞에 있는 원소를 삭제.

// 서칭
pq.top() // 맨 앞에 있는 원소를 반환.

// 기타
pq.empty() // priority_queue가 비어있다면 true 아니면 false를 반환
pq.size() // priority_queue의 크기를 반환
```

### 구조체 비교함수 선언
```c++
struct compare {
    bool operator()(fish a, fish b) {
        if (a.dist == b.dist) {
            if (a.y == b.y) return a.x > b.x;
            return a.y > b.y;
        }
        return a.dist > b.dist;
    }
};

priority_queue<fish, vector<fish>, compare> pq;
// BOJ 16236번: 아기 상어
```