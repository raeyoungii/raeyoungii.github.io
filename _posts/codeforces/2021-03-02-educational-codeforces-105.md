---
layout: post
title: "Educational Codeforces: Round 105 (Div. 2)"
category: Codeforces
tags: [알고리즘, Codeforces]
comments: true
mathjax: true
---

> Codeforces

# A. ABC String

You are given a string $𝑎$, consisting of $𝑛$ characters, $𝑛$ is even. For each $𝑖$ from $1$ to $𝑛$ $𝑎_𝑖$ is one of 'A', 'B' or 'C'.

A bracket sequence is a string containing only characters "(" and ")". A regular bracket sequence is a bracket sequence that can be transformed into a correct arithmetic expression by inserting characters "1" and "+" between the original characters of the sequence. For example, bracket sequences "()()" and "(())" are regular (the resulting expressions are: "(1)+(1)" and "((1+1)+1)"), and ")(", "(" and ")" are not.

You want to find a string $𝑏$ that consists of $𝑛$ characters such that:
* $𝑏$ is a regular bracket sequence;
* if for some $𝑖$ and $𝑗$ $(1≤𝑖,𝑗≤𝑛)$ $𝑎_𝑖=𝑎_𝑗$, then $𝑏_𝑖=𝑏_𝑗$. 

In other words, you want to replace all occurrences of 'A' with the same type of bracket, then all occurrences of 'B' with the same type of bracket and all occurrences of 'C' with the same type of bracket.

Your task is to determine if such a string $𝑏$ exists.

### Input
The first line contains a single integer $𝑡$ $(1≤𝑡≤1000)$ — the number of testcases.

Then the descriptions of $𝑡$ testcases follow.

The only line of each testcase contains a string $𝑎$. $𝑎$ consists only of uppercase letters 'A', 'B' and 'C'. Let $𝑛$ be the length of $𝑎$. It is guaranteed that $𝑛$ is even and $2≤𝑛≤50$.

### Output
For each testcase print "YES" if there exists such a string $𝑏$ that:
* $𝑏$ is a regular bracket sequence;
* if for some $𝑖$ and $𝑗$ $(1≤𝑖,𝑗≤𝑛)$ $𝑎_𝑖=𝑎_𝑗$, then $𝑏_𝑖=𝑏_𝑗$. 

Otherwise, print "NO".

You may print every letter in any case you want (so, for example, the strings yEs, yes, Yes and YES are all recognized as positive answer).

## 풀이


### 코드
```c++
#include <bits/stdc++.h>

using namespace std;
typedef long long ll;

void solve() {
    string s; cin >> s;
    char x = s[0], z = s[s.size() - 1];
    if (x == z) cout << "NO\n";
    else {
        int sum1 = 0;
        for (int i = 0; i < s.size(); i++) {
            if (s[i] == z) sum1--;
            else sum1++;
        }
        if (sum1 == 0) { cout << "YES\n"; return; }

        int sum2 = 0;
        for (int i = 0; i < s.size(); i++) {
            if (s[i] == x) sum2++;
            else sum2--;
            if (sum2 < 0) break;
        }
        if (sum2 == 0) cout << "YES\n";
        else cout << "NO\n";
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

# B. 

Berland crossword is a puzzle that is solved on a square grid with $𝑛$ rows and $𝑛$ columns. Initially all the cells are white.

To solve the puzzle one has to color some cells on the border of the grid black in such a way that:
* exactly $𝑈$ cells in the top row are black;
* exactly $𝑅$ cells in the rightmost column are black;
* exactly $𝐷$ cells in the bottom row are black;
* exactly $𝐿$ cells in the leftmost column are black. 

Note that you can color zero cells black and leave every cell white.

Your task is to check if there exists a solution to the given puzzle.

### Input
The first line contains a single integer $𝑡$ $(1≤𝑡≤1000)$ — the number of testcases.

Then the descriptions of $𝑡$ testcases follow.

The only line of each testcase contains 5 integers $𝑛,𝑈,𝑅,𝐷,𝐿$ $(2≤𝑛≤100; 0≤𝑈,𝑅,𝐷,𝐿≤𝑛)$.

### Output
For each testcase print "YES" if the solution exists and "NO" otherwise.

You may print every letter in any case you want (so, for example, the strings yEs, yes, Yes and YES are all recognized as positive answer).

## 풀이


### 코드
```c++
#include <bits/stdc++.h>

using namespace std;
typedef long long ll;

int n;
int urdl[4];

bool chk(int x) {
    if (0 <= x && x <= n - 2) return true;
    else return false;
}

void solve() {
    cin >> n;
    for (int i = 0; i < 4; i++) {
        cin >> urdl[i];
    }
    bool flag = false;
    // 0
    if (chk(urdl[0]) && chk(urdl[1]) && chk(urdl[2]) && chk(urdl[3])) flag = true;
    // 1
    for (int i = 0; i < 4; i++) {
        if (chk(urdl[(0 + i) % 4] - 1) && chk(urdl[(1 + i) % 4] - 1) && chk(urdl[(2 + i) % 4]) && chk(urdl[(3 + i) % 4])) flag = true;
    }
    // 2 - 1
    if (chk(urdl[0] - 1) && chk(urdl[1] - 1) && chk(urdl[2] - 1) && chk(urdl[3]) - 1) flag = true;
    // 2 - 2
    for (int i = 0; i < 4; i++) {
        if (chk(urdl[(0 + i) % 4] - 1) && chk(urdl[(1 + i) % 4] - 2) && chk(urdl[(2 + i) % 4] - 1) && chk(urdl[(3 + i) % 4])) flag = true;
    }
    // 3
    for (int i = 0; i < 4; i++) {
        if (chk(urdl[(0 + i) % 4] - 1) && chk(urdl[(1 + i) % 4] - 2) && chk(urdl[(2 + i) % 4] - 2) && chk(urdl[(3 + i) % 4] - 1)) flag = true;
    }
    // 4
    if (chk(urdl[0] - 2) && chk(urdl[1] - 2) && chk(urdl[2] - 2) && chk(urdl[3] - 2)) flag = true;
    if (flag) cout << "YES\n";
    else cout << "NO\n";
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    int t; cin >> t;
    while(t--) solve();
    return 0;
}

```

<https://codeforces.com/contest/1494>{:target="_blank"}
