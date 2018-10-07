---
layout: blog
title: 02-线性结构3 Reversing Linked List
date: 2018-9-12 14:03:19
tags: 中国大学MOOC-陈越、何钦铭-数据结构-2018秋
categories: 数据结构与算法
---
# 进展
|时间|进展|
|:--:|:--:|
|2018年9月12日中午|到目前为止还有两个测试点没过一个是全部反转，我测试的时候是对的呀；还有一个是超时|
|2018年9月13日21:02:58|AC|

# 难点
- 容易想到一些歪门邪道，比如说我第一次想到的排序方法。
- 模拟内存的想法。
- 具体进行逆转的时候的操作

# 反思
- 做OJ的题目有一些注意事项是你不得不放在心上的
 - 边界条件

# 代码
```C++
#include <iostream>
#include <iomanip>
#define max 100005

using namespace std;

struct node {
    int ads;
    int data;
    int next;
};

node memory[max];

int getlength(node * head);
node * reverse(node * head, int k);
void print(node * head, int length);

int main(int argc, char const *argv[]) {
    freopen("D:\\SJTU\\Freshman Summer\\DS\\test.txt", "r", stdin);
    int ads, n, k;cin >> ads >> n >> k;
    int address, data, next;
    for (int i = 0; i < n; i++) {
        cin >> address >> data >> next;
        memory[address].ads = address;
        memory[address].data = data;
        memory[address].next = next;
    }
    node head, *headptr;
    head.next = ads;
    headptr = &head;
    int length = getlength(headptr);
    for (size_t i = k; i <= length; i+=k) {
        int front = headptr->next;
        headptr->next = reverse(headptr,k)->ads;
        headptr = &memory[front];
        //print(&head,length);cout << endl;

    }
    headptr = &head;
    print(headptr,length);

    return 0;
}

node * reverse(node * head, int k) {
    node * front = &memory[head->next];
    node * rear = &memory[front->next];
    node * temp;
    int cnt = 1;
    while (cnt<k) {
        temp = &memory[rear->next];
        rear->next = front->ads;
        front = rear;
        rear = temp;
        cnt++;
    }
    memory[head->next].next = rear->ads;
    return front;
}

int getlength(node * head) {
    int cnt = 0, adds = head->next;
    while (adds!=-1) {
        cnt++;
        adds = memory[adds].next;
    }
    return cnt;
}

void print(node * head, int length) {
    node * ptr = &memory[head->next];
    for (size_t i = 0; i < length; i++) {
        cout << setw(5) << setfill('0') << ptr->ads;
        cout << ' ' << ptr->data << ' ';
        if ( i==length-1 ) cout << "-1";
        else cout << setw(5) << setfill('0') << ptr->next << endl;
        ptr = &memory[ptr->next];
    }
}
```
