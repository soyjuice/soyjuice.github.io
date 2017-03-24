---
layout: post
title: 动态规划专练（四）
categories: [NOI, 动态规划]
description: 老文章
keywords: C++, 动态规划
---

# 1.采药

## 题目描述

辰辰是个天资聪颖的孩子，他的梦想是成为世界上最伟大的医师。为此，他想拜附近最有威望的医师为师。医师为了判断他的资质，给他出了一个难题。医师把他带到一个到处都是草药的山洞里对他说：“孩子，这个山洞里有一些不同的草药，采每一株都需要一些时间，每一株也有它自身的价值。我会给你一段时间，在这段时间里，你可以采到一些草药。如果你是一个聪明的孩子，你应该可以让采到的草药的总价值最大。”

如果你是辰辰，你能完成这个任务吗？
<!--more-->
## 输入格式

第一行有两个整数T（1 &lt;= T &lt;= 1000）和M（1 &lt;= M &lt;= 100），用一个空格隔开，T代表总共能够用来采药的时间，M代表山洞里的草药的数目。接下来的M行每行包括两个在1到100之间（包括1和100）的整数，分别表示采摘某株草药的时间和这株草药的价值。

## 输出格式

一行，这一行只包含一个整数，表示在规定的时间内，可以采到的草药的最大总价值。

## **输入样例**

```
70 3
71 100
69 1
1 2
```

## 输出样例

```
3
```

## 说明

对于30%的数据，M &lt;= 10；

对于全部的数据，M &lt;= 100。

NOIP2005普及组第三题，也就是背包问题中的01背包。

代码：

<pre style="color:#000000;background:transparent;"><span style="color:#004a43;">#</span><span style="color:#004a43;">include</span><span style="color:#800000;">&lt;</span><span style="color:#40015a;">bits/stdc++.h</span><span style="color:#800000;">&gt;</span>
<span style="color:#800000;font-weight:bold;">using</span> <span style="color:#800000;font-weight:bold;">namespace</span> <span style="color:#666616;">std</span><span style="color:#800080;">;</span>

<span style="color:#800000;font-weight:bold;">const</span> <span style="color:#800000;font-weight:bold;">int</span> up<span style="color:#808030;">=</span><span style="color:#008c00;">1000</span> <span style="color:#808030;">+</span><span style="color:#008c00;">5</span><span style="color:#800080;">;</span>

