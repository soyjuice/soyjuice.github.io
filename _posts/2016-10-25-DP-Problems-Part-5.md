---
layout: post
title: 动态规划专练（五）
categories: [NOI, 动态规划]
description: 老文章
keywords: C++, 动态规划
---

# 1.最长公共子序列(LCS)

时间限制：3000 ms | 内存限制：65535 KB
难度：3 |  提供网站：NYOJ (稍有改动)

## 描述

咱们就不拐弯抹角了，如题，需要你做的就是写一个程序，得出最长公共子序列。
tip：最长公共子序列也称作最长公共子串(不要求连续)，英文缩写为LCS（Longest Common Subsequence）。其定义是，一个序列 S ，如果分别是两个或多个已知序列的子序列，且是所有符合此条件序列中最长的，则 S 称为已知序列的最长公共子序列。
<!--more-->
## 输入

第一行给出一个整数N(0&lt;N&lt;100)表示待测数据组数
接下来每组数据两行，分别为待测的两组字符串。每个字符串长度不大于5000.

## 输出

每组测试数据输出一个整数，表示最长公共子序列长度。每组结果占一行。

## 样例输入

```
2
asdf
adfsd
123abc
abc123abc
```

## 样例输出

```
3
6
```

代码：

<pre style="color:#000000;background:transparent;"><span style="color:#004a43;">#</span><span style="color:#004a43;">include</span><span style="color:#800000;">&lt;</span><span style="color:#40015a;">bits/stdc++.h</span><span style="color:#800000;">&gt;</span>
<span style="color:#800000;font-weight:bold;">using</span> <span style="color:#800000;font-weight:bold;">namespace</span> <span style="color:#666616;">std</span><span style="color:#800080;">;</span>

<span style="color:#800000;font-weight:bold;">const</span> <span style="color:#800000;font-weight:bold;">int</span> up<span style="color:#808030;">=</span><span style="color:#008c00;">5000</span> <span style="color:#808030;">+</span><span style="color:#008c00;">5</span><span style="color:#800080;">;</span>
<span style="color:#800000;font-weight:bold;">char</span> a<span style="color:#808030;">[</span>up<span style="color:#808030;">]</span><span style="color:#808030;">,</span>b<span style="color:#808030;">[</span>up<span style="color:#808030;">]</span><span style="color:#800080;">;</span><span style="color:#800000;font-weight:bold;">int</span> k<span style="color:#808030;">,</span>l<span style="color:#808030;">,</span>f<span style="color:#808030;">[</span><span style="color:#008c00;">2</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span>up<span style="color:#808030;">]</span><span style="color:#808030;">,</span>T<span style="color:#800080;">;</span>

