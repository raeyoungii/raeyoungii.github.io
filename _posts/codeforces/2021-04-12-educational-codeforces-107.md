---
layout: post
title: "Educational Codeforces: Round 107 (Div. 2)"
category: Codeforces
tags: [알고리즘, Codeforces]
comments: true
mathjax: true
---

> Codeforces

# A. Review Site

You are an upcoming movie director, and you have just released your first movie. You have also launched a simple review site with two buttons to press — upvote and downvote.

However, the site is not so simple on the inside. There are two servers, each with its separate counts for the upvotes and the downvotes.

$𝑛$ reviewers enter the site one by one. Each reviewer is one of the following types:

* type 1: a reviewer has watched the movie, and they like it — they press the upvote button;
* type 2: a reviewer has watched the movie, and they dislike it — they press the downvote button;
* type 3: a reviewer hasn't watched the movie — they look at the current number of upvotes and downvotes of the movie on the server they are in and decide what button to press. If there are more downvotes than upvotes, then a reviewer downvotes the movie. Otherwise, they upvote the movie.
Each reviewer votes on the movie exactly once.

Since you have two servers, you can actually manipulate the votes so that your movie gets as many upvotes as possible. When a reviewer enters a site, you know their type, and you can send them either to the first server or to the second one.

What is the maximum total number of upvotes you can gather over both servers if you decide which server to send each reviewer to?

### Input
The first line contains a single integer $𝑡$ $(1≤𝑡≤10^4)$ — the number of testcases.

Then the descriptions of $𝑡$ testcases follow.

The first line of each testcase contains a single integer $𝑛$ $(1≤𝑛≤50)$ — the number of reviewers.

The second line of each testcase contains $𝑛$ integers $𝑟_1,𝑟_2,…,𝑟_𝑛$ $(1≤𝑟_𝑖≤3)$ — the types of the reviewers in the same order they enter the site.

### Output
For each testcase print a single integer — the maximum total number of upvotes you can gather over both servers if you decide which server to send each reviewer to.


## 풀이


### 코드
```c++
#include <bits/stdc++.h>

using namespace std;
typedef long long ll;
const char nl = '\n';

int R[51];

void solve() {
    int n; cin >> n;
    for (int i = 0; i < n; i++) cin >> R[i];
    int cnt = 0;
    for (int i = 0; i < n; i++) {
        if (R[i] == 1 || R[i] == 3) cnt++;
    }
    cout << cnt << nl;
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    int t; cin >> t;
    while(t--) solve();
    return 0;
}

```

# B. GCD Length

You are given three integers $𝑎, 𝑏$ and $𝑐$.

Find two positive integers $𝑥$ and $𝑦$ $(𝑥>0, 𝑦>0)$ such that:

* the decimal representation of $𝑥$ without leading zeroes consists of $𝑎$ digits;
* the decimal representation of $𝑦$ without leading zeroes consists of $𝑏$ digits;
* the decimal representation of $𝑔𝑐𝑑(𝑥,𝑦)$ without leading zeroes consists of $𝑐$ digits.

