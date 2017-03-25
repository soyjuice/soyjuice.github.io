---
layout: post
title: 贪心专练
categories: 贪心
description: 老文章
keywords: 贪心
---

不知道怎么做哎。 

不断行就去死吧。
&nbsp

## 硬币问题

1.有1元、5元、10元、50元、100元与500元的硬币各C<sub>1</sub>、C<sub>5</sub>、C<sub>10</sub>、C<sub>50</sub>、C<sub>100</sub>、C<sub>500</sub>枚，现在要用这些硬币来支付A元，最少需要多少枚硬币？假定至少有支付方案。

分析：尽可能多的使用大面值的硬币，因为同样的价值所需的硬币中，使用大面值一定少于使用小面值的数量（也许这些小面值还可以拼成一个大面值）。

``` cpp
int ans=0;
for(int i=5;i>=0;i--) 
{ 
    int t=min(A/V[i],C[i]); 
    A-=t*V[i]; ans+=t; 
}
```

2.相似的选取最大值，比如UVa 11292 The Dargon of Loowater。

## 区间问题

1.有n项工作，每项工作分别在s<sub>i</sub>时间开始，在t<sub>i</sub>时间结束。对于每项工作，你都可以选择参与与否，但必须全程参与，这意味着时间不能重叠。

分析：每次选择时间结束最早的，在同等条件（仅仅是一个工作）下，选择结束最早的工作，因为完成一个工作后，剩下的时间越长，还可以做的工作就有可能会更多，就一定是最优。

``` cpp
for(int i=0;i<N;i++) 
{ 
    itv[i].be=S[i]; 
    itv[i].en=T[i]; 
}

int ans=0,t=0; 
for(int i=0;i<N;i++) 
if(t<itv[i].be) 
{ 
    ans++; 
    t=itv[i].en; 
} 
printf("%d\n",&ans);
```

另外，在证明贪心策略是最优解时，可以广泛的使用归纳法或是反证法（其实它更多用来证明贪心不是最优）。

3.相似的同等条件下最多或最少，比如POJ 3069 Suruman’s Army、UVa 11729 Commando War。

## 字典序问题

1.给定长度为N且只有大写字母的字符串S，构造一个长度为N的字符串T，反复选择S的前后字母删除，放入T末尾，构造一个字典序最小的T。

分析：尽可能选取字典序小的字母先放，如果前后相等，那么就选择可以较快取到小的字母的那一边。

``` cpp
int a=0,b=N-1; 
while(a<=b) 
{ 
    bool left=false; 
    for(int i=0;a+i<=b-i;i++) 
    if(S[a+i]<S[b-i]) 
    { 
        left=true; 
        break; 
    } else if(S[a+i]>S[b-i]) break; 
    if(left) putchar(S[a++]); 
    else putchar(S[b--]); 
} 
putchar('\n');
```

2.相似的字典序问题，如POJ 3617 Best Cow Line。

3.类比的两端加权取数，如Vijos 1378 矩阵取数游戏。

## 更多的贪心问题

1.本文仅仅挑选了有代表性的且较为简单的贪心题，然而还有更多且复杂的题目，它们都需要好好地思考一下才能做对。

2.更多的贪心问题，还有代表性的有Vijos 1097 合并果子(POJ 3253 Fence Repair)、UVa 11300 Spreading the Wealth、LA 3708 Graveyard，甚至一些动规问题都可以用贪心处理（当然能拿多少分还是得靠信仰）。

3.本文所有的题目

|来源&题号|题目|
|:--|:--|
|UVa 11292|The Dargon of Loowater|
|POJ 3069|Suruman’s Army|
|UVa 11729|Commando War|
|POJ 3617|Best Cow Line|
|Vijos 1378|矩阵取数游戏|
|Vijos 1097|合并果子|
|UVa 11300|Spreading the Wealth|
|LA 3708|Graveyard|