<span style="color:#800000;font-weight:bold;">int</span> <span style="color:#400000;">main</span><span style="color:#808030;">(</span><span style="color:#808030;">)</span>
<span style="color:#800080;">{</span>
    <span style="color:#603000;">scanf</span><span style="color:#808030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%d</span><span style="color:#800000;">"</span><span style="color:#808030;">,</span><span style="color:#808030;">&amp;</span>T<span style="color:#808030;">)</span><span style="color:#800080;">;</span>
    <span style="color:#800000;font-weight:bold;">while</span><span style="color:#808030;">(</span>T<span style="color:#808030;">-</span><span style="color:#808030;">-</span><span style="color:#808030;">)</span>
    <span style="color:#800080;">{</span>
        <span style="color:#603000;">memset</span><span style="color:#808030;">(</span>f<span style="color:#808030;">[</span><span style="color:#008c00;">0</span><span style="color:#808030;">]</span><span style="color:#808030;">,</span><span style="color:#008c00;">0</span><span style="color:#808030;">,</span><span style="color:#800000;font-weight:bold;">sizeof</span> f<span style="color:#808030;">[</span><span style="color:#008c00;">0</span><span style="color:#808030;">]</span><span style="color:#808030;">)</span><span style="color:#800080;">;</span>
        <span style="color:#603000;">memset</span><span style="color:#808030;">(</span>f<span style="color:#808030;">[</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">,</span><span style="color:#008c00;">0</span><span style="color:#808030;">,</span><span style="color:#800000;font-weight:bold;">sizeof</span> f<span style="color:#808030;">[</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">)</span><span style="color:#800080;">;</span>
        <span style="color:#603000;">scanf</span><span style="color:#808030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%s</span> <span style="color:#007997;">%s</span><span style="color:#800000;">"</span><span style="color:#808030;">,</span>a<span style="color:#808030;">+</span><span style="color:#008c00;">1</span><span style="color:#808030;">,</span>b<span style="color:#808030;">+</span><span style="color:#008c00;">1</span><span style="color:#808030;">)</span><span style="color:#800080;">;</span>
        k<span style="color:#808030;">=</span><span style="color:#603000;">strlen</span><span style="color:#808030;">(</span>a<span style="color:#808030;">+</span><span style="color:#008c00;">1</span><span style="color:#808030;">)</span><span style="color:#808030;">,</span>l<span style="color:#808030;">=</span><span style="color:#603000;">strlen</span><span style="color:#808030;">(</span>b<span style="color:#808030;">+</span><span style="color:#008c00;">1</span><span style="color:#808030;">)</span><span style="color:#800080;">;</span>
        <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> i<span style="color:#808030;">=</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>i<span style="color:#808030;">&lt;</span><span style="color:#808030;">=</span>k<span style="color:#800080;">;</span>i<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span>
            <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> j<span style="color:#808030;">=</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>j<span style="color:#808030;">&lt;</span><span style="color:#808030;">=</span>l<span style="color:#800080;">;</span>j<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span>
                <span style="color:#800000;font-weight:bold;">if</span><span style="color:#808030;">(</span>a<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">=</span><span style="color:#808030;">=</span>b<span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#808030;">)</span> f<span style="color:#808030;">[</span>i<span style="color:#808030;">&amp;</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#808030;">=</span>f<span style="color:#808030;">[</span><span style="color:#808030;">(</span>i<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">)</span><span style="color:#808030;">&amp;</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span>j<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">+</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>
                <span style="color:#800000;font-weight:bold;">else</span> f<span style="color:#808030;">[</span>i<span style="color:#808030;">&amp;</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#808030;">=</span><span style="color:#603000;">max</span><span style="color:#808030;">(</span>f<span style="color:#808030;">[</span><span style="color:#808030;">(</span>i<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">)</span><span style="color:#808030;">&amp;</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#808030;">,</span>f<span style="color:#808030;">[</span>i<span style="color:#808030;">&amp;</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span>j<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">)</span><span style="color:#800080;">;</span>
        <span style="color:#603000;">printf</span><span style="color:#808030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%d</span><span style="color:#0f69ff;">\n</span><span style="color:#800000;">"</span><span style="color:#808030;">,</span>f<span style="color:#808030;">[</span>k<span style="color:#808030;">&amp;</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span>l<span style="color:#808030;">]</span><span style="color:#808030;">)</span><span style="color:#800080;">;</span>
    <span style="color:#800080;">}</span>

    <span style="color:#800000;font-weight:bold;">return</span> <span style="color:#008c00;">0</span><span style="color:#800080;">;</span>
<span style="color:#800080;">}</span></pre>


如果是直接开5000*5000的数组，内存是不够的，所以要用滚动数组进行优化。

用非常常用的k&amp;1优化，第一维保留这一排与上一排的状态，根据最长公共子序列问题的动态转移方程：如果a[i]=a[j]，f[i,j]=f[i-1,j-1]+1；否则，f[i,j]=max(f[i-1,j],f[i,j-1])。可以变成上面的

**if(a[i]==b[j]) f[i&amp;1][j]=f[(i-1)&amp;1][j-1]+1;
else f[i&amp;1][j]=max(f[(i-1)&amp;1][j],f[i&amp;1][j-1]);**

# 2.最长上升子序列(LIS)

时间限制：3000 ms | 内存限制：65535 KB
难度：4 | 提供网站：NYOJ

## 描述

求一个字符串的最长递增子序列的长度
如：dabdbf最长递增子序列就是abdf，长度为4

## 输入

第一行一个整数0&lt;n&lt;20,表示有n个字符串要处理
随后的n行，每行有一个字符串，该字符串的长度不会超过10000

## 输出

输出字符串的最长递增子序列的长度

## 样例输入

```
3
aaa
ababc
abklmncdefg
```

## 样例输出

```
1
3
7
```

代码：

<pre style="color:#000000;background:transparent;"><span style="color:#004a43;">#</span><span style="color:#004a43;">include</span><span style="color:#800000;">&lt;</span><span style="color:#40015a;">bits/stdc++.h</span><span style="color:#800000;">&gt;</span>
<span style="color:#800000;font-weight:bold;">using</span> <span style="color:#800000;font-weight:bold;">namespace</span> <span style="color:#666616;">std</span><span style="color:#800080;">;</span>

<span style="color:#800000;font-weight:bold;">const</span> <span style="color:#800000;font-weight:bold;">int</span> up<span style="color:#808030;">=</span><span style="color:#008c00;">10000</span> <span style="color:#808030;">+</span><span style="color:#008c00;">5</span><span style="color:#800080;">;</span>
<span style="color:#800000;font-weight:bold;">int</span> T<span style="color:#808030;">,</span>f<span style="color:#808030;">[</span>up<span style="color:#808030;">]</span><span style="color:#808030;">,</span>g<span style="color:#808030;">[</span>up<span style="color:#808030;">]</span><span style="color:#800080;">;</span>
<span style="color:#800000;font-weight:bold;">char</span> a<span style="color:#808030;">[</span>up<span style="color:#808030;">]</span><span style="color:#800080;">;</span>

<span style="color:#800000;font-weight:bold;">int</span> <span style="color:#400000;">main</span><span style="color:#808030;">(</span><span style="color:#808030;">)</span>
<span style="color:#800080;">{</span>
    <span style="color:#800000;font-weight:bold;">int</span> k<span style="color:#808030;">,</span>l<span style="color:#808030;">,</span>maxn<span style="color:#808030;">=</span><span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>
    <span style="color:#603000;">scanf</span><span style="color:#808030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%d</span><span style="color:#800000;">"</span><span style="color:#808030;">,</span><span style="color:#808030;">&amp;</span>T<span style="color:#808030;">)</span><span style="color:#800080;">;</span>
    <span style="color:#800000;font-weight:bold;">while</span><span style="color:#808030;">(</span>T<span style="color:#808030;">-</span><span style="color:#808030;">-</span><span style="color:#808030;">)</span>
    <span style="color:#800080;">{</span>
        <span style="color:#603000;">memset</span><span style="color:#808030;">(</span>g<span style="color:#808030;">,</span><span style="color:#008000;">0x7f</span><span style="color:#808030;">,</span><span style="color:#800000;font-weight:bold;">sizeof</span> g<span style="color:#808030;">)</span><span style="color:#800080;">;</span>
        <span style="color:#603000;">memset</span><span style="color:#808030;">(</span>f<span style="color:#808030;">,</span><span style="color:#008c00;">0</span><span style="color:#808030;">,</span><span style="color:#800000;font-weight:bold;">sizeof</span> f<span style="color:#808030;">)</span><span style="color:#800080;">;</span>
        maxn<span style="color:#808030;">=</span><span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>
        <span style="color:#603000;">scanf</span><span style="color:#808030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%s</span><span style="color:#800000;">"</span><span style="color:#808030;">,</span>a<span style="color:#808030;">)</span><span style="color:#800080;">;</span>l<span style="color:#808030;">=</span><span style="color:#603000;">strlen</span><span style="color:#808030;">(</span>a<span style="color:#808030;">)</span><span style="color:#800080;">;</span>
        <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> i<span style="color:#808030;">=</span><span style="color:#008c00;">0</span><span style="color:#800080;">;</span>i<span style="color:#808030;">&lt;</span>l<span style="color:#800080;">;</span>i<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span>
        <span style="color:#800080;">{</span>
            k<span style="color:#808030;">=</span><span style="color:#603000;">lower_bound</span><span style="color:#808030;">(</span>g<span style="color:#808030;">+</span><span style="color:#008c00;">1</span><span style="color:#808030;">,</span>g<span style="color:#808030;">+</span>l<span style="color:#808030;">+</span><span style="color:#008c00;">1</span><span style="color:#808030;">,</span>a<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">)</span><span style="color:#808030;">-</span>g<span style="color:#800080;">;</span>
            f<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">=</span>k<span style="color:#800080;">;</span>
            g<span style="color:#808030;">[</span>k<span style="color:#808030;">]</span><span style="color:#808030;">=</span>a<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#800080;">;</span>
            maxn<span style="color:#808030;">=</span><span style="color:#603000;">max</span><span style="color:#808030;">(</span>maxn<span style="color:#808030;">,</span>f<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">)</span><span style="color:#800080;">;</span>
        <span style="color:#800080;">}</span>
        <span style="color:#603000;">printf</span><span style="color:#808030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%d</span><span style="color:#0f69ff;">\n</span><span style="color:#800000;">"</span><span style="color:#808030;">,</span>maxn<span style="color:#808030;">)</span><span style="color:#800080;">;</span>
    <span style="color:#800080;">}</span>
    <span style="color:#800000;font-weight:bold;">return</span> <span style="color:#008c00;">0</span><span style="color:#800080;">;</span>
<span style="color:#800080;">}</span></pre>


假设有两个状态a,b满足Aa&lt;Ab且d(a)=d(b)，则对于后续所有的状态，b都不会比a更优。

因此，如果只保留a一定不会丢失最优解，设g(i)表示d值为i的最小状态，不断更新，二分查找。

# 3.最大连续和

## 题目描述 Description

给定一个长度为n的一个序列A1，A2，…，An，求序列中连续子序列的最大和。
例如：当输入为-5，3，5，7，-15，6，9，27，-36，10时，连续子序列6，9，27的和为42是最大值；而当序列变成-5，3，5，8，-15，6，9，27，-36，10时，连续子序列3，5，8，-15，6，9，27的和为43是最大值。

## 输入描述 Input Description

第一行为n (n≤1000)，第二行为n个数，表示序列Ai（-10000≤Ai≤10000）。

## 输出描述 Output Description

一个数，表示连续子序列的最大和。

## 样例输入 Sample Input

```
10
-5 3 5 8 -15 6 9 27 -36 10
```

## 样例输出 Sample Output

```
43
```

## 数据范围及提示 Data Size &amp; Hint

-10000≤Ai≤10000
n≤1000

代码：

<pre style="color:#000000;background:transparent;"><span style="color:#004a43;">#</span><span style="color:#004a43;">include</span><span style="color:#800000;">&lt;</span><span style="color:#40015a;">bits/stdc++.h</span><span style="color:#800000;">&gt;</span>
<span style="color:#800000;font-weight:bold;">using</span> <span style="color:#800000;font-weight:bold;">namespace</span> <span style="color:#666616;">std</span><span style="color:#800080;">;</span>

<span style="color:#800000;font-weight:bold;">const</span> <span style="color:#800000;font-weight:bold;">int</span> up<span style="color:#808030;">=</span><span style="color:#008c00;">1000</span> <span style="color:#808030;">+</span><span style="color:#008c00;">5</span><span style="color:#800080;">;</span>
<span style="color:#800000;font-weight:bold;">int</span> T<span style="color:#808030;">,</span>f<span style="color:#808030;">[</span>up<span style="color:#808030;">]</span><span style="color:#808030;">,</span>a<span style="color:#808030;">[</span>up<span style="color:#808030;">]</span><span style="color:#800080;">;</span>

<span style="color:#800000;font-weight:bold;">int</span> <span style="color:#400000;">main</span><span style="color:#808030;">(</span><span style="color:#808030;">)</span>
<span style="color:#800080;">{</span>
    <span style="color:#800000;font-weight:bold;">int</span> maxn<span style="color:#808030;">=</span><span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>
    <span style="color:#603000;">scanf</span><span style="color:#808030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%d</span><span style="color:#800000;">"</span><span style="color:#808030;">,</span><span style="color:#808030;">&amp;</span>T<span style="color:#808030;">)</span><span style="color:#800080;">;</span>
    <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> i<span style="color:#808030;">=</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>i<span style="color:#808030;">&lt;</span><span style="color:#808030;">=</span>T<span style="color:#800080;">;</span>i<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span>
    <span style="color:#800080;">{</span>
    <span style="color:#603000;">scanf</span><span style="color:#808030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%d</span><span style="color:#800000;">"</span><span style="color:#808030;">,</span><span style="color:#808030;">&amp;</span>a<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">)</span><span style="color:#800080;">;</span>
    f<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">=</span><span style="color:#603000;">max</span><span style="color:#808030;">(</span><span style="color:#008c00;">0</span><span style="color:#808030;">,</span>f<span style="color:#808030;">[</span>i<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">)</span><span style="color:#808030;">+</span>a<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#800080;">;</span>
    maxn<span style="color:#808030;">=</span><span style="color:#603000;">max</span><span style="color:#808030;">(</span>maxn<span style="color:#808030;">,</span>f<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">)</span><span style="color:#800080;">;</span>
    <span style="color:#800080;">}</span>
    <span style="color:#603000;">printf</span><span style="color:#808030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%d</span><span style="color:#0f69ff;">\n</span><span style="color:#800000;">"</span><span style="color:#808030;">,</span>maxn<span style="color:#808030;">)</span><span style="color:#800080;">;</span>

    <span style="color:#800000;font-weight:bold;">return</span> <span style="color:#008c00;">0</span><span style="color:#800080;">;</span>
<span style="color:#800080;">}</span></pre>
