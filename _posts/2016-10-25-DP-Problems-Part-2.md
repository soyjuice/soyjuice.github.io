---
layout: post
title: 动态规划专练（二）
categories: [NOI, 动态规划]
description: 老文章
mini-description: 依然非常简单的DP
keywords: C++, 动态规划
---

# 1.数字三角形（一维数组）

## 描述

示出了一个数字三角形。 请编一个程序计算从顶至底的某处的一条路
径，使该路径所经过的数字的总和最大。
每一步可沿左斜线向下或右斜线向下走；
1&lt;三角形行数&lt;25；
三角形中的数字为整数&lt;1000；
<!--more-->
## 输入格式

第一行为N，表示有N行
后面N行表示三角形每条路的路径权

## 输出格式

路径所经过的数字的总和最大的答案

## 测试样例

### 输入

```
5
7
3 8
8 1 0
2 7 4 4
4 5 2 6 5
```

### 输出

```
30
```

## 备注

搜索80，记忆化AC。

代码：

``` cpp
#include<bits/stdc++.h>
using namespace std;

const int up=30;

int main() 
{
    int a[up],f[up],n,ans=-1;
    memset(a,0,sizeof a);
    memset(f,0,sizeof f);

    cin>>n;
    for(int i=1;i<=n;i++)
    {
        for(int j=1;j<=i;j++) cin>>a[j];
        for(int j=i;j>=1;j--) f[j]=max(f[j],f[j-1])+a[j];
    }

    for(int i=1;i<=n;i++) ans=max(ans,f[i]);
    cout<<ans<<endl;

    return 0;
}
```


# 2.三取方格数

## 背景

JerryZhou同学经常改编习题给自己做。

这天，他又改编了一题。。。。。

## 描述

设有N*N的方格图，我们将其中的某些方格填入正整数，
而其他的方格中放入0。

某人从图得左上角出发，可以向下走，也可以向右走，直到到达右下角。

在走过的路上，他取走了方格中的数。（取走后方格中数字变为0）
此人从左上角到右下角共走3次，试找出3条路径，使得取得的数总和最大。

## 格式

### 输入格式

第一行:N (4&lt;=N&lt;=20)
接下来一个N*N的矩阵，矩阵中每个元素不超过80，不小于0

### 输出格式

一行，表示最大的总和。

## 测试样例

### 样例输入

```
4
1 2 3 4
2 1 3 4
1 2 3 4
1 3 2 4
```

### 样例输出

```
39
```

## 限制

各个测试点1s

## 提示

多进程DP

代码：

``` cpp
#include<bits/stdc++.h>
using namespace std;

const int up=20 +5;

int n,a[up][up],f[2*up][up][up][up];

int main()
{
    scanf("%d",&n);
    for(int i=1;i<=n;i++)
        for(int j=1;j<=n;j++)
            scanf("%d",&a[i][j]);
    f[1][1][1][1]=a[1][1];

    for(int s=2;s<=2*n-1;s++)
        for(int x1=max(1,s-n+1);x1<=min(n,s);x1++)
            for(int x2=max(1,s-n+1);x2<=min(n,s);x2++)
                for(int x3=max(1,s-n+1);x3<=min(n,s);x3++)
                {
                    //s=x+y-1
                    int mid=a[x1][s-x1+1]+a[x2][s-x2+1]+a[x3][s-x3+1];
                    if(x1==x2) mid-=a[x1][s-x1+1];
                    if(x1==x3) mid-=a[x1][s-x1+1];
                    if(x2==x3) mid-=a[x2][s-x2+1];
                    if(x1==x2 && x2==x3) mid+=a[x1][s-x1+1];//容斥原理
                    f[s][x1][x2][x3]=max(f[s-1][x1][x2][x3],max(f[s-1][x1][x2][x3-1],max(f[s-1][x1][x2-1][x3],max(f[s-1][x1][x2-1][x3-1],max(f[s-1][x1-1][x2][x3],max(f[s-1][x1-1][x2][x3-1],max(f[s-1][x1-1][x2-1][x3],f[s-1][x1-1][x2-1][x3-1])))))));
                    f[s][x1][x2][x3]+=mid;
                }

    printf("%d",f[2*n-1][n][n][n]);

    return 0;
}
```

**注**：

思路与传纸条和方格取数相似，但由于数组维数过高（6维）无法直接声明，所以只能压缩维度。
通过分析，可以发现y坐标直接与x坐标相关，可以通过步数算出y坐标，同理，x坐标也可以被y坐标算出，这里姑且使用x坐标作为另外三个维度。

循环的时候x从1到n，用x=max(1,s-n+1)，其中1是防止x越界，s-n+1是防止y越界；因为s=x+y-1，所以y=s-x+1&lt;=n，s-n+1&lt;=x，用x&lt;=min(n,s)是防止x越界。