<span style="color:#800000;font-weight:bold;">int</span> <span style="color:#400000;">main</span><span style="color:#808030;">(</span><span style="color:#808030;">)</span>
<span style="color:#800080;">{</span>
    <span style="color:#800000;font-weight:bold;">int</span> t<span style="color:#808030;">,</span>m<span style="color:#808030;">,</span>ti<span style="color:#808030;">,</span>vi<span style="color:#808030;">,</span>f<span style="color:#808030;">[</span>up<span style="color:#808030;">]</span><span style="color:#800080;">;</span>
    <span style="color:#603000;">memset</span><span style="color:#808030;">(</span>f<span style="color:#808030;">,</span><span style="color:#008c00;">0</span><span style="color:#808030;">,</span><span style="color:#800000;font-weight:bold;">sizeof</span> f<span style="color:#808030;">)</span><span style="color:#800080;">;</span>
    <span style="color:#603000;">scanf</span><span style="color:#808030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%d</span> <span style="color:#007997;">%d</span><span style="color:#800000;">"</span><span style="color:#808030;">,</span><span style="color:#808030;">&amp;</span>t<span style="color:#808030;">,</span><span style="color:#808030;">&amp;</span>m<span style="color:#808030;">)</span><span style="color:#800080;">;</span>
    <span style="color:#800000;font-weight:bold;">while</span><span style="color:#808030;">(</span>m<span style="color:#808030;">-</span><span style="color:#808030;">-</span><span style="color:#808030;">)</span>
    <span style="color:#800080;">{</span>
        <span style="color:#603000;">scanf</span><span style="color:#808030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%d</span> <span style="color:#007997;">%d</span><span style="color:#800000;">"</span><span style="color:#808030;">,</span><span style="color:#808030;">&amp;</span>ti<span style="color:#808030;">,</span><span style="color:#808030;">&amp;</span>vi<span style="color:#808030;">)</span><span style="color:#800080;">;</span>
        <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> i<span style="color:#808030;">=</span>t<span style="color:#800080;">;</span>i<span style="color:#808030;">&gt;</span><span style="color:#808030;">=</span>ti<span style="color:#800080;">;</span>i<span style="color:#808030;">-</span><span style="color:#808030;">-</span><span style="color:#808030;">)</span> f<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">=</span><span style="color:#603000;">max</span><span style="color:#808030;">(</span>f<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">,</span>f<span style="color:#808030;">[</span>i<span style="color:#808030;">-</span>ti<span style="color:#808030;">]</span><span style="color:#808030;">+</span>vi<span style="color:#808030;">)</span><span style="color:#800080;">;</span>
    <span style="color:#800080;">}</span>
    <span style="color:#603000;">printf</span><span style="color:#808030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%d</span><span style="color:#0f69ff;">\n</span><span style="color:#800000;">"</span><span style="color:#808030;">,</span>f<span style="color:#808030;">[</span>t<span style="color:#808030;">]</span><span style="color:#808030;">)</span><span style="color:#800080;">;</span>

    <span style="color:#800000;font-weight:bold;">return</span> <span style="color:#008c00;">0</span><span style="color:#800080;">;</span>
<span style="color:#800080;">}</span></pre>


对于 背包问题，我个人是这么认为的：

首先，**滚动数组**（其实就是压了并不重要的一维）是必然的，而且背包问题滚动数组更容易理解。

在01背包中，循环由大到小，如“for(int i=C;i&gt;=V;i--) f[i]=max(f[i],f[i-V]+W);”，较末的状态转移自较前的状态是背包问题也是大部分动态规划题目的特点，而较末的状态先被计算，对**同一个循环中的其它状态**是不会有影响的，因为较前的状态只会转移自比它更前的状态；而在完全背包中，循环由小到大，如“for(int i=V;i&lt;=C;i++) f[i]=max(f[i],f[i-V]+W);”，较前的状态先被计算，于是就有可能对**同一循环中之后的状态**造成影响。

至于剩下的一些背包问题，则是万变不离其宗，比如多重背包，可以看作有同种物品的01背包，还有混合背包，也可以同样看作是不同多种物品的01背包。

# 2.点集配对问题

## 问题描述

空间里有n个点P0,P1,P2,...,Pn-1，把它们分成n/2对，使得每个点恰好在一个点对中，且所有点对距离之和尽量小。

## 输入格式

第一行是整数n，数据保证n为偶数；接下来n行每行三个数，分别代表点i的x,y,z坐标。

## 输出格式

输出只有一行，为最小的所有点对距离之和，保留两位小数。

## 输入样例

```
4
1 1 1
1 1 2
1 4 3
1 6 6
```

## 输出样例

```
4.61
```

## 说明

n&lt;=20，|xi|,|yi|,|zi|&lt;=10000。

代码：

<pre style="color:#000000;background:transparent;"><span style="color:#004a43;">#</span><span style="color:#004a43;">include</span><span style="color:#800000;">&lt;</span><span style="color:#40015a;">bits/stdc++.h</span><span style="color:#800000;">&gt;</span>
<span style="color:#800000;font-weight:bold;">using</span> <span style="color:#800000;font-weight:bold;">namespace</span> <span style="color:#666616;">std</span><span style="color:#800080;">;</span>

