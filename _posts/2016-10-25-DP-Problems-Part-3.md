---
layout: post
title: DP Problems Part 3
categories: [NOI, 动态规划]
description: 老文章
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

## 样例输出

5

## 来源

经典题目

## 上传者

[张云聪](http://acm.nyist.net/JudgeOnline/profile.php?userid=%E5%BC%A0%E4%BA%91%E8%81%AA)

代码（这里提供两份，一份记忆化搜索，一份DAG最长路标准套路）：

<pre style="color:#000000;background:transparent;"><span style="color:#004a43;">#</span><span style="color:#004a43;">include</span><span style="color:#800000;">&lt;</span><span style="color:#40015a;">bits/stdc++.h</span><span style="color:#800000;">&gt;</span>
<span style="color:#800000;font-weight:bold;">using</span> <span style="color:#800000;font-weight:bold;">namespace</span> <span style="color:#666616;">std</span><span style="color:#800080;">;</span>

<span style="color:#800000;font-weight:bold;">const</span> <span style="color:#800000;font-weight:bold;">int</span> up<span style="color:#808030;">=</span><span style="color:#008c00;">1000</span> <span style="color:#808030;">+</span><span style="color:#008c00;">5</span><span style="color:#800080;">;</span>
<span style="color:#800000;font-weight:bold;">struct</span> matrix
<span style="color:#800080;">{</span>
    <span style="color:#800000;font-weight:bold;">int</span> h<span style="color:#808030;">,</span>w<span style="color:#800080;">;</span>
<span style="color:#800080;">}</span> a<span style="color:#808030;">[</span>up<span style="color:#808030;">]</span><span style="color:#800080;">;</span>
<span style="color:#800000;font-weight:bold;">int</span> f<span style="color:#808030;">[</span>up<span style="color:#808030;">]</span><span style="color:#808030;">,</span>n<span style="color:#800080;">;</span>
<span style="color:#800000;font-weight:bold;">int</span> fi<span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> x<span style="color:#808030;">)</span>
<span style="color:#800080;">{</span>
    <span style="color:#800000;font-weight:bold;">if</span><span style="color:#808030;">(</span>f<span style="color:#808030;">[</span>x<span style="color:#808030;">]</span><span style="color:#808030;">)</span> <span style="color:#800000;font-weight:bold;">return</span> f<span style="color:#808030;">[</span>x<span style="color:#808030;">]</span><span style="color:#800080;">;</span>
    <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> j<span style="color:#808030;">=</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>j<span style="color:#808030;">&lt;</span><span style="color:#808030;">=</span>n<span style="color:#800080;">;</span>j<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span>         
    <span style="color:#800000;font-weight:bold;">if</span><span style="color:#808030;">(</span>j<span style="color:#808030;">=</span><span style="color:#808030;">=</span>x<span style="color:#808030;">)</span> <span style="color:#800000;font-weight:bold;">continue</span><span style="color:#800080;">;</span>         
        <span style="color:#800000;font-weight:bold;">else</span> <span style="color:#800000;font-weight:bold;">if</span><span style="color:#808030;">(</span><span style="color:#808030;">(</span>a<span style="color:#808030;">[</span>x<span style="color:#808030;">]</span><span style="color:#808030;">.</span>w<span style="color:#808030;">&gt;</span>a<span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#808030;">.</span>w <span style="color:#808030;">&amp;</span><span style="color:#808030;">&amp;</span> a<span style="color:#808030;">[</span>x<span style="color:#808030;">]</span><span style="color:#808030;">.</span>h<span style="color:#808030;">&gt;</span>a<span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#808030;">.</span>h<span style="color:#808030;">)</span> <span style="color:#808030;">|</span><span style="color:#808030;">|</span> <span style="color:#808030;">(</span>a<span style="color:#808030;">[</span>x<span style="color:#808030;">]</span><span style="color:#808030;">.</span>h<span style="color:#808030;">&gt;</span>a<span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#808030;">.</span>w <span style="color:#808030;">&amp;</span><span style="color:#808030;">&amp;</span> a<span style="color:#808030;">[</span>x<span style="color:#808030;">]</span><span style="color:#808030;">.</span>w<span style="color:#808030;">&gt;</span>a<span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#808030;">.</span>h<span style="color:#808030;">)</span><span style="color:#808030;">)</span>
            f<span style="color:#808030;">[</span>x<span style="color:#808030;">]</span><span style="color:#808030;">=</span><span style="color:#603000;">max</span><span style="color:#808030;">(</span>f<span style="color:#808030;">[</span>x<span style="color:#808030;">]</span><span style="color:#808030;">,</span>fi<span style="color:#808030;">(</span>j<span style="color:#808030;">)</span><span style="color:#808030;">+</span><span style="color:#008c00;">1</span><span style="color:#808030;">)</span><span style="color:#800080;">;</span>
    <span style="color:#800000;font-weight:bold;">return</span> f<span style="color:#808030;">[</span>x<span style="color:#808030;">]</span><span style="color:#800080;">;</span>
<span style="color:#800080;">}</span>

<span style="color:#800000;font-weight:bold;">int</span> <span style="color:#400000;">main</span><span style="color:#808030;">(</span><span style="color:#808030;">)</span>
<span style="color:#800080;">{</span>
    <span style="color:#800000;font-weight:bold;">int</span> N<span style="color:#808030;">,</span>x<span style="color:#808030;">,</span>y<span style="color:#808030;">,</span>maxn<span style="color:#800080;">;</span>

    <span style="color:#603000;">scanf</span><span style="color:#808030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%d</span><span style="color:#800000;">"</span><span style="color:#808030;">,</span><span style="color:#808030;">&amp;</span>N<span style="color:#808030;">)</span><span style="color:#800080;">;</span>
    <span style="color:#800000;font-weight:bold;">while</span><span style="color:#808030;">(</span>N<span style="color:#808030;">-</span><span style="color:#808030;">-</span><span style="color:#808030;">)</span>
    <span style="color:#800080;">{</span>
        <span style="color:#603000;">scanf</span><span style="color:#808030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%d</span><span style="color:#800000;">"</span><span style="color:#808030;">,</span><span style="color:#808030;">&amp;</span>n<span style="color:#808030;">)</span><span style="color:#800080;">;</span>maxn<span style="color:#808030;">=</span><span style="color:#008c00;">0</span><span style="color:#800080;">;</span><span style="color:#603000;">memset</span><span style="color:#808030;">(</span>f<span style="color:#808030;">,</span><span style="color:#008c00;">0</span><span style="color:#808030;">,</span><span style="color:#800000;font-weight:bold;">sizeof</span><span style="color:#808030;">(</span>f<span style="color:#808030;">)</span><span style="color:#808030;">)</span><span style="color:#800080;">;</span>
        <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> i<span style="color:#808030;">=</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>i<span style="color:#808030;">&lt;</span><span style="color:#808030;">=</span>n<span style="color:#800080;">;</span>i<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span> <span style="color:#603000;">scanf</span><span style="color:#808030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%d</span> <span style="color:#007997;">%d</span><span style="color:#800000;">"</span><span style="color:#808030;">,</span><span style="color:#808030;">&amp;</span>a<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">.</span>h<span style="color:#808030;">,</span><span style="color:#808030;">&amp;</span>a<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">.</span>w<span style="color:#808030;">)</span><span style="color:#800080;">;</span>
        <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> i<span style="color:#808030;">=</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>i<span style="color:#808030;">&lt;</span><span style="color:#808030;">=</span>n<span style="color:#800080;">;</span>i<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span> maxn<span style="color:#808030;">=</span><span style="color:#603000;">max</span><span style="color:#808030;">(</span>maxn<span style="color:#808030;">,</span>fi<span style="color:#808030;">(</span>i<span style="color:#808030;">)</span><span style="color:#808030;">)</span><span style="color:#800080;">;</span>
        <span style="color:#603000;">printf</span><span style="color:#808030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%d</span><span style="color:#0f69ff;">\n</span><span style="color:#800000;">"</span><span style="color:#808030;">,</span>maxn<span style="color:#808030;">+</span><span style="color:#008c00;">1</span><span style="color:#808030;">)</span><span style="color:#800080;">;</span>
    <span style="color:#800080;">}</span>

    <span style="color:#800000;font-weight:bold;">return</span> <span style="color:#008c00;">0</span><span style="color:#800080;">;</span>
<span style="color:#800080;">}</span></pre>


<pre style="color:#000000;background:transparent;"><span style="color:#004a43;">#</span><span style="color:#004a43;">include</span><span style="color:#800000;">&lt;</span><span style="color:#40015a;">bits/stdc++.h</span><span style="color:#800000;">&gt;</span>
<span style="color:#800000;font-weight:bold;">using</span> <span style="color:#800000;font-weight:bold;">namespace</span> <span style="color:#666616;">std</span><span style="color:#800080;">;</span>

<span style="color:#800000;font-weight:bold;">const</span> <span style="color:#800000;font-weight:bold;">int</span> up<span style="color:#808030;">=</span><span style="color:#008c00;">1000</span> <span style="color:#808030;">+</span><span style="color:#008c00;">5</span><span style="color:#800080;">;</span>
<span style="color:#800000;font-weight:bold;">struct</span> matrix
<span style="color:#800080;">{</span>
    <span style="color:#800000;font-weight:bold;">int</span> h<span style="color:#808030;">,</span>w<span style="color:#800080;">;</span>
<span style="color:#800080;">}</span> a<span style="color:#808030;">[</span>up<span style="color:#808030;">]</span><span style="color:#800080;">;</span>
<span style="color:#800000;font-weight:bold;">int</span> f<span style="color:#808030;">[</span>up<span style="color:#808030;">]</span><span style="color:#800080;">;</span>
<span style="color:#800000;font-weight:bold;">bool</span> cmp<span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">const</span> matrix<span style="color:#808030;">&amp;</span> x<span style="color:#808030;">,</span><span style="color:#800000;font-weight:bold;">const</span> matrix<span style="color:#808030;">&amp;</span> y<span style="color:#808030;">)</span>
<span style="color:#800080;">{</span>
    <span style="color:#800000;font-weight:bold;">return</span> x<span style="color:#808030;">.</span>h<span style="color:#808030;">&lt;</span>y<span style="color:#808030;">.</span>h<span style="color:#800080;">;</span>
<span style="color:#800080;">}</span>

<span style="color:#800000;font-weight:bold;">int</span> <span style="color:#400000;">main</span><span style="color:#808030;">(</span><span style="color:#808030;">)</span>
<span style="color:#800080;">{</span>
    <span style="color:#800000;font-weight:bold;">int</span> N<span style="color:#808030;">,</span>n<span style="color:#808030;">,</span>x<span style="color:#808030;">,</span>y<span style="color:#808030;">,</span>maxn<span style="color:#800080;">;</span>

    <span style="color:#603000;">scanf</span><span style="color:#808030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%d</span><span style="color:#800000;">"</span><span style="color:#808030;">,</span><span style="color:#808030;">&amp;</span>N<span style="color:#808030;">)</span><span style="color:#800080;">;</span>
    <span style="color:#800000;font-weight:bold;">while</span><span style="color:#808030;">(</span>N<span style="color:#808030;">-</span><span style="color:#808030;">-</span><span style="color:#808030;">)</span>
    <span style="color:#800080;">{</span>
        <span style="color:#603000;">scanf</span><span style="color:#808030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%d</span><span style="color:#800000;">"</span><span style="color:#808030;">,</span><span style="color:#808030;">&amp;</span>n<span style="color:#808030;">)</span><span style="color:#800080;">;</span>maxn<span style="color:#808030;">=</span><span style="color:#008c00;">0</span><span style="color:#800080;">;</span>
        <span style="color:#603000;">memset</span><span style="color:#808030;">(</span>f<span style="color:#808030;">,</span><span style="color:#008c00;">0</span><span style="color:#808030;">,</span><span style="color:#800000;font-weight:bold;">sizeof</span> f<span style="color:#808030;">)</span><span style="color:#800080;">;</span>
        <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> i<span style="color:#808030;">=</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>i<span style="color:#808030;">&lt;</span><span style="color:#808030;">=</span>n<span style="color:#800080;">;</span>i<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span>         
        <span style="color:#800080;">{</span>             
            <span style="color:#603000;">scanf</span><span style="color:#808030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%d</span> <span style="color:#007997;">%d</span><span style="color:#800000;">"</span><span style="color:#808030;">,</span><span style="color:#808030;">&amp;</span>x<span style="color:#808030;">,</span><span style="color:#808030;">&amp;</span>y<span style="color:#808030;">)</span><span style="color:#800080;">;</span>             
            <span style="color:#800000;font-weight:bold;">if</span><span style="color:#808030;">(</span>x<span style="color:#808030;">&gt;</span>y<span style="color:#808030;">)</span> a<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">.</span>h<span style="color:#808030;">=</span>y<span style="color:#808030;">,</span>a<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">.</span>w<span style="color:#808030;">=</span>x<span style="color:#800080;">;</span>
            <span style="color:#800000;font-weight:bold;">else</span> a<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">.</span>h<span style="color:#808030;">=</span>x<span style="color:#808030;">,</span>a<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">.</span>w<span style="color:#808030;">=</span>y<span style="color:#800080;">;</span>
        <span style="color:#800080;">}</span>
        <span style="color:#603000;">sort</span><span style="color:#808030;">(</span>a<span style="color:#808030;">+</span><span style="color:#008c00;">1</span><span style="color:#808030;">,</span>a<span style="color:#808030;">+</span>n<span style="color:#808030;">+</span><span style="color:#008c00;">1</span><span style="color:#808030;">,</span>cmp<span style="color:#808030;">)</span><span style="color:#800080;">;</span>
        <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> i<span style="color:#808030;">=</span><span style="color:#008c00;">2</span><span style="color:#800080;">;</span>i<span style="color:#808030;">&lt;</span><span style="color:#808030;">=</span>n<span style="color:#800080;">;</span>i<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span>
            <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> j<span style="color:#808030;">=</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>j<span style="color:#808030;">&lt;</span>i<span style="color:#800080;">;</span>j<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span>                 
                <span style="color:#800000;font-weight:bold;">if</span><span style="color:#808030;">(</span>a<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">.</span>w<span style="color:#808030;">&gt;</span>a<span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#808030;">.</span>w <span style="color:#808030;">&amp;</span><span style="color:#808030;">&amp;</span> a<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">.</span>h<span style="color:#808030;">&gt;</span>a<span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#808030;">.</span>h<span style="color:#808030;">)</span> f<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">=</span><span style="color:#603000;">max</span><span style="color:#808030;">(</span>f<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">,</span>f<span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#808030;">+</span><span style="color:#008c00;">1</span><span style="color:#808030;">)</span><span style="color:#800080;">;</span>
        <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> i<span style="color:#808030;">=</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>i<span style="color:#808030;">&lt;</span><span style="color:#808030;">=</span>n<span style="color:#800080;">;</span>i<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span> maxn<span style="color:#808030;">=</span><span style="color:#603000;">max</span><span style="color:#808030;">(</span>maxn<span style="color:#808030;">,</span>f<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">)</span><span style="color:#800080;">;</span>
        <span style="color:#603000;">printf</span><span style="color:#808030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%d</span><span style="color:#0f69ff;">\n</span><span style="color:#800000;">"</span><span style="color:#808030;">,</span>maxn<span style="color:#808030;">+</span><span style="color:#008c00;">1</span><span style="color:#808030;">)</span><span style="color:#800080;">;</span>
    <span style="color:#800080;">}</span>
    <span style="color:#800000;font-weight:bold;">return</span> <span style="color:#008c00;">0</span><span style="color:#800080;">;</span>
<span style="color:#800080;">}</span></pre>


# 2.硬币问题

## 描述

有n种硬币，面值分别为V1,V2,...Vn,每种都有无限多。给定非负整数S，可以选用多少个硬币，使得面值之和恰好为S？输出硬币数目的最小值和最大值。

## 输入

第一行是两个数n，S，1&lt;=n&lt;=100，0&lt;=S&lt;=10000；接下来n行是每一种硬币的面值Vi，1&lt;=Vi&lt;=S。

## 输出

两行各一个整数，第一行是硬币数目最小值，第二行是硬币数目最大值。

## 样例输入

5 10
1
2
4
5
7

## 样例输出

2
10

## 来源

ACM常见模型：DAG最长最短路，也可以看成完全背包。

代码：

<pre style="color:#000000;background:transparent;"><span style="color:#004a43;">#</span><span style="color:#004a43;">include</span><span style="color:#800000;">&lt;</span><span style="color:#40015a;">bits/stdc++.h</span><span style="color:#800000;">&gt;</span>
<span style="color:#800000;font-weight:bold;">using</span> <span style="color:#800000;font-weight:bold;">namespace</span> <span style="color:#666616;">std</span><span style="color:#800080;">;</span>

<span style="color:#800000;font-weight:bold;">const</span> <span style="color:#800000;font-weight:bold;">int</span> up1<span style="color:#808030;">=</span><span style="color:#008c00;">10000</span> <span style="color:#808030;">+</span><span style="color:#008c00;">5</span><span style="color:#808030;">,</span>up2<span style="color:#808030;">=</span><span style="color:#008c00;">100</span> <span style="color:#808030;">+</span><span style="color:#008c00;">5</span><span style="color:#808030;">,</span>inf<span style="color:#808030;">=</span><span style="color:#008000;">0x3f3f3f3f</span><span style="color:#800080;">;</span>
<span style="color:#800000;font-weight:bold;">int</span> f<span style="color:#808030;">[</span>up1<span style="color:#808030;">]</span><span style="color:#808030;">,</span>g<span style="color:#808030;">[</span>up1<span style="color:#808030;">]</span><span style="color:#800080;">;</span>
<span style="color:#800000;font-weight:bold;">int</span> V<span style="color:#808030;">[</span>up2<span style="color:#808030;">]</span><span style="color:#800080;">;</span>

<span style="color:#800000;font-weight:bold;">int</span> <span style="color:#400000;">main</span><span style="color:#808030;">(</span><span style="color:#808030;">)</span>
<span style="color:#800080;">{</span>
    <span style="color:#800000;font-weight:bold;">int</span> n<span style="color:#808030;">,</span>S<span style="color:#808030;">,</span>maxn<span style="color:#800080;">;</span>

    <span style="color:#603000;">scanf</span><span style="color:#808030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%d</span> <span style="color:#007997;">%d</span><span style="color:#800000;">"</span><span style="color:#808030;">,</span><span style="color:#808030;">&amp;</span>n<span style="color:#808030;">,</span><span style="color:#808030;">&amp;</span>S<span style="color:#808030;">)</span><span style="color:#800080;">;</span>
    <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> i<span style="color:#808030;">=</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>i<span style="color:#808030;">&lt;</span><span style="color:#808030;">=</span>S<span style="color:#800080;">;</span>i<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span> f<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">=</span>inf<span style="color:#808030;">,</span>g<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">=</span><span style="color:#808030;">-</span>inf<span style="color:#800080;">;</span>
    <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> i<span style="color:#808030;">=</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>i<span style="color:#808030;">&lt;</span><span style="color:#808030;">=</span>n<span style="color:#800080;">;</span>i<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span>
    <span style="color:#800080;">{</span>
        <span style="color:#603000;">scanf</span><span style="color:#808030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%d</span><span style="color:#800000;">"</span><span style="color:#808030;">,</span><span style="color:#808030;">&amp;</span>V<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">)</span><span style="color:#800080;">;</span>
        <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> j<span style="color:#808030;">=</span>V<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#800080;">;</span>j<span style="color:#808030;">&lt;</span><span style="color:#808030;">=</span>S<span style="color:#800080;">;</span>j<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span> 
            f<span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#808030;">=</span><span style="color:#603000;">min</span><span style="color:#808030;">(</span>f<span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#808030;">,</span>f<span style="color:#808030;">[</span>j<span style="color:#808030;">-</span>V<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">]</span><span style="color:#808030;">+</span><span style="color:#008c00;">1</span><span style="color:#808030;">)</span><span style="color:#808030;">,</span>g<span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#808030;">=</span><span style="color:#603000;">max</span><span style="color:#808030;">(</span>g<span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#808030;">,</span>g<span style="color:#808030;">[</span>j<span style="color:#808030;">-</span>V<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">]</span><span style="color:#808030;">+</span><span style="color:#008c00;">1</span><span style="color:#808030;">)</span><span style="color:#800080;">;</span>
    <span style="color:#800080;">}</span>
    <span style="color:#603000;">printf</span><span style="color:#808030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%d</span><span style="color:#0f69ff;">\n</span><span style="color:#007997;">%d</span><span style="color:#800000;">"</span><span style="color:#808030;">,</span>f<span style="color:#808030;">[</span>S<span style="color:#808030;">]</span><span style="color:#808030;">,</span>g<span style="color:#808030;">[</span>S<span style="color:#808030;">]</span><span style="color:#808030;">)</span><span style="color:#800080;">;</span>
    <span style="color:#800000;font-weight:bold;">return</span> <span style="color:#008c00;">0</span><span style="color:#800080;">;</span>
<span style="color:#800080;">}</span></pre>


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

6

1 1 2 1 4 3

## 输出样例

5

## 数据规模

30%：N&lt;1000

100%：N0&lt;P&lt;=100

代码：

<pre style="color:#000000;background:transparent;"><span style="color:#004a43;">#</span><span style="color:#004a43;">include</span><span style="color:#800000;">&lt;</span><span style="color:#40015a;">bits/stdc++.h</span><span style="color:#800000;">&gt;</span>
<span style="color:#800000;font-weight:bold;">using</span> <span style="color:#800000;font-weight:bold;">namespace</span> <span style="color:#666616;">std</span><span style="color:#800080;">;</span>

<span style="color:#800000;font-weight:bold;">int</span> f<span style="color:#808030;">[</span><span style="color:#008c00;">100005</span><span style="color:#808030;">]</span><span style="color:#800080;">;</span>
<span style="color:#800000;font-weight:bold;">int</span> a<span style="color:#808030;">[</span><span style="color:#008c00;">105</span><span style="color:#808030;">]</span><span style="color:#800080;">;</span>

<span style="color:#800000;font-weight:bold;">int</span> <span style="color:#400000;">main</span><span style="color:#808030;">(</span><span style="color:#808030;">)</span>
<span style="color:#800080;">{</span>
    <span style="color:#800000;font-weight:bold;">int</span> n<span style="color:#808030;">,</span>maxn<span style="color:#808030;">=</span><span style="color:#008c00;">0</span><span style="color:#808030;">,</span>x<span style="color:#800080;">;</span>

    <span style="color:#603000;">cin</span><span style="color:#808030;">&gt;</span><span style="color:#808030;">&gt;</span>n<span style="color:#800080;">;</span>
    <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> i<span style="color:#808030;">=</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>i<span style="color:#808030;">&lt;</span><span style="color:#808030;">=</span>n<span style="color:#800080;">;</span>i<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span> f<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">=</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>
    <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> i<span style="color:#808030;">=</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>i<span style="color:#808030;">&lt;</span><span style="color:#808030;">=</span>n<span style="color:#800080;">;</span>i<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span>          
<span style="color:#800080;">    {</span>                  
<span style="color:#603000;">        scanf</span><span style="color:#808030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%d</span><span style="color:#800000;">"</span><span style="color:#808030;">,</span><span style="color:#808030;">&amp;</span>x<span style="color:#808030;">)</span><span style="color:#800080;">;</span>                  
<span style="color:#800000;font-weight:bold;">        for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> j<span style="color:#808030;">=</span><span style="color:#603000;">min</span><span style="color:#808030;">(</span>i<span style="color:#808030;">,</span><span style="color:#008c00;">100</span><span style="color:#808030;">)</span><span style="color:#800080;">;</span>j<span style="color:#808030;">&gt;</span><span style="color:#808030;">=</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>j<span style="color:#808030;">-</span><span style="color:#808030;">-</span><span style="color:#808030;">)</span> <span style="color:#800000;font-weight:bold;">if</span><span style="color:#808030;">(</span>i<span style="color:#808030;">%</span>j<span style="color:#808030;">=</span><span style="color:#808030;">=</span><span style="color:#008c00;">0</span><span style="color:#808030;">)</span> f<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">=</span><span style="color:#603000;">max</span><span style="color:#808030;">(</span>f<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">,</span>a<span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#808030;">+</span><span style="color:#008c00;">1</span><span style="color:#808030;">)</span><span style="color:#800080;">;</span>
        a<span style="color:#808030;">[</span>x<span style="color:#808030;">]</span><span style="color:#808030;">=</span><span style="color:#603000;">max</span><span style="color:#808030;">(</span>a<span style="color:#808030;">[</span>x<span style="color:#808030;">]</span><span style="color:#808030;">,</span>f<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">)</span><span style="color:#800080;">;</span>
        maxn<span style="color:#808030;">=</span><span style="color:#603000;">max</span><span style="color:#808030;">(</span>maxn<span style="color:#808030;">,</span>f<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">)</span><span style="color:#800080;">;</span>
    <span style="color:#800080;">}</span>
    <span style="color:#603000;">printf</span><span style="color:#808030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%d</span><span style="color:#0f69ff;">\n</span><span style="color:#800000;">"</span><span style="color:#808030;">,</span>maxn<span style="color:#808030;">)</span><span style="color:#800080;">;</span>

    <span style="color:#800000;font-weight:bold;">return</span> <span style="color:#008c00;">0</span><span style="color:#800080;">;</span>
<span style="color:#800080;">}</span></pre>


同样是DAG最长路，但又有一些改变，首先是状态转移的改变，其次是策略的改变。

当同样的数作为状态推出最优解时，只需考虑同一个数中的链较长的一个，因为比它小的就一定不是最优解。

若以f[i]表示以i为尾最长的信任链，那么可以再声明a[p]表示在i之前值为p的最长信任链的长度。