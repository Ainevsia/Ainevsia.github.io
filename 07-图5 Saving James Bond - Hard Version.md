---
layout: blog
title: 07-图5 Saving James Bond - Hard Version
date: 2018-10-17 21:43:08
tags: 中国大学MOOC-陈越、何钦铭-数据结构-2018秋
categories: 数据结构与算法
---
# Links
[Here](https://pintia.cn/problem-sets/1010070491934568448/problems/1050401612970643457)

# Thoughts

## How to use the function qsort()
- parameters: qsort(void * array, int numberofcells, int sizeofeachcell, function cmp)
- function cmp:
- ```int cmp(const void * a, const void * b) {
    return ((*pointer* to the type of the elements waiting to be sorted)a)->some attribute of the element - ...b;
}```

## It is certainly a great habbit to write comments while writing the codes

# Talk is cheap, show me your **Codes**
```C++
#include <iostream>
#include <cmath>
#include <cstdlib>
#define max 102
const int radius = 50;
int maxtime = max;

struct node {           //crocodile -- node
    int x, y;           //position label x and y
    bool flag;          //true if the crocodile is close enough to the beach
    node * precedent;   //pointer to the previous crocodile
    double distance;    //distance to the previous crocodile
    int nodetime;       //attribute that trace the distance from island
};

struct Stack {          //stack to implement the closest way
    node * stack[max * 2];
    int sp;
    node * Pop(){return stack[sp--];}
    void Push(node * ptr){stack[++sp] = ptr;}
};

node croco[max];        //all the crocodiles are kept in this array
Stack priostack;        //priority stack
node * FinalNode = NULL;//keep the exit

using namespace std;

double getdis(int x1, int y1, int x2, int y2);
void dfs(node * ptr, int n, int d, node * pre, int times);
int cmp(const void * a, const void * b);

int main(int argc, char const *argv[]) {
    freopen("../test.txt", "r", stdin);
    int n, d;cin >> n >> d;
    priostack.sp = -1;
    for (int i = 0; i < n; ++i) {   //inialization
        cin >> croco[i].x >> croco[i].y;
        croco[i].flag = radius - abs(croco[i].x) <= d || radius - abs(croco[i].y) <= d;
        croco[i].precedent = NULL;
        croco[i].distance = 0;
        croco[i].nodetime = max;
    }

    //first iteration
    for (int i = 0; i < n; ++i) {
        if (getdis(0,0,croco[i].x,croco[i].y)<=7.5+d) {
            croco[i].distance = getdis(0,0,croco[i].x,croco[i].y);
            priostack.Push(&croco[i]);
        }
    }
    if (priostack.sp+1 > 1) qsort(&priostack.stack[0], priostack.sp+1, sizeof(node*), cmp);
    int cnt = 0, num = priostack.sp + 1;
    while (cnt++ < num) dfs(priostack.Pop(),n,d,NULL,1);

    //out put section
    if (maxtime == max) cout << 0;
    else if (d >= 43) cout << 1;
    else {
        int outputcnt = 0;
        while (FinalNode) {
            outputcnt++;
            priostack.Push(FinalNode);
            FinalNode = FinalNode->precedent;
        }
        cout << outputcnt + 1 << endl;
        while (outputcnt--) {
            FinalNode = priostack.Pop();
            cout << FinalNode->x << ' ' << FinalNode->y << endl;
        }
    }
    return 0;
}

void dfs(node * ptr, int n, int d, node * pre, int times) {
    ptr->precedent = pre;
    if (ptr->flag && times < maxtime) {
        maxtime = times;
        FinalNode = ptr;
    }
    ptr->nodetime = times;
    int bp = priostack.sp;
    for (int i = 0; i < n; ++i) {
        if (croco[i].nodetime>times+1 && getdis(ptr->x,ptr->y,croco[i].x,croco[i].y)<=d) {
            croco[i].distance = getdis(0,0,croco[i].x,croco[i].y);
            priostack.Push(&croco[i]);
        }
    }
    int num = priostack.sp - bp;
    if (num > 1) qsort(&priostack.stack[bp+1], (size_t)priostack.sp-bp, sizeof(node*), cmp);
    int cnt = 0;
    while (cnt++ < num) dfs(priostack.Pop(),n,d,ptr,times+1);
}

int cmp(const void * a, const void * b) {
    double d = (*((node**)b))->distance - (*((node**)a))->distance;
    return d > 0 ? 1 : -1;
}

double getdis(int x1, int y1, int x2, int y2) {
    double ret = sqrt((x1-x2)*(x1-x2) + (y1-y2)*(y1-y2));
    return ret;
}

```
