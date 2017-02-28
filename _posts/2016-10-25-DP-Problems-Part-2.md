---
layout: post
title: DP Problems Part 2
categories: [NOI, 动态规划]
description: 老文章
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

 5
 7
 3 8
 8 1 0
 2 7 4 4
 4 5 2 6 5

### 输出

 30

## 备注

搜索80，记忆化AC。

代码：

<pre style="color:#000000;background:transparent;"><span style="color:#004a43;">#</span><span style="color:#004a43;">include</span><span style="color:#800000;">&lt;</span><span style="color:#40015a;">bits/stdc++.h</span><span style="color:#800000;">&gt;</span>
<span style="color:#800000;font-weight:bold;">using</span> <span style="color:#800000;font-weight:bold;">namespace</span> <span style="color:#666616;">std</span><span style="color:#800080;">;</span>

<span style="color:#800000;font-weight:bold;">const</span> <span style="color:#800000;font-weight:bold;">int</span> up<span style="color:#808030;">=</span><span style="color:#008c00;">30</span><span style="color:#800080;">;</span>

<span style="color:#800000;font-weight:bold;">int</span> <span style="color:#400000;">main</span><span style="color:#808030;">(</span><span style="color:#808030;">)</span> 
<span style="color:#800080;">{</span>
    <span style="color:#800000;font-weight:bold;">int</span> a<span style="color:#808030;">[</span>up<span style="color:#808030;">]</span><span style="color:#808030;">,</span>f<span style="color:#808030;">[</span>up<span style="color:#808030;">]</span><span style="color:#808030;">,</span>n<span style="color:#808030;">,</span>ans<span style="color:#808030;">=</span><span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>
    <span style="color:#603000;">memset</span><span style="color:#808030;">(</span>a<span style="color:#808030;">,</span><span style="color:#008c00;">0</span><span style="color:#808030;">,</span><span style="color:#800000;font-weight:bold;">sizeof</span> a<span style="color:#808030;">)</span><span style="color:#800080;">;</span>
    <span style="color:#603000;">memset</span><span style="color:#808030;">(</span>f<span style="color:#808030;">,</span><span style="color:#008c00;">0</span><span style="color:#808030;">,</span><span style="color:#800000;font-weight:bold;">sizeof</span> f<span style="color:#808030;">)</span><span style="color:#800080;">;</span>

    <span style="color:#603000;">cin</span><span style="color:#808030;">&gt;</span><span style="color:#808030;">&gt;</span>n<span style="color:#800080;">;</span>
    <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> i<span style="color:#808030;">=</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>i<span style="color:#808030;">&lt;</span><span style="color:#808030;">=</span>n<span style="color:#800080;">;</span>i<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span>
    <span style="color:#800080;">{</span>
        <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> j<span style="color:#808030;">=</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>j<span style="color:#808030;">&lt;</span><span style="color:#808030;">=</span>i<span style="color:#800080;">;</span>j<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span> <span style="color:#603000;">cin</span><span style="color:#808030;">&gt;</span><span style="color:#808030;">&gt;</span>a<span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#800080;">;</span>
        <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> j<span style="color:#808030;">=</span>i<span style="color:#800080;">;</span>j<span style="color:#808030;">&gt;</span><span style="color:#808030;">=</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>j<span style="color:#808030;">-</span><span style="color:#808030;">-</span><span style="color:#808030;">)</span> f<span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#808030;">=</span><span style="color:#603000;">max</span><span style="color:#808030;">(</span>f<span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#808030;">,</span>f<span style="color:#808030;">[</span>j<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">)</span><span style="color:#808030;">+</span>a<span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#800080;">;</span>
    <span style="color:#800080;">}</span>

    <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> i<span style="color:#808030;">=</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>i<span style="color:#808030;">&lt;</span><span style="color:#808030;">=</span>n<span style="color:#800080;">;</span>i<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span> ans<span style="color:#808030;">=</span><span style="color:#603000;">max</span><span style="color:#808030;">(</span>ans<span style="color:#808030;">,</span>f<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">)</span><span style="color:#800080;">;</span>
    <span style="color:#603000;">cout</span><span style="color:#808030;">&lt;</span><span style="color:#808030;">&lt;</span>ans<span style="color:#808030;">&lt;</span><span style="color:#808030;">&lt;</span><span style="color:#603000;">endl</span><span style="color:#800080;">;</span>

    <span style="color:#800000;font-weight:bold;">return</span> <span style="color:#008c00;">0</span><span style="color:#800080;">;</span>
<span style="color:#800080;">}</span></pre>


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

4
1 2 3 4
2 1 3 4
1 2 3 4
1 3 2 4

### 样例输出

39

## 限制

各个测试点1s

## 提示

多进程DP

代码：
<pre style="color:#000000;background:transparent;"><span style="color:#004a43;">#</span><span style="color:#004a43;">include</span><span style="color:#800000;">&lt;</span><span style="color:#40015a;">bits/stdc++.h</span><span style="color:#800000;">&gt;</span>
<span style="color:#800000;font-weight:bold;">using</span> <span style="color:#800000;font-weight:bold;">namespace</span> <span style="color:#666616;">std</span><span style="color:#800080;">;</span>

<span style="color:#800000;font-weight:bold;">const</span> <span style="color:#800000;font-weight:bold;">int</span> up<span style="color:#808030;">=</span><span style="color:#008c00;">20</span> <span style="color:#808030;">+</span><span style="color:#008c00;">5</span><span style="color:#800080;">;</span>

