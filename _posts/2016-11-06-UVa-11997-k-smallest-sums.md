---
layout: post
title: UVa 11997 K Smallest Sums
categories: [NOI, 多路归并]
description: 老文章
keywords: C++, 多路归并, 暴力
---

You’re given k arrays, each array has k integers. There are k<sup>k</sup>  ways to pick exactly one element in each array and calculate the sum of the integers. Your task is to find the k smallest sums among them.

你被赋予了k个数组，每个数组都有k个整数。有k<sup>k</sup>的方式去在每个数组中挑选一个数，然后计算这些整数之和。你的任务是找到他们之间的最小的和。
<!--more-->
## Input

There will be several test cases. The first line of each case contains an integer k (2 ≤ k ≤ 750). Each of the following k lines contains k positive integers in each array. Each of these integers does not exceed 1,000,000\. The input is terminated by end-of-file (EOF).

将有几个测试数据。每个数据的第一行包含一个整数k（2≤k≤750）。每个下面的K行中包含每个数组中的k个正整数。这些整数中的每一个不超过1000000。输入EOF结束（EOF）。

## Output

For each test case, print the k smallest sums, in ascending order.

对于每一个测试数据，输出最小的和，以递增的顺序。

## Data

**标准输入**

<pre>3
1 8 5
9 2 5
10 7 6
2
1 1
1 2</pre>

**标准输出**

<pre>9 10 12
2 2</pre>

**注：以上翻译取自机翻，加上我的修改，应该勉强能看。**

## Analysis

**题目分析：**非常简单明了的题意，如果是最优解，可以直接从每个序列选取最大值，但是由于是前优K解，所以没法这么直接。

**算法分析：**对于前优K解，根据刘汝佳大神的方法，可以用多路归并解决。

解决这个问题之前，可以先考虑它的简化版：给出两个长度为n的**有序**表A,B各取一个数，可以有n<sup>2</sup>个和，求最小的前n个和。

我们可以将这n<sup>2</sup>个和分成n个有序表

表1：A<sub>1</sub>+B<sub>1 </sub><= A<sub>1</sub>+B<sub>2 </sub><= A<sub>1</sub>+B<sub>3 </sub><= ...
表2：A<sub>2</sub>+B<sub>1 </sub><= A<sub>2</sub>+B<sub>2 </sub><= A<sub>2</sub>+B<sub>3 </sub><= ...
表3：A<sub>3</sub>+B<sub>1 </sub><= A<sub>3</sub>+B<sub>2 </sub><= A<sub>3</sub>+B<sub>3 </sub><= ...

可以看出当A,B递增时，上表也是递增。

可以用二元组(s,b)表示一个元素，其中s=A<sub>a</sub>+A<sub>b</sub>。当需要某个表中的下一个元素(s',b+1)时，只需要

**s'**=A<sub>a</sub>+B<sub>b+1</sub>=A<sub>a</sub>+B<sub>b</sub>-B<sub>b</sub>+B<sub>b+1</sub>=**s-B<sub>b</sub>+B<sub>b+1</sub>**

因此，定义下面这个结构体来表示上述二元组。

``` cpp
struct Item
{
    int s,b;
    Item(int s,int b):s(s),b(b){}
    bool operator < (const Item& rhs) const  
    {       
        return s > rhs.s;
    }
};
```


每次读入一组数据时，将表合并，取n次最小值；因为在取出表1的元素之前，表2对应位置的数一定要大，一定不是当前的最小值，所以当取出这个元素后，再将它同列的下一个元素入队。

``` cpp
void merge(int* A,int* B,int* C,int n)
{
    priority_queue q;
    for(int i=0;i<n;i++) q.push(Item(A[i]+B[0],0));
    for(int i=0;i<n;i++)
    {
        Item item=q.top();q.pop();
        C[i]=item.s;
        int b=item.b;
        if(b+1<n) q.push(Item(item.s-B[b]+B[b+1],b+1));
    }
}
```


这样，两个表的问题就解决了。如果是多个表的话，两两合并就可以。

**数据分析：**k<=750，并不算特别大，优先队列完全可以承受。

**代码分析：**

``` cpp
#include<bits/stdc++.h>
using namespace std;

const int maxn=768;
int A[maxn][maxn];

struct Item
{
    int s,b;
    Item(int s,int b):s(s),b(b){}
    bool operator < (const Item& rhs) const     
    {         
        return s > rhs.s;
    }
};

void merge(int* A,int* B,int* C,int n)
{
    priority_queue q;
    for(int i=0;i<n;i++) q.push(Item(A[i]+B[0],0));
    for(int i=0;i<n;i++)
    {
        Item item=q.top();q.pop();
        C[i]=item.s;
        int b=item.b;
        if(b+1<n) q.push(Item(item.s-B[b]+B[b+1],b+1));
    }
}

int main()
{
    int n;
    while(scanf("%d",&n)==1)
    {
        for(int i=0;i<n;i++) 
        {
            for(int j=0;j<n;j++) scanf("%d",&A[i][j]);
            sort(A[i],A[i]+n);
        }
        for(int i=1;i<n;i++) merge(A[0],A[i],A[0],n);
        for(int i=0;i<n;i++) printf("%d ",A[0][i]);
        printf("\n");
    }
    return 0;
}
```

**多路归并**可以广泛地运用于各种求**最优k解**，原理是将**多个有序表**合并成**一个有序表**，对于答案来说，其必然是一个有序表，故此算法正确，并将所有可能性考虑到。