<span style="color:#800000;font-weight:bold;">const</span> <span style="color:#800000;font-weight:bold;">int</span> up<span style="color:#808030;">=</span><span style="color:#008c00;">20</span> <span style="color:#808030;">+</span><span style="color:#008c00;">5</span><span style="color:#800080;">;</span>
<span style="color:#800000;font-weight:bold;">const</span> <span style="color:#800000;font-weight:bold;">double</span> inf<span style="color:#808030;">=</span><span style="color:#008000;">1e10</span><span style="color:#800080;">;</span>
<span style="color:#800000;font-weight:bold;">struct</span> node
<span style="color:#800080;">{</span>
    <span style="color:#800000;font-weight:bold;">int</span> x<span style="color:#808030;">,</span>y<span style="color:#808030;">,</span>z<span style="color:#800080;">;</span>
<span style="color:#800080;">}</span> g<span style="color:#808030;">[</span>up<span style="color:#808030;">]</span><span style="color:#800080;">;</span>
<span style="color:#800000;font-weight:bold;">int</span> n<span style="color:#808030;">,</span>k<span style="color:#800080;">;</span>
<span style="color:#800000;font-weight:bold;">double</span> f<span style="color:#808030;">[</span><span style="color:#008c00;">1</span><span style="color:#808030;">&lt;</span><span style="color:#808030;">&lt;</span>up<span style="color:#808030;">]</span><span style="color:#800080;">;</span><span style="color:#696969;">//二进制集合表示状态</span>