**另外，分享一份网络流的题解（[wang_yanheng](https://vijos.org/user/101292)）：**
> 把MAX_CAPACITY改成任意正整数k，即可实现k取方格数
> 主要思路就是拆点构图。
> 把每个点 x 拆成 x1, x2，x1与x2之间有：
> 
> *   一条容量为1，价值为x权值的边
> *   一条容量为MAX_CAPACITY，价值为0的边
> 
> 假设y, z分别为 x 右侧、下方的点，把 x2 与 y1、x2 与 z1 各连一条边，容量为MAX_CAPACITY，价值为0
> 最后加上源点与汇点，最大费用流即可。我使用了SPFA寻找最长价值的路径。
> 
> 解释一下变量含义：
> 
> *   edge类型中，next指向的是同一起点的下一条边在E中的位置
> *   E是边集，size 是 E 的大小
> *   headIndex[i] 指向的是起点为 i 的头一条边在E中的位置
> *   used, dist, queue, prev 用于最长路算法，其中 prev[i] 记录最长路中通往点 i 的边在E中的位置

``` cpp
#include <bits/stdc++.h>
#define NIL -1
#define MAX_CAPACITY 3
#define INF 10000000
#define MIN(a,b) ((a)<(b)?(a):(b))
using namespace std;

typedef struct{
    int next;
    int from, to, value, f;
} edge;

edge E[5000];
int headIndex[1000];
int size = 0;

short used[1000];
int queue[10000];
int dist[1000];
int prev[1000];

void addEdge1(int from, int to, int value, int capacity);
void addEdge(int from, int to, int value, int capacity);
int maxPath(int source, int sink, int numV);
int maxValueFlow(int source, int sink, int numV);

int main(){
    int n, numV;
    int x, y, source, sink, value;

    scanf("%d", &n);

    /*initialize*/
    for(x=0; x<1000; x++)
        headIndex[x] = NIL;

    /*build the network*/
    numV = 0;
    for(x=0; x<n; x++){
        for(y=0; y<n; y++){
            scanf("%d", &value);
            addEdge(numV, numV+1, value, 1);  //connect numV & numV+1
            addEdge(numV, numV+1, 0, MAX_CAPACITY);
            if(x < n-1)
                addEdge(numV+1, numV+2*n, 0, MAX_CAPACITY);  //connnect numV+1 & its downer neighbour, if exists
            if(y < n-1)
                addEdge(numV+1, numV+2, 0, MAX_CAPACITY);  //connnect numV+1 & its righter neighbour, if exists
            numV += 2;
        }
    }
    source = numV, sink = numV+1;
    addEdge(source, 0, 0, MAX_CAPACITY);  //source
    addEdge(numV-1, sink, 0, MAX_CAPACITY);  //sink

    /*solve*/
    printf("%d\n", maxValueFlow(source, sink, numV+2));
    return 0;
}
void addEdge1(int from, int to, int value, int capacity){
    E[size].from = from;
    E[size].to = to;
    E[size].value = value;
    E[size].f = capacity;
    E[size].next = headIndex[from];
    headIndex[from] = size;
    size++;
}
void addEdge(int from, int to, int value, int capacity){
    addEdge1(from, to, value, capacity);
    addEdge1(to, from, -value, 0);
}
int maxPath(int source, int sink, int numV){
    int i, head = 0, tail = 0;
    for(i=0; i<numV; i++){
        used[i] = 0;
        prev[i] = NIL;
        dist[i] = -INF;
    }
    dist[source] = 0;
    queue[tail++] = source;
    while(head < tail){
        source = queue[head];
        used[source] = 0;
        i = headIndex[source];
        while(i != NIL){
            if(E[i].f > 0 && dist[E[i].to] < dist[source] + E[i].value){
                dist[E[i].to] = dist[source] + E[i].value;
                prev[E[i].to] = i;
                if(!used[E[i].to]){
                    queue[tail++] = E[i].to;
                    used[E[i].to] = 1;
                }
            }
            i = E[i].next;
        }
        head++;
    }
    return dist[sink];
}
int maxValueFlow(int source, int sink, int numV){
    int path, v, augment, value, ret = 0;
    while((value = maxPath(source, sink, numV)) > 0){
        augment = INF;
        for(v=sink; v!=source; ){
            path = prev[v];
            augment = MIN(augment, E[path].f);
            v = E[path].from;
        }
        for(v=sink; v!=source; ){
            path = prev[v];
            E[path].f -= augment;
            E[path^1].f += augment;
            v = E[path].from;
        }
        ret += value*augment;
    }
    return ret;
}
```