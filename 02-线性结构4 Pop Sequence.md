---
layout: blog
title: 02-线性结构4 Pop Sequence
date: 2018-9-14 12:11:54
tags: 中国大学MOOC-陈越、何钦铭-数据结构-2018秋
categories: 数据结构与算法
---
# thoughts
- too simple: just stack simulation
- 这一次真的是爽啊，一次性过，代码简洁没有任何冗余的边界调试
- 这样的题目是可遇而不可求啊！
- 我用树和用图也要达到我用堆的这样的境界！

# codes
```C++
#include <iostream>

using namespace std;

bool check(int m, int n);

int main(int argc, char const *argv[]) {
    int m, n, k;cin >> m >> n >> k;
    for (int i = 0; i < k; i++) {
        bool valid = check(m,n);
        if (valid) cout << "YES" << endl;
        else cout << "NO" << endl;
    }
    return 0;
}

bool check(int m, int n) {
    int * stack = new int [n], stk = -1;
    int * store = new int [n], str = 0;
    for (int i = 0; i < n; i++) {
        cin >> store[i];
    }
    bool valid = false;
    for (int topush = 1; topush <= n; topush++) {
        stack[++stk] = topush;
        if (stk==m) break;
        while (stk!=-1 && store[str]==stack[stk]) {
            stk--;str++;
        }
    }
    if (stk==-1) valid = true;
    delete [] stack;
    return valid;
}

```
