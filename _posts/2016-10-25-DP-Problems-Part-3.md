---
layout: post
title: 动态规划专练（三）
categories: [NOI, 动态规划]
description: 老文章
mini-description: 不知道写些什么，只好使用小红皮上的题
keywords: C++, 动态规划
---

# 1.矩形嵌套

时间限制：3000 ms  |  内存限制：65535 KB
难度：4  |  提供网站：NYOJ

## 描述

有n个矩形，每个矩形可以用a,b来描述，表示长和宽。矩形X(a,b)可以嵌套在矩形Y(c,d)中当且仅当a&lt;c,b&lt;d或者b&lt;c,a&lt;d（相当于旋转X90度）。例如（1,5）可以嵌套在（6,2）内，但不能嵌套在（3,4）中。你的任务是选出尽可能多的矩形排成一行，使得除最后一个外，每一个矩形都可以嵌套在下一个矩形内。
<!--more-->
## 输入

第一行是一个正正数N(0&lt;N&lt;10)，表示测试数据组数；每组测试数据的第一行是一个正正数n，表示该组测试数据中含有矩形的个数(n&lt;=1000)；随后的n行，每行有两个数a,b(0&lt;a,b&lt;100)，表示矩形的长和宽。

## 输出

每组测试数据都输出一个数，表示最多符合条件的矩形数目，每组输出占一行。

## 样例输入

```
1
10
1 2
2 4
5 8
6 10
7 9
3 1
5 8
12 10
9 7
2 2
```

## 样例输出

```
5
```

## 来源

经典题目

## 上传者

[张云聪](http://acm.nyist.net/JudgeOnline/profile.php?userid=%E5%BC%A0%E4%BA%91%E8%81%AA)

代码（这里提供两份，一份记忆化搜索，一份DAG最长路标准套路）：

``` cpp
#include<bits/stdc++.h>
using namespace std;

const int up=1000 +5;
struct matrix
{
    int h,w;
} a[up];
int f[up],n;
int fi(int x)
{
    if(f[x]) return f[x];
    for(int j=1;j<=n;j++)         
    if(j==x) continue;         
        else if((a[x].w>a[j].w && a[x].h>a[j].h) || (a[x].h>a[j].w && a[x].w>a[j].h))
            f[x]=max(f[x],fi(j)+1);
    return f[x];
}

int main()
{
    int N,x,y,maxn;

    scanf("%d",&N);
    while(N--)
    {
        scanf("%d",&n);maxn=0;memset(f,0,sizeof(f));
        for(int i=1;i<=n;i++) scanf("%d %d",&a[i].h,&a[i].w);
        for(int i=1;i<=n;i++) maxn=max(maxn,fi(i));
        printf("%d\n",maxn+1);
    }

    return 0;
}

#include<bits/stdc++.h>
using namespace std;

const int up=1000 +5;
struct matrix
{
    int h,w;
} a[up];
int f[up];
bool cmp(const matrix& x,const matrix& y)
{
    return x.h<y.h;
}

int main()
{
    int N,n,x,y,maxn;

    scanf("%d",&N);
    while(N--)
    {
        scanf("%d",&n);maxn=0;
        memset(f,0,sizeof f);
        for(int i=1;i<=n;i++)         
        {             
            scanf("%d %d",&x,&y);             
            if(x>y) a[i].h=y,a[i].w=x;
            else a[i].h=x,a[i].w=y;
        }
        sort(a+1,a+n+1,cmp);
        for(int i=2;i<=n;i++)
            for(int j=1;j<i;j++)                 
                if(a[i].w>a[j].w && a[i].h>a[j].h) f[i]=max(f[i],f[j]+1);
        for(int i=1;i<=n;i++) maxn=max(maxn,f[i]);
        printf("%d\n",maxn+1);
    }
    return 0;
}
```


# 2.硬币问题

## 描述

有n种硬币，面值分别为V1,V2,...Vn,每种都有无限多。给定非负整数S，可以选用多少个硬币，使得面值之和恰好为S？输出硬币数目的最小值和最大值。

## 输入

第一行是两个数n，S，1&lt;=n&lt;=100，0&lt;=S&lt;=10000；接下来n行是每一种硬币的面值Vi，1&lt;=Vi&lt;=S。

## 输出

两行各一个整数，第一行是硬币数目最小值，第二行是硬币数目最大值。

## 样例输入

```
5 10
1
2
4
5
7
```

## 样例输出

```
2
10
```

## 来源

ACM常见模型：DAG最长最短路，也可以看成完全背包。

代码：

``` cpp
#include<bits/stdc++.h>
using namespace std;

const int up1=10000 +5,up2=100 +5,inf=0x3f3f3f3f;
int f[up1],g[up1];
int V[up2];

int main()
{
    int n,S,maxn;

    scanf("%d %d",&n,&S);
    for(int i=1;i<=S;i++) f[i]=inf,g[i]=-inf;
    for(int i=1;i<=n;i++)
    {
        scanf("%d",&V[i]);
        for(int j=V[i];j<=S;j++) 
            f[j]=min(f[j],f[j-V[i]]+1),g[j]=max(g[j],g[j-V[i]]+1);
    }
    printf("%d\n%d",f[S],g[S]);
    return 0;
}
```


# 3.信任链

## 题目描述

现在有一排人站成一列，然后开始玩游戏。

现在告诉你有N个人（编号成1到N，排成一列），每个人有一个唯一的数字P。如果有俩个人A和B， 如果B的P是A的编号的约数并且B的编号小于A，那么A就相信B。

现在要找出最长的信任链，即一系列人，每个人都信任他前面的一个人**，序列可以不连续**。

## 输入格式

第一行一个数N。

下面一行N个数，表示每个人的唯一数字P。

## 输出格式

输出最长的信任链的长度。

## 输入样例

```
6
1 1 2 1 4 3
```

## 输出样例

```
5
```

## 数据规模

30%：N&lt;1000

100%：N0&lt;P&lt;=100

代码：

``` cpp
#include<bits/stdc++.h>
using namespace std;

int f[100005];
int a[105];

int main()
{
    int n,maxn=0,x;

    cin>>n;
    for(int i=1;i<=n;i++) f[i]=1;
    for(int i=1;i<=n;i++)          
    {                  
        scanf("%d",&x);                  
        for(int j=min(i,100);j>=1;j--) if(i%j==0) f[i]=max(f[i],a[j]+1);
        a[x]=max(a[x],f[i]);
        maxn=max(maxn,f[i]);
    }
    printf("%d\n",maxn);

    return 0;
}
```

同样是DAG最长路，但又有一些改变，首先是状态转移的改变，其次是策略的改变。

当同样的数作为状态推出最优解时，只需考虑同一个数中的链较长的一个，因为比它小的就一定不是最优解。

若以f[i]表示以i为尾最长的信任链，那么可以再声明a[p]表示在i之前值为p的最长信任链的长度。