$𝑔𝑐𝑑(𝑥,𝑦)$ denotes the [greatest common divisor (GCD)](https://en.wikipedia.org/wiki/Greatest_common_divisor){:target="_blank"} of integers $𝑥$ and $𝑦$.

Output $𝑥$ and $𝑦$. If there are multiple answers, output any of them.

### Input
The first line contains a single integer $𝑡$ $(1≤𝑡≤285)$ — the number of testcases.

Each of the next $𝑡$ lines contains three integers $𝑎, 𝑏$ and $𝑐$ $(1≤𝑎,𝑏≤9, 1≤𝑐≤𝑚𝑖𝑛(𝑎,𝑏))$ — the required lengths of the numbers.

It can be shown that the answer exists for all testcases under the given constraints.

Additional constraint on the input: all testcases are different.

### Output
For each testcase print two positive integers — $𝑥$ and $𝑦$ $(𝑥>0, 𝑦>0)$ such that

* the decimal representation of $𝑥$ without leading zeroes consists of $𝑎$ digits;
* the decimal representation of $𝑦$ without leading zeroes consists of $𝑏$ digits;
* the decimal representation of $𝑔𝑐𝑑(𝑥,𝑦)$ without leading zeroes consists of $𝑐$ digits.

## 풀이


### 코드
```c++
#include <bits/stdc++.h>

using namespace std;
typedef long long ll;
const char nl = '\n';

void solve() {
    int a, b, c; cin >> a >> b >> c;
    int x = 1, y = 1, z = 1;
    for (int i = 0; i < a - 1; i++) x *= 10;
    for (int i = 0; i < b - 1; i++) y *= 10;
    for (int i = 0; i < c - 1; i++) z *= 10;
    cout << x << " " << (y + z) << nl;
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    int t; cin >> t;
    while(t--) solve();
    return 0;
}

```

# C. Yet Another Card Deck

You have a card deck of $𝑛$ cards, numbered from top to bottom, i. e. the top card has index $1$ and bottom card — index $𝑛$. Each card has its color: the $𝑖$-th card has color $𝑎_𝑖$.

You should process $𝑞$ queries. The $𝑗$-th query is described by integer $𝑡_𝑗$. For each query you should:

* find the highest card in the deck with color $𝑡_𝑗$, i. e. the card with minimum index;
* print the position of the card you found;
* take the card and place it on top of the deck.

### Input
The first line contains two integers $𝑛$ and $𝑞$ $(2≤𝑛≤3⋅10^5; 1≤𝑞≤3⋅10^5)$ — the number of cards in the deck and the number of queries.

The second line contains $𝑛$ integers $𝑎_1,𝑎_2,…,𝑎_𝑛$ $(1≤𝑎_𝑖≤50)$ — the colors of cards.

The third line contains $𝑞$ integers$ 𝑡_1,𝑡_2,…,𝑡_𝑞$ $(1≤𝑡_𝑗≤50)$ — the query colors. It's guaranteed that **queries ask only colors that are present in the deck**.

### Output
Print $𝑞$ integers — the answers for each query.

## 풀이 1


### 코드
```c++
#include <bits/stdc++.h>

using namespace std;
typedef long long ll;
const char nl = '\n';

int A[303030];
int Q[303030];
int D[51];

void solve() {
    int n, q; cin >> n >> q;
    for (int i = 1; i <= n; i++) {
        cin >> A[i];
        if (!D[A[i]]) D[A[i]] = i;
    }
    for (int i = 1; i <= q; i++) cin >> Q[i];
    for (int i = 1; i <= q; i++) {
        cout << D[Q[i]] << " ";
        for (int j = 1; j <= 50; j++) {
            if (j == Q[i]) continue;
            if (D[j] && D[j] < D[Q[i]]) D[j]++;
        }
        D[Q[i]] = 1;
    }
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    solve();
    return 0;
}

```

## 풀이 2


### 코드
```c++
#include <bits/stdc++.h>

using namespace std;
typedef long long ll;
const char nl = '\n';

int main() {
  int n, q; cin >> n >> q;
  vector<int> a(n);
  for (int& x : a) cin >> x;
  while (q--) {
    int x; cin >> x;
    int p = find(a.begin(), a.end(), x) - a.begin();
    cout << p + 1 << ' ';
    rotate(a.begin(), a.begin() + p, a.begin() + p + 1);
  }
}
```

# D. Min Cost String

Let's define the cost of a string $𝑠$ as the number of index pairs $𝑖$ and $𝑗$ $(1≤𝑖<𝑗<\|𝑠\|)$ such that $𝑠_𝑖=𝑠_𝑗$ and $𝑠_{𝑖+1}=𝑠_{𝑗+1}$.

You are given two positive integers $𝑛$ and $𝑘$. Among all strings with length $𝑛$ that contain only the first $𝑘$ characters of the Latin alphabet, find a string with minimum possible cost. If there are multiple such strings with minimum cost — find any of them.

### Input
The only line contains two integers $𝑛$ and $𝑘$ $(1≤𝑛≤2⋅10^5;1≤𝑘≤26)$.

### Output
Print the string $𝑠$ such that it consists of 𝑛 characters, each its character is one of the $𝑘$ first Latin letters, and it has the minimum possible cost among all these strings. If there are multiple such strings — print any of them.

## 풀이 1
* 오일러 경로 ([백준 19565번: 수열 만들기](https://www.acmicpc.net/problem/19565){:target="_blank"})


### 코드
```c++
#include <bits/stdc++.h>

using namespace std;
typedef long long ll;
const char nl = '\n';

void solve() {
    int n, k; cin >> n >> k;
    char a = 'a';
    vector<char> s;
    while (k > 0) {
        for (int j = 0; j < k - 1; j++) {
            s.push_back(a + j);
            s.push_back(a);
        }
        s.push_back(a + k - 1);
        a++; k--;
    }
    for (int i = 0; i < n; i++) {
        cout << s[i % s.size()];
    }
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    solve();
    return 0;
}

```
## 풀이 2


### 코드
```c++
#include <bits/stdc++.h>

using namespace std;

int n, k;
int cur[26];
vector<int> path;

void dfs(int v) {
  while (cur[v] < k) {
    int u = cur[v]++;
    dfs(u);
    path.push_back(u);
  }
}

int main() {
  cin >> n >> k;
  dfs(0);
  cout << 'a';
  for (int i = 0; i < n - 1; i++)
    cout << path[i % path.size()] + 'a';
}
```

<https://codeforces.com/contest/1511>{:target="_blank"}