<span style="color:#800000;font-weight:bold;">double</span> dis<span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> i<span style="color:#808030;">,</span><span style="color:#800000;font-weight:bold;">int</span> j<span style="color:#808030;">)</span>
<span style="color:#800080;">{</span>
    <span style="color:#800000;font-weight:bold;">return</span> <span style="color:#603000;">sqrt</span><span style="color:#808030;">(</span><span style="color:#808030;">(</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">double</span><span style="color:#808030;">)</span><span style="color:#808030;">(</span>g<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">.</span>x<span style="color:#808030;">-</span>g<span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#808030;">.</span>x<span style="color:#808030;">)</span><span style="color:#808030;">*</span><span style="color:#808030;">(</span>g<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">.</span>x<span style="color:#808030;">-</span>g<span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#808030;">.</span>x<span style="color:#808030;">)</span><span style="color:#808030;">+</span><span style="color:#808030;">(</span>g<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">.</span>y<span style="color:#808030;">-</span>g<span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#808030;">.</span>y<span style="color:#808030;">)</span><span style="color:#808030;">*</span><span style="color:#808030;">(</span>g<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">.</span>y<span style="color:#808030;">-</span>g<span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#808030;">.</span>y<span style="color:#808030;">)</span><span style="color:#808030;">+</span><span style="color:#808030;">(</span>g<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">.</span>z<span style="color:#808030;">-</span>g<span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#808030;">.</span>z<span style="color:#808030;">)</span><span style="color:#808030;">*</span><span style="color:#808030;">(</span>g<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">.</span>z<span style="color:#808030;">-</span>g<span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#808030;">.</span>z<span style="color:#808030;">)</span><span style="color:#808030;">)</span><span style="color:#808030;">)</span><span style="color:#800080;">;</span>
<span style="color:#800080;">}</span>

<span style="color:#800000;font-weight:bold;">int</span> <span style="color:#400000;">main</span><span style="color:#808030;">(</span><span style="color:#808030;">)</span>
<span style="color:#800080;">{</span>
    <span style="color:#603000;">scanf</span><span style="color:#808030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%d</span><span style="color:#800000;">"</span><span style="color:#808030;">,</span><span style="color:#808030;">&amp;</span>n<span style="color:#808030;">)</span><span style="color:#800080;">;</span>
    <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> i<span style="color:#808030;">=</span><span style="color:#008c00;">0</span><span style="color:#800080;">;</span>i<span style="color:#808030;">&lt;</span>n<span style="color:#800080;">;</span>i<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span> <span style="color:#603000;">scanf</span><span style="color:#808030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%d</span> <span style="color:#007997;">%d</span> <span style="color:#007997;">%d</span><span style="color:#800000;">"</span><span style="color:#808030;">,</span><span style="color:#808030;">&amp;</span>g<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">.</span>x<span style="color:#808030;">,</span><span style="color:#808030;">&amp;</span>g<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">.</span>y<span style="color:#808030;">,</span><span style="color:#808030;">&amp;</span>g<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">.</span>z<span style="color:#808030;">)</span><span style="color:#800080;">;</span>
    <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> i<span style="color:#808030;">=</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>i<span style="color:#808030;">&lt;</span><span style="color:#808030;">(</span><span style="color:#008c00;">1</span><span style="color:#808030;">&lt;</span><span style="color:#808030;">&lt;</span>n<span style="color:#808030;">)</span><span style="color:#800080;">;</span>i<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span>
    <span style="color:#800080;">{</span>
    f<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">=</span>inf<span style="color:#800080;">;</span>
    <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span>k<span style="color:#808030;">=</span><span style="color:#008c00;">0</span><span style="color:#800080;">;</span>k<span style="color:#808030;">&lt;</span>n<span style="color:#800080;">;</span>k<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span> <span style="color:#800000;font-weight:bold;">if</span><span style="color:#808030;">(</span>i<span style="color:#808030;">&amp;</span><span style="color:#808030;">(</span><span style="color:#008c00;">1</span><span style="color:#808030;">&lt;</span><span style="color:#808030;">&lt;</span>k<span style="color:#808030;">)</span><span style="color:#808030;">)</span> <span style="color:#800000;font-weight:bold;">break</span><span style="color:#800080;">;</span>
    <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> j<span style="color:#808030;">(</span>k<span style="color:#808030;">+</span><span style="color:#008c00;">1</span><span style="color:#808030;">)</span><span style="color:#800080;">;</span>j<span style="color:#808030;">&lt;</span>n<span style="color:#800080;">;</span>j<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span> <span style="color:#800000;font-weight:bold;">if</span><span style="color:#808030;">(</span>i<span style="color:#808030;">&amp;</span><span style="color:#808030;">(</span><span style="color:#008c00;">1</span><span style="color:#808030;">&lt;</span><span style="color:#808030;">&lt;</span>j<span style="color:#808030;">)</span><span style="color:#808030;">)</span> f<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">=</span><span style="color:#603000;">min</span><span style="color:#808030;">(</span>f<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">,</span>dis<span style="color:#808030;">(</span>k<span style="color:#808030;">,</span>j<span style="color:#808030;">)</span><span style="color:#808030;">+</span>f<span style="color:#808030;">[</span>i<span style="color:#808030;">^</span><span style="color:#808030;">(</span><span style="color:#008c00;">1</span><span style="color:#808030;">&lt;</span><span style="color:#808030;">&lt;</span>j<span style="color:#808030;">)</span><span style="color:#808030;">^</span><span style="color:#808030;">(</span><span style="color:#008c00;">1</span><span style="color:#808030;">&lt;</span><span style="color:#808030;">&lt;</span>k<span style="color:#808030;">)</span><span style="color:#808030;">]</span><span style="color:#808030;">)</span><span style="color:#800080;">;</span>
    <span style="color:#800080;">}</span>
    <span style="color:#603000;">printf</span><span style="color:#808030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%.2lf</span><span style="color:#800000;">"</span><span style="color:#808030;">,</span>f<span style="color:#808030;">[</span><span style="color:#808030;">(</span><span style="color:#008c00;">1</span><span style="color:#808030;">&lt;</span><span style="color:#808030;">&lt;</span>n<span style="color:#808030;">)</span><span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">)</span><span style="color:#800080;">;</span>

    <span style="color:#800000;font-weight:bold;">return</span> <span style="color:#008c00;">0</span><span style="color:#800080;">;</span>
<span style="color:#800080;">}</span></pre>


代码本身没有什么亮点，但有一处值得注意，当遇到集合DP时可以考虑使用二进制代表集合。