<span style="color:#800000;font-weight:bold;">int</span> n<span style="color:#808030;">,</span>a<span style="color:#808030;">[</span>up<span style="color:#808030;">]</span><span style="color:#808030;">[</span>up<span style="color:#808030;">]</span><span style="color:#808030;">,</span>f<span style="color:#808030;">[</span><span style="color:#008c00;">2</span><span style="color:#808030;">*</span>up<span style="color:#808030;">]</span><span style="color:#808030;">[</span>up<span style="color:#808030;">]</span><span style="color:#808030;">[</span>up<span style="color:#808030;">]</span><span style="color:#808030;">[</span>up<span style="color:#808030;">]</span><span style="color:#800080;">;</span>

<span style="color:#800000;font-weight:bold;">int</span> <span style="color:#400000;">main</span><span style="color:#808030;">(</span><span style="color:#808030;">)</span>
<span style="color:#800080;">{</span>
    <span style="color:#603000;">scanf</span><span style="color:#808030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%d</span><span style="color:#800000;">"</span><span style="color:#808030;">,</span><span style="color:#808030;">&amp;</span>n<span style="color:#808030;">)</span><span style="color:#800080;">;</span>
    <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> i<span style="color:#808030;">=</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>i<span style="color:#808030;">&lt;</span><span style="color:#808030;">=</span>n<span style="color:#800080;">;</span>i<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span>
        <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> j<span style="color:#808030;">=</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>j<span style="color:#808030;">&lt;</span><span style="color:#808030;">=</span>n<span style="color:#800080;">;</span>j<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span>
            <span style="color:#603000;">scanf</span><span style="color:#808030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%d</span><span style="color:#800000;">"</span><span style="color:#808030;">,</span><span style="color:#808030;">&amp;</span>a<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#808030;">)</span><span style="color:#800080;">;</span>
    f<span style="color:#808030;">[</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">=</span>a<span style="color:#808030;">[</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#800080;">;</span>

    <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> s<span style="color:#808030;">=</span><span style="color:#008c00;">2</span><span style="color:#800080;">;</span>s<span style="color:#808030;">&lt;</span><span style="color:#808030;">=</span><span style="color:#008c00;">2</span><span style="color:#808030;">*</span>n<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>s<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span>
        <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> x1<span style="color:#808030;">=</span><span style="color:#603000;">max</span><span style="color:#808030;">(</span><span style="color:#008c00;">1</span><span style="color:#808030;">,</span>s<span style="color:#808030;">-</span>n<span style="color:#808030;">+</span><span style="color:#008c00;">1</span><span style="color:#808030;">)</span><span style="color:#800080;">;</span>x1<span style="color:#808030;">&lt;</span><span style="color:#808030;">=</span><span style="color:#603000;">min</span><span style="color:#808030;">(</span>n<span style="color:#808030;">,</span>s<span style="color:#808030;">)</span><span style="color:#800080;">;</span>x1<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span>
            <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> x2<span style="color:#808030;">=</span><span style="color:#603000;">max</span><span style="color:#808030;">(</span><span style="color:#008c00;">1</span><span style="color:#808030;">,</span>s<span style="color:#808030;">-</span>n<span style="color:#808030;">+</span><span style="color:#008c00;">1</span><span style="color:#808030;">)</span><span style="color:#800080;">;</span>x2<span style="color:#808030;">&lt;</span><span style="color:#808030;">=</span><span style="color:#603000;">min</span><span style="color:#808030;">(</span>n<span style="color:#808030;">,</span>s<span style="color:#808030;">)</span><span style="color:#800080;">;</span>x2<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span>
                <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> x3<span style="color:#808030;">=</span><span style="color:#603000;">max</span><span style="color:#808030;">(</span><span style="color:#008c00;">1</span><span style="color:#808030;">,</span>s<span style="color:#808030;">-</span>n<span style="color:#808030;">+</span><span style="color:#008c00;">1</span><span style="color:#808030;">)</span><span style="color:#800080;">;</span>x3<span style="color:#808030;">&lt;</span><span style="color:#808030;">=</span><span style="color:#603000;">min</span><span style="color:#808030;">(</span>n<span style="color:#808030;">,</span>s<span style="color:#808030;">)</span><span style="color:#800080;">;</span>x3<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span>
                <span style="color:#800080;">{</span>
                    <span style="color:#696969;">//s=x+y-1</span>
                    <span style="color:#800000;font-weight:bold;">int</span> mid<span style="color:#808030;">=</span>a<span style="color:#808030;">[</span>x1<span style="color:#808030;">]</span><span style="color:#808030;">[</span>s<span style="color:#808030;">-</span>x1<span style="color:#808030;">+</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">+</span>a<span style="color:#808030;">[</span>x2<span style="color:#808030;">]</span><span style="color:#808030;">[</span>s<span style="color:#808030;">-</span>x2<span style="color:#808030;">+</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">+</span>a<span style="color:#808030;">[</span>x3<span style="color:#808030;">]</span><span style="color:#808030;">[</span>s<span style="color:#808030;">-</span>x3<span style="color:#808030;">+</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#800080;">;</span>
                    <span style="color:#800000;font-weight:bold;">if</span><span style="color:#808030;">(</span>x1<span style="color:#808030;">=</span><span style="color:#808030;">=</span>x2<span style="color:#808030;">)</span> mid<span style="color:#808030;">-</span><span style="color:#808030;">=</span>a<span style="color:#808030;">[</span>x1<span style="color:#808030;">]</span><span style="color:#808030;">[</span>s<span style="color:#808030;">-</span>x1<span style="color:#808030;">+</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#800080;">;</span>
                    <span style="color:#800000;font-weight:bold;">if</span><span style="color:#808030;">(</span>x1<span style="color:#808030;">=</span><span style="color:#808030;">=</span>x3<span style="color:#808030;">)</span> mid<span style="color:#808030;">-</span><span style="color:#808030;">=</span>a<span style="color:#808030;">[</span>x1<span style="color:#808030;">]</span><span style="color:#808030;">[</span>s<span style="color:#808030;">-</span>x1<span style="color:#808030;">+</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#800080;">;</span>
                    <span style="color:#800000;font-weight:bold;">if</span><span style="color:#808030;">(</span>x2<span style="color:#808030;">=</span><span style="color:#808030;">=</span>x3<span style="color:#808030;">)</span> mid<span style="color:#808030;">-</span><span style="color:#808030;">=</span>a<span style="color:#808030;">[</span>x2<span style="color:#808030;">]</span><span style="color:#808030;">[</span>s<span style="color:#808030;">-</span>x2<span style="color:#808030;">+</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#800080;">;</span>
                    <span style="color:#800000;font-weight:bold;">if</span><span style="color:#808030;">(</span>x1<span style="color:#808030;">=</span><span style="color:#808030;">=</span>x2 <span style="color:#808030;">&amp;</span><span style="color:#808030;">&amp;</span> x2<span style="color:#808030;">=</span><span style="color:#808030;">=</span>x3<span style="color:#808030;">)</span> mid<span style="color:#808030;">+</span><span style="color:#808030;">=</span>a<span style="color:#808030;">[</span>x1<span style="color:#808030;">]</span><span style="color:#808030;">[</span>s<span style="color:#808030;">-</span>x1<span style="color:#808030;">+</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#800080;">;</span><span style="color:#696969;">//容斥原理</span>
                    f<span style="color:#808030;">[</span>s<span style="color:#808030;">]</span><span style="color:#808030;">[</span>x1<span style="color:#808030;">]</span><span style="color:#808030;">[</span>x2<span style="color:#808030;">]</span><span style="color:#808030;">[</span>x3<span style="color:#808030;">]</span><span style="color:#808030;">=</span><span style="color:#603000;">max</span><span style="color:#808030;">(</span>f<span style="color:#808030;">[</span>s<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span>x1<span style="color:#808030;">]</span><span style="color:#808030;">[</span>x2<span style="color:#808030;">]</span><span style="color:#808030;">[</span>x3<span style="color:#808030;">]</span><span style="color:#808030;">,</span><span style="color:#603000;">max</span><span style="color:#808030;">(</span>f<span style="color:#808030;">[</span>s<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span>x1<span style="color:#808030;">]</span><span style="color:#808030;">[</span>x2<span style="color:#808030;">]</span><span style="color:#808030;">[</span>x3<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">,</span><span style="color:#603000;">max</span><span style="color:#808030;">(</span>f<span style="color:#808030;">[</span>s<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span>x1<span style="color:#808030;">]</span><span style="color:#808030;">[</span>x2<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span>x3<span style="color:#808030;">]</span><span style="color:#808030;">,</span><span style="color:#603000;">max</span><span style="color:#808030;">(</span>f<span style="color:#808030;">[</span>s<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span>x1<span style="color:#808030;">]</span><span style="color:#808030;">[</span>x2<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span>x3<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">,</span><span style="color:#603000;">max</span><span style="color:#808030;">(</span>f<span style="color:#808030;">[</span>s<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span>x1<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span>x2<span style="color:#808030;">]</span><span style="color:#808030;">[</span>x3<span style="color:#808030;">]</span><span style="color:#808030;">,</span><span style="color:#603000;">max</span><span style="color:#808030;">(</span>f<span style="color:#808030;">[</span>s<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span>x1<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span>x2<span style="color:#808030;">]</span><span style="color:#808030;">[</span>x3<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">,</span><span style="color:#603000;">max</span><span style="color:#808030;">(</span>f<span style="color:#808030;">[</span>s<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span>x1<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span>x2<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span>x3<span style="color:#808030;">]</span><span style="color:#808030;">,</span>f<span style="color:#808030;">[</span>s<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span>x1<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span>x2<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span>x3<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">)</span><span style="color:#808030;">)</span><span style="color:#808030;">)</span><span style="color:#808030;">)</span><span style="color:#808030;">)</span><span style="color:#808030;">)</span><span style="color:#808030;">)</span><span style="color:#800080;">;</span>
                    f<span style="color:#808030;">[</span>s<span style="color:#808030;">]</span><span style="color:#808030;">[</span>x1<span style="color:#808030;">]</span><span style="color:#808030;">[</span>x2<span style="color:#808030;">]</span><span style="color:#808030;">[</span>x3<span style="color:#808030;">]</span><span style="color:#808030;">+</span><span style="color:#808030;">=</span>mid<span style="color:#800080;">;</span>
                <span style="color:#800080;">}</span>

    <span style="color:#603000;">printf</span><span style="color:#808030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%d</span><span style="color:#800000;">"</span><span style="color:#808030;">,</span>f<span style="color:#808030;">[</span><span style="color:#008c00;">2</span><span style="color:#808030;">*</span>n<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span>n<span style="color:#808030;">]</span><span style="color:#808030;">[</span>n<span style="color:#808030;">]</span><span style="color:#808030;">[</span>n<span style="color:#808030;">]</span><span style="color:#808030;">)</span><span style="color:#800080;">;</span>

    <span style="color:#800000;font-weight:bold;">return</span> <span style="color:#008c00;">0</span><span style="color:#800080;">;</span>
<span style="color:#800080;">}</span></pre>

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

<pre style='color:#000000;background:#ffffff;'><span style='color:#004a43; '>#</span><span style='color:#004a43; '>include </span><span style='color:#800000; '>&lt;</span><span style='color:#40015a; '>bits/stdc++.h</span><span style='color:#800000; '>></span>
<span style='color:#004a43; '>#</span><span style='color:#004a43; '>define</span><span style='color:#004a43; '> NIL </span><span style='color:#808030; '>-</span><span style='color:#004a43; '>1</span>
<span style='color:#004a43; '>#</span><span style='color:#004a43; '>define</span><span style='color:#004a43; '> MAX_CAPACITY 3</span>
<span style='color:#004a43; '>#</span><span style='color:#004a43; '>define</span><span style='color:#004a43; '> INF 10000000</span>
<span style='color:#004a43; '>#</span><span style='color:#004a43; '>define</span><span style='color:#004a43; '> MIN</span><span style='color:#808030; '>(</span><span style='color:#004a43; '>a</span><span style='color:#808030; '>,</span><span style='color:#004a43; '>b</span><span style='color:#808030; '>)</span><span style='color:#004a43; '> </span><span style='color:#808030; '>(</span><span style='color:#808030; '>(</span><span style='color:#004a43; '>a</span><span style='color:#808030; '>)</span><span style='color:#808030; '>&lt;</span><span style='color:#808030; '>(</span><span style='color:#004a43; '>b</span><span style='color:#808030; '>)</span><span style='color:#808030; '>?</span><span style='color:#808030; '>(</span><span style='color:#004a43; '>a</span><span style='color:#808030; '>)</span><span style='color:#808030; '>:</span><span style='color:#808030; '>(</span><span style='color:#004a43; '>b</span><span style='color:#808030; '>)</span><span style='color:#808030; '>)</span>
<span style='color:#800000; font-weight:bold; '>using</span> <span style='color:#800000; font-weight:bold; '>namespace</span> <span style='color:#666616; '>std</span><span style='color:#800080; '>;</span>

<span style='color:#800000; font-weight:bold; '>typedef</span> <span style='color:#800000; font-weight:bold; '>struct</span><span style='color:#800080; '>{</span>
    <span style='color:#800000; font-weight:bold; '>int</span> next<span style='color:#800080; '>;</span>
    <span style='color:#800000; font-weight:bold; '>int</span> from<span style='color:#808030; '>,</span> to<span style='color:#808030; '>,</span> value<span style='color:#808030; '>,</span> f<span style='color:#800080; '>;</span>
<span style='color:#800080; '>}</span> edge<span style='color:#800080; '>;</span>

edge E<span style='color:#808030; '>[</span><span style='color:#008c00; '>5000</span><span style='color:#808030; '>]</span><span style='color:#800080; '>;</span>
<span style='color:#800000; font-weight:bold; '>int</span> headIndex<span style='color:#808030; '>[</span><span style='color:#008c00; '>1000</span><span style='color:#808030; '>]</span><span style='color:#800080; '>;</span>
<span style='color:#800000; font-weight:bold; '>int</span> size <span style='color:#808030; '>=</span> <span style='color:#008c00; '>0</span><span style='color:#800080; '>;</span>

<span style='color:#800000; font-weight:bold; '>short</span> used<span style='color:#808030; '>[</span><span style='color:#008c00; '>1000</span><span style='color:#808030; '>]</span><span style='color:#800080; '>;</span>
<span style='color:#800000; font-weight:bold; '>int</span> <span style='color:#603000; '>queue</span><span style='color:#808030; '>[</span><span style='color:#008c00; '>10000</span><span style='color:#808030; '>]</span><span style='color:#800080; '>;</span>
<span style='color:#800000; font-weight:bold; '>int</span> dist<span style='color:#808030; '>[</span><span style='color:#008c00; '>1000</span><span style='color:#808030; '>]</span><span style='color:#800080; '>;</span>
<span style='color:#800000; font-weight:bold; '>int</span> prev<span style='color:#808030; '>[</span><span style='color:#008c00; '>1000</span><span style='color:#808030; '>]</span><span style='color:#800080; '>;</span>

<span style='color:#800000; font-weight:bold; '>void</span> addEdge1<span style='color:#808030; '>(</span><span style='color:#800000; font-weight:bold; '>int</span> from<span style='color:#808030; '>,</span> <span style='color:#800000; font-weight:bold; '>int</span> to<span style='color:#808030; '>,</span> <span style='color:#800000; font-weight:bold; '>int</span> value<span style='color:#808030; '>,</span> <span style='color:#800000; font-weight:bold; '>int</span> capacity<span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
<span style='color:#800000; font-weight:bold; '>void</span> addEdge<span style='color:#808030; '>(</span><span style='color:#800000; font-weight:bold; '>int</span> from<span style='color:#808030; '>,</span> <span style='color:#800000; font-weight:bold; '>int</span> to<span style='color:#808030; '>,</span> <span style='color:#800000; font-weight:bold; '>int</span> value<span style='color:#808030; '>,</span> <span style='color:#800000; font-weight:bold; '>int</span> capacity<span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
<span style='color:#800000; font-weight:bold; '>int</span> maxPath<span style='color:#808030; '>(</span><span style='color:#800000; font-weight:bold; '>int</span> source<span style='color:#808030; '>,</span> <span style='color:#800000; font-weight:bold; '>int</span> sink<span style='color:#808030; '>,</span> <span style='color:#800000; font-weight:bold; '>int</span> numV<span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
<span style='color:#800000; font-weight:bold; '>int</span> maxValueFlow<span style='color:#808030; '>(</span><span style='color:#800000; font-weight:bold; '>int</span> source<span style='color:#808030; '>,</span> <span style='color:#800000; font-weight:bold; '>int</span> sink<span style='color:#808030; '>,</span> <span style='color:#800000; font-weight:bold; '>int</span> numV<span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>

<span style='color:#800000; font-weight:bold; '>int</span> <span style='color:#400000; '>main</span><span style='color:#808030; '>(</span><span style='color:#808030; '>)</span><span style='color:#800080; '>{</span>
    <span style='color:#800000; font-weight:bold; '>int</span> n<span style='color:#808030; '>,</span> numV<span style='color:#800080; '>;</span>
    <span style='color:#800000; font-weight:bold; '>int</span> x<span style='color:#808030; '>,</span> y<span style='color:#808030; '>,</span> source<span style='color:#808030; '>,</span> sink<span style='color:#808030; '>,</span> value<span style='color:#800080; '>;</span>

    <span style='color:#603000; '>scanf</span><span style='color:#808030; '>(</span><span style='color:#800000; '>"</span><span style='color:#007997; '>%d</span><span style='color:#800000; '>"</span><span style='color:#808030; '>,</span> <span style='color:#808030; '>&amp;</span>n<span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>

    <span style='color:#696969; '>/*initialize*/</span>
    <span style='color:#800000; font-weight:bold; '>for</span><span style='color:#808030; '>(</span>x<span style='color:#808030; '>=</span><span style='color:#008c00; '>0</span><span style='color:#800080; '>;</span> x<span style='color:#808030; '>&lt;</span><span style='color:#008c00; '>1000</span><span style='color:#800080; '>;</span> x<span style='color:#808030; '>+</span><span style='color:#808030; '>+</span><span style='color:#808030; '>)</span>
        headIndex<span style='color:#808030; '>[</span>x<span style='color:#808030; '>]</span> <span style='color:#808030; '>=</span> NIL<span style='color:#800080; '>;</span>

    <span style='color:#696969; '>/*build the network*/</span>
    numV <span style='color:#808030; '>=</span> <span style='color:#008c00; '>0</span><span style='color:#800080; '>;</span>
    <span style='color:#800000; font-weight:bold; '>for</span><span style='color:#808030; '>(</span>x<span style='color:#808030; '>=</span><span style='color:#008c00; '>0</span><span style='color:#800080; '>;</span> x<span style='color:#808030; '>&lt;</span>n<span style='color:#800080; '>;</span> x<span style='color:#808030; '>+</span><span style='color:#808030; '>+</span><span style='color:#808030; '>)</span><span style='color:#800080; '>{</span>
        <span style='color:#800000; font-weight:bold; '>for</span><span style='color:#808030; '>(</span>y<span style='color:#808030; '>=</span><span style='color:#008c00; '>0</span><span style='color:#800080; '>;</span> y<span style='color:#808030; '>&lt;</span>n<span style='color:#800080; '>;</span> y<span style='color:#808030; '>+</span><span style='color:#808030; '>+</span><span style='color:#808030; '>)</span><span style='color:#800080; '>{</span>
            <span style='color:#603000; '>scanf</span><span style='color:#808030; '>(</span><span style='color:#800000; '>"</span><span style='color:#007997; '>%d</span><span style='color:#800000; '>"</span><span style='color:#808030; '>,</span> <span style='color:#808030; '>&amp;</span>value<span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
            addEdge<span style='color:#808030; '>(</span>numV<span style='color:#808030; '>,</span> numV<span style='color:#808030; '>+</span><span style='color:#008c00; '>1</span><span style='color:#808030; '>,</span> value<span style='color:#808030; '>,</span> <span style='color:#008c00; '>1</span><span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>  <span style='color:#696969; '>//connect numV &amp; numV+1</span>
            addEdge<span style='color:#808030; '>(</span>numV<span style='color:#808030; '>,</span> numV<span style='color:#808030; '>+</span><span style='color:#008c00; '>1</span><span style='color:#808030; '>,</span> <span style='color:#008c00; '>0</span><span style='color:#808030; '>,</span> MAX_CAPACITY<span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
            <span style='color:#800000; font-weight:bold; '>if</span><span style='color:#808030; '>(</span>x <span style='color:#808030; '>&lt;</span> n<span style='color:#808030; '>-</span><span style='color:#008c00; '>1</span><span style='color:#808030; '>)</span>
                addEdge<span style='color:#808030; '>(</span>numV<span style='color:#808030; '>+</span><span style='color:#008c00; '>1</span><span style='color:#808030; '>,</span> numV<span style='color:#808030; '>+</span><span style='color:#008c00; '>2</span><span style='color:#808030; '>*</span>n<span style='color:#808030; '>,</span> <span style='color:#008c00; '>0</span><span style='color:#808030; '>,</span> MAX_CAPACITY<span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>  <span style='color:#696969; '>//connnect numV+1 &amp; its downer neighbour, if exists</span>
            <span style='color:#800000; font-weight:bold; '>if</span><span style='color:#808030; '>(</span>y <span style='color:#808030; '>&lt;</span> n<span style='color:#808030; '>-</span><span style='color:#008c00; '>1</span><span style='color:#808030; '>)</span>
                addEdge<span style='color:#808030; '>(</span>numV<span style='color:#808030; '>+</span><span style='color:#008c00; '>1</span><span style='color:#808030; '>,</span> numV<span style='color:#808030; '>+</span><span style='color:#008c00; '>2</span><span style='color:#808030; '>,</span> <span style='color:#008c00; '>0</span><span style='color:#808030; '>,</span> MAX_CAPACITY<span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>  <span style='color:#696969; '>//connnect numV+1 &amp; its righter neighbour, if exists</span>
            numV <span style='color:#808030; '>+</span><span style='color:#808030; '>=</span> <span style='color:#008c00; '>2</span><span style='color:#800080; '>;</span>
        <span style='color:#800080; '>}</span>
    <span style='color:#800080; '>}</span>
    source <span style='color:#808030; '>=</span> numV<span style='color:#808030; '>,</span> sink <span style='color:#808030; '>=</span> numV<span style='color:#808030; '>+</span><span style='color:#008c00; '>1</span><span style='color:#800080; '>;</span>
    addEdge<span style='color:#808030; '>(</span>source<span style='color:#808030; '>,</span> <span style='color:#008c00; '>0</span><span style='color:#808030; '>,</span> <span style='color:#008c00; '>0</span><span style='color:#808030; '>,</span> MAX_CAPACITY<span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>  <span style='color:#696969; '>//source</span>
    addEdge<span style='color:#808030; '>(</span>numV<span style='color:#808030; '>-</span><span style='color:#008c00; '>1</span><span style='color:#808030; '>,</span> sink<span style='color:#808030; '>,</span> <span style='color:#008c00; '>0</span><span style='color:#808030; '>,</span> MAX_CAPACITY<span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>  <span style='color:#696969; '>//sink</span>

    <span style='color:#696969; '>/*solve*/</span>
    <span style='color:#603000; '>printf</span><span style='color:#808030; '>(</span><span style='color:#800000; '>"</span><span style='color:#007997; '>%d</span><span style='color:#0f69ff; '>\n</span><span style='color:#800000; '>"</span><span style='color:#808030; '>,</span> maxValueFlow<span style='color:#808030; '>(</span>source<span style='color:#808030; '>,</span> sink<span style='color:#808030; '>,</span> numV<span style='color:#808030; '>+</span><span style='color:#008c00; '>2</span><span style='color:#808030; '>)</span><span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
    <span style='color:#800000; font-weight:bold; '>return</span> <span style='color:#008c00; '>0</span><span style='color:#800080; '>;</span>
<span style='color:#800080; '>}</span>
<span style='color:#800000; font-weight:bold; '>void</span> addEdge1<span style='color:#808030; '>(</span><span style='color:#800000; font-weight:bold; '>int</span> from<span style='color:#808030; '>,</span> <span style='color:#800000; font-weight:bold; '>int</span> to<span style='color:#808030; '>,</span> <span style='color:#800000; font-weight:bold; '>int</span> value<span style='color:#808030; '>,</span> <span style='color:#800000; font-weight:bold; '>int</span> capacity<span style='color:#808030; '>)</span><span style='color:#800080; '>{</span>
    E<span style='color:#808030; '>[</span>size<span style='color:#808030; '>]</span><span style='color:#808030; '>.</span>from <span style='color:#808030; '>=</span> from<span style='color:#800080; '>;</span>
    E<span style='color:#808030; '>[</span>size<span style='color:#808030; '>]</span><span style='color:#808030; '>.</span>to <span style='color:#808030; '>=</span> to<span style='color:#800080; '>;</span>
    E<span style='color:#808030; '>[</span>size<span style='color:#808030; '>]</span><span style='color:#808030; '>.</span>value <span style='color:#808030; '>=</span> value<span style='color:#800080; '>;</span>
    E<span style='color:#808030; '>[</span>size<span style='color:#808030; '>]</span><span style='color:#808030; '>.</span>f <span style='color:#808030; '>=</span> capacity<span style='color:#800080; '>;</span>
    E<span style='color:#808030; '>[</span>size<span style='color:#808030; '>]</span><span style='color:#808030; '>.</span>next <span style='color:#808030; '>=</span> headIndex<span style='color:#808030; '>[</span>from<span style='color:#808030; '>]</span><span style='color:#800080; '>;</span>
    headIndex<span style='color:#808030; '>[</span>from<span style='color:#808030; '>]</span> <span style='color:#808030; '>=</span> size<span style='color:#800080; '>;</span>
    size<span style='color:#808030; '>+</span><span style='color:#808030; '>+</span><span style='color:#800080; '>;</span>
<span style='color:#800080; '>}</span>
<span style='color:#800000; font-weight:bold; '>void</span> addEdge<span style='color:#808030; '>(</span><span style='color:#800000; font-weight:bold; '>int</span> from<span style='color:#808030; '>,</span> <span style='color:#800000; font-weight:bold; '>int</span> to<span style='color:#808030; '>,</span> <span style='color:#800000; font-weight:bold; '>int</span> value<span style='color:#808030; '>,</span> <span style='color:#800000; font-weight:bold; '>int</span> capacity<span style='color:#808030; '>)</span><span style='color:#800080; '>{</span>
    addEdge1<span style='color:#808030; '>(</span>from<span style='color:#808030; '>,</span> to<span style='color:#808030; '>,</span> value<span style='color:#808030; '>,</span> capacity<span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
    addEdge1<span style='color:#808030; '>(</span>to<span style='color:#808030; '>,</span> from<span style='color:#808030; '>,</span> <span style='color:#808030; '>-</span>value<span style='color:#808030; '>,</span> <span style='color:#008c00; '>0</span><span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
<span style='color:#800080; '>}</span>
<span style='color:#800000; font-weight:bold; '>int</span> maxPath<span style='color:#808030; '>(</span><span style='color:#800000; font-weight:bold; '>int</span> source<span style='color:#808030; '>,</span> <span style='color:#800000; font-weight:bold; '>int</span> sink<span style='color:#808030; '>,</span> <span style='color:#800000; font-weight:bold; '>int</span> numV<span style='color:#808030; '>)</span><span style='color:#800080; '>{</span>
    <span style='color:#800000; font-weight:bold; '>int</span> i<span style='color:#808030; '>,</span> head <span style='color:#808030; '>=</span> <span style='color:#008c00; '>0</span><span style='color:#808030; '>,</span> tail <span style='color:#808030; '>=</span> <span style='color:#008c00; '>0</span><span style='color:#800080; '>;</span>
    <span style='color:#800000; font-weight:bold; '>for</span><span style='color:#808030; '>(</span>i<span style='color:#808030; '>=</span><span style='color:#008c00; '>0</span><span style='color:#800080; '>;</span> i<span style='color:#808030; '>&lt;</span>numV<span style='color:#800080; '>;</span> i<span style='color:#808030; '>+</span><span style='color:#808030; '>+</span><span style='color:#808030; '>)</span><span style='color:#800080; '>{</span>
        used<span style='color:#808030; '>[</span>i<span style='color:#808030; '>]</span> <span style='color:#808030; '>=</span> <span style='color:#008c00; '>0</span><span style='color:#800080; '>;</span>
        prev<span style='color:#808030; '>[</span>i<span style='color:#808030; '>]</span> <span style='color:#808030; '>=</span> NIL<span style='color:#800080; '>;</span>
        dist<span style='color:#808030; '>[</span>i<span style='color:#808030; '>]</span> <span style='color:#808030; '>=</span> <span style='color:#808030; '>-</span>INF<span style='color:#800080; '>;</span>
    <span style='color:#800080; '>}</span>
    dist<span style='color:#808030; '>[</span>source<span style='color:#808030; '>]</span> <span style='color:#808030; '>=</span> <span style='color:#008c00; '>0</span><span style='color:#800080; '>;</span>
    <span style='color:#603000; '>queue</span><span style='color:#808030; '>[</span>tail<span style='color:#808030; '>+</span><span style='color:#808030; '>+</span><span style='color:#808030; '>]</span> <span style='color:#808030; '>=</span> source<span style='color:#800080; '>;</span>
    <span style='color:#800000; font-weight:bold; '>while</span><span style='color:#808030; '>(</span>head <span style='color:#808030; '>&lt;</span> tail<span style='color:#808030; '>)</span><span style='color:#800080; '>{</span>
        source <span style='color:#808030; '>=</span> <span style='color:#603000; '>queue</span><span style='color:#808030; '>[</span>head<span style='color:#808030; '>]</span><span style='color:#800080; '>;</span>
        used<span style='color:#808030; '>[</span>source<span style='color:#808030; '>]</span> <span style='color:#808030; '>=</span> <span style='color:#008c00; '>0</span><span style='color:#800080; '>;</span>
        i <span style='color:#808030; '>=</span> headIndex<span style='color:#808030; '>[</span>source<span style='color:#808030; '>]</span><span style='color:#800080; '>;</span>
        <span style='color:#800000; font-weight:bold; '>while</span><span style='color:#808030; '>(</span>i <span style='color:#808030; '>!</span><span style='color:#808030; '>=</span> NIL<span style='color:#808030; '>)</span><span style='color:#800080; '>{</span>
            <span style='color:#800000; font-weight:bold; '>if</span><span style='color:#808030; '>(</span>E<span style='color:#808030; '>[</span>i<span style='color:#808030; '>]</span><span style='color:#808030; '>.</span>f <span style='color:#808030; '>></span> <span style='color:#008c00; '>0</span> <span style='color:#808030; '>&amp;</span><span style='color:#808030; '>&amp;</span> dist<span style='color:#808030; '>[</span>E<span style='color:#808030; '>[</span>i<span style='color:#808030; '>]</span><span style='color:#808030; '>.</span>to<span style='color:#808030; '>]</span> <span style='color:#808030; '>&lt;</span> dist<span style='color:#808030; '>[</span>source<span style='color:#808030; '>]</span> <span style='color:#808030; '>+</span> E<span style='color:#808030; '>[</span>i<span style='color:#808030; '>]</span><span style='color:#808030; '>.</span>value<span style='color:#808030; '>)</span><span style='color:#800080; '>{</span>
                dist<span style='color:#808030; '>[</span>E<span style='color:#808030; '>[</span>i<span style='color:#808030; '>]</span><span style='color:#808030; '>.</span>to<span style='color:#808030; '>]</span> <span style='color:#808030; '>=</span> dist<span style='color:#808030; '>[</span>source<span style='color:#808030; '>]</span> <span style='color:#808030; '>+</span> E<span style='color:#808030; '>[</span>i<span style='color:#808030; '>]</span><span style='color:#808030; '>.</span>value<span style='color:#800080; '>;</span>
                prev<span style='color:#808030; '>[</span>E<span style='color:#808030; '>[</span>i<span style='color:#808030; '>]</span><span style='color:#808030; '>.</span>to<span style='color:#808030; '>]</span> <span style='color:#808030; '>=</span> i<span style='color:#800080; '>;</span>
                <span style='color:#800000; font-weight:bold; '>if</span><span style='color:#808030; '>(</span><span style='color:#808030; '>!</span>used<span style='color:#808030; '>[</span>E<span style='color:#808030; '>[</span>i<span style='color:#808030; '>]</span><span style='color:#808030; '>.</span>to<span style='color:#808030; '>]</span><span style='color:#808030; '>)</span><span style='color:#800080; '>{</span>
                    <span style='color:#603000; '>queue</span><span style='color:#808030; '>[</span>tail<span style='color:#808030; '>+</span><span style='color:#808030; '>+</span><span style='color:#808030; '>]</span> <span style='color:#808030; '>=</span> E<span style='color:#808030; '>[</span>i<span style='color:#808030; '>]</span><span style='color:#808030; '>.</span>to<span style='color:#800080; '>;</span>
                    used<span style='color:#808030; '>[</span>E<span style='color:#808030; '>[</span>i<span style='color:#808030; '>]</span><span style='color:#808030; '>.</span>to<span style='color:#808030; '>]</span> <span style='color:#808030; '>=</span> <span style='color:#008c00; '>1</span><span style='color:#800080; '>;</span>
                <span style='color:#800080; '>}</span>
            <span style='color:#800080; '>}</span>
            i <span style='color:#808030; '>=</span> E<span style='color:#808030; '>[</span>i<span style='color:#808030; '>]</span><span style='color:#808030; '>.</span>next<span style='color:#800080; '>;</span>
        <span style='color:#800080; '>}</span>
        head<span style='color:#808030; '>+</span><span style='color:#808030; '>+</span><span style='color:#800080; '>;</span>
    <span style='color:#800080; '>}</span>
    <span style='color:#800000; font-weight:bold; '>return</span> dist<span style='color:#808030; '>[</span>sink<span style='color:#808030; '>]</span><span style='color:#800080; '>;</span>
<span style='color:#800080; '>}</span>
<span style='color:#800000; font-weight:bold; '>int</span> maxValueFlow<span style='color:#808030; '>(</span><span style='color:#800000; font-weight:bold; '>int</span> source<span style='color:#808030; '>,</span> <span style='color:#800000; font-weight:bold; '>int</span> sink<span style='color:#808030; '>,</span> <span style='color:#800000; font-weight:bold; '>int</span> numV<span style='color:#808030; '>)</span><span style='color:#800080; '>{</span>
    <span style='color:#800000; font-weight:bold; '>int</span> path<span style='color:#808030; '>,</span> v<span style='color:#808030; '>,</span> augment<span style='color:#808030; '>,</span> value<span style='color:#808030; '>,</span> ret <span style='color:#808030; '>=</span> <span style='color:#008c00; '>0</span><span style='color:#800080; '>;</span>
    <span style='color:#800000; font-weight:bold; '>while</span><span style='color:#808030; '>(</span><span style='color:#808030; '>(</span>value <span style='color:#808030; '>=</span> maxPath<span style='color:#808030; '>(</span>source<span style='color:#808030; '>,</span> sink<span style='color:#808030; '>,</span> numV<span style='color:#808030; '>)</span><span style='color:#808030; '>)</span> <span style='color:#808030; '>></span> <span style='color:#008c00; '>0</span><span style='color:#808030; '>)</span><span style='color:#800080; '>{</span>
        augment <span style='color:#808030; '>=</span> INF<span style='color:#800080; '>;</span>
        <span style='color:#800000; font-weight:bold; '>for</span><span style='color:#808030; '>(</span>v<span style='color:#808030; '>=</span>sink<span style='color:#800080; '>;</span> v<span style='color:#808030; '>!</span><span style='color:#808030; '>=</span>source<span style='color:#800080; '>;</span> <span style='color:#808030; '>)</span><span style='color:#800080; '>{</span>
            path <span style='color:#808030; '>=</span> prev<span style='color:#808030; '>[</span>v<span style='color:#808030; '>]</span><span style='color:#800080; '>;</span>
            augment <span style='color:#808030; '>=</span> MIN<span style='color:#808030; '>(</span>augment<span style='color:#808030; '>,</span> E<span style='color:#808030; '>[</span>path<span style='color:#808030; '>]</span><span style='color:#808030; '>.</span>f<span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
            v <span style='color:#808030; '>=</span> E<span style='color:#808030; '>[</span>path<span style='color:#808030; '>]</span><span style='color:#808030; '>.</span>from<span style='color:#800080; '>;</span>
        <span style='color:#800080; '>}</span>
        <span style='color:#800000; font-weight:bold; '>for</span><span style='color:#808030; '>(</span>v<span style='color:#808030; '>=</span>sink<span style='color:#800080; '>;</span> v<span style='color:#808030; '>!</span><span style='color:#808030; '>=</span>source<span style='color:#800080; '>;</span> <span style='color:#808030; '>)</span><span style='color:#800080; '>{</span>
            path <span style='color:#808030; '>=</span> prev<span style='color:#808030; '>[</span>v<span style='color:#808030; '>]</span><span style='color:#800080; '>;</span>
            E<span style='color:#808030; '>[</span>path<span style='color:#808030; '>]</span><span style='color:#808030; '>.</span>f <span style='color:#808030; '>-</span><span style='color:#808030; '>=</span> augment<span style='color:#800080; '>;</span>
            E<span style='color:#808030; '>[</span>path<span style='color:#808030; '>^</span><span style='color:#008c00; '>1</span><span style='color:#808030; '>]</span><span style='color:#808030; '>.</span>f <span style='color:#808030; '>+</span><span style='color:#808030; '>=</span> augment<span style='color:#800080; '>;</span>
            v <span style='color:#808030; '>=</span> E<span style='color:#808030; '>[</span>path<span style='color:#808030; '>]</span><span style='color:#808030; '>.</span>from<span style='color:#800080; '>;</span>
        <span style='color:#800080; '>}</span>
        ret <span style='color:#808030; '>+</span><span style='color:#808030; '>=</span> value<span style='color:#808030; '>*</span>augment<span style='color:#800080; '>;</span>
    <span style='color:#800080; '>}</span>
    <span style='color:#800000; font-weight:bold; '>return</span> ret<span style='color:#800080; '>;</span>
<span style='color:#800080; '>}</span>
</pre>
