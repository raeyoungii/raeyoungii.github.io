---
layout: post
title: "Educational Codeforces: Round 104 (Div.2)"
category: Codeforces
tags: [알고리즘, Codeforces]
comments: true
mathjax: true
---

> Codeforces

# A. Arena

$n$ heroes fight against each other in the Arena. Initially, the $i$-th hero has level $a_i$.

Each minute, a fight between two different heroes occurs. These heroes can be chosen arbitrarily (it's even possible that it is the same two heroes that were fighting during the last minute).

When two heroes of equal levels fight, nobody wins the fight. When two heroes of different levels fight, the one with the higher level wins, and his level increases by $1$.

The winner of the tournament is the first hero that wins in at least $100^{500}$ fights (note that it's possible that the tournament lasts forever if no hero wins this number of fights, then there is no winner). A possible winner is a hero such that there exists a sequence of fights that this hero becomes the winner of the tournament.

Calculate the number of possible winners among $n$ heroes.

### Input
The first line contains one integer $t$ $(1≤t≤500)$ — the number of test cases.

Each test case consists of two lines. The first line contains one integer $n$ $(2≤n≤100)$ — the number of heroes. The second line contains $n$ integers $a_1,a_2,…,a_n$ $(1≤a_i≤100)$, where $a_i$ is the initial level of the $i$-th hero.

### Output
For each test case, print one integer — the number of possible winners among the given $n$ heroes.

## 풀이
배열의 최솟값만 아니면 우승 가능성이 있으므로 배열의 최솟값보다 큰 영웅의 수를 세주면 된다.

### 코드
```c++
#include <bits/stdc++.h>

using namespace std;
typedef long long ll;

void solve() {
    int n; cin >> n;
    vector<int> v(n);
    for (int i = 0; i < n; i++) {
        cin >> v[i];
    }
    int mn = *min_element(v.begin(), v.end());
    int cnt = 0;
    for (int i = 0; i < n; i++) {
        if (mn < v[i]) cnt++;
    }
    cout << cnt << "\n";

}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    int t; cin >> t;
    while(t--) solve();
    return 0;
}

```

# B. Cat Cycle

Suppose you are living with two cats: A and B. There are $n$ napping spots where both cats usually sleep.

Your cats like to sleep and also like all these spots, so they change napping spot each hour cyclically:

* Cat A changes its napping place in order: $n,n−1,n−2,…,3,2,1,n,n−1,…$ In other words, at the first hour it's on the spot $n$ and then goes in decreasing order cyclically;
* Cat B changes its napping place in order: $1,2,3,…,n−1,n,1,2,…$ In other words, at the first hour it's on the spot 1 and then goes in increasing order cyclically. 

The cat B is much younger, so they have a strict hierarchy: A and B don't lie together. In other words, if both cats'd like to go in spot $x$ then the A takes this place and B moves to the next place in its order (if $x < n$ then to $x+1$, but if $x=n$ then to 1). Cat B follows his order, so **it won't return to the skipped spot $x$ after A frees it, but will move to the spot $x+2$ and so on.**

Calculate, where cat B will be at hour $k$?

### Input
The first line contains a single integer t $(1≤t≤10^4)$ — the number of test cases.

The first and only line of each test case contains two integers $n$ and $k$ $(2≤n≤10^9; 1≤k≤10^9)$ — the number of spots and hour $k$.

### Output
For each test case, print one integer — the index of the spot where cat B will sleep at hour $k$.

## 풀이
> 나머지를 출력할 때 1 ~ k 까지 출력하고 싶다면
```c++
if (n % k == 0) s = k;
else s = n % k;
```
위 코드보다는 아래의 코드로 간편하게 출력할 수 있다.
```c++
s = (n - 1) % k + 1; 
```
나눗셈 올림(ceil)을 출력하고 싶다면
```c++
if (n % k == 0) s = n / k;
else s = n / k + 1;
```
위 코드보다는 아래의 코드로 간편하게 출력할 수 있다.
```c++
s = (n + k - 1) / k;
```

* n이 짝수일 때 고양이 B의 k번째 위치는 항상 n % k (이때, 1 부터 k까지)이다.

* n이 홀수일 때 고양이 B의 위치는 일정한 규칙을 갖는다.<br>
```
ex) n이 7일때 아래의 배열이 계속 반복된다.
[1, 2, 3,   5, 6, 7]
[2, 3, 4,   6, 7, 1]
[3, 4, 5,   7, 1, 2]
[4, 5, 6]
```
반복되는 수가 $n * \frac{n - 1}{2}$개 이므로 k를 k % ($n * \frac{n - 1}{2}$) (이때, 1 부터 $n * \frac{n - 1}{2}$까지)로 바꾼다.<br>
원하는 k번째 수는 다음과 같이 구할 수 있다.<br>
    * 행: ceil($\frac{k}{n - 1}$)$-1$<br>
    * 열: $k$ % $(n - 1)$ (이때, 1 부터 n - 1까지)<br>

    이때 k번째 숫자는 (열 $≤ \frac{n - 1}{2}$) 이면 $ans$ = (행 + 열) % $n$,<br>
    아니면 $ans$ = (행 + 열) % $n + 1$ 이다.

### 코드
```c++
#include <bits/stdc++.h>

using namespace std;
typedef long long ll;

void solve() {
    ll n, k; cin >> n >> k;
    if (n % 2 == 0) {
        cout << (k - 1) % n + 1 << "\n";
    } else {
        ll div, mod;
        k = (k - 1) % (n * (n / 2)) + 1;
        div = (k + n - 2) / (n - 1) - 1;
        mod = (k - 1) % (n - 1) + 1;
        if (mod <= n / 2) cout << (div + mod) % n << "\n";
        else cout << (div + mod) % n + 1 << "\n";
    }
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    int t; cin >> t;
    while(t--) solve();
    return 0;
}

```

<https://codeforces.com/contest/1487>{:target="_blank"}
