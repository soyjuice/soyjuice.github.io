---
layout: post
title: DP Problems Part 1
categories: [NOI, 动态规划]
description: 老文章
keywords: C++, 动态规划
---

# 1.数字三角形

## 描述

示出了一个数字三角形。 请编一个程序计算从顶至底的某处的一条路
径，使该路径所经过的数字的总和最大。
每一步可沿左斜线向下或右斜线向下走；
1&lt;三角形行数&lt;25；
三角形中的数字为整数&lt;1000；
<!--more-->
## 输入格式

第一行为N，表示有N行
后面N行表示三角形每条路的路径权</div>

## 输出格式

路径所经过的数字的总和最大的答案

## 测试样例1

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

**代码**：

<pre style="color:#000000;background:transparent;"><span style="color:#004a43;">#</span><span style="color:#004a43;">include</span><span style="color:#800000;">&lt;</span><span style="color:#40015a;">bits/stdc++.h</span><span style="color:#800000;">&gt;</span>
<span style="color:#800000;font-weight:bold;">using</span> <span style="color:#800000;font-weight:bold;">namespace</span> <span style="color:#666616;">std</span><span style="color:#800080;">;</span>

<span style="color:#800000;font-weight:bold;">const</span> <span style="color:#800000;font-weight:bold;">int</span> up<span style="color:#808030;">=</span><span style="color:#008c00;">30</span><span style="color:#800080;">;</span>
<span style="color:#603000;">vector</span> ve<span style="color:#808030;">[</span>up<span style="color:#808030;">]</span><span style="color:#800080;">;</span>
<span style="color:#800000;font-weight:bold;">int</span> f<span style="color:#808030;">[</span>up<span style="color:#808030;">]</span><span style="color:#808030;">[</span>up<span style="color:#808030;">]</span><span style="color:#800080;">;</span>

<span style="color:#800000;font-weight:bold;">int</span> dfs<span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> x<span style="color:#808030;">,</span><span style="color:#800000;font-weight:bold;">int</span> y<span style="color:#808030;">)</span>
<span style="color:#800080;">{</span>
    <span style="color:#800000;font-weight:bold;">if</span><span style="color:#808030;">(</span>f<span style="color:#808030;">[</span>x<span style="color:#808030;">]</span><span style="color:#808030;">[</span>y<span style="color:#808030;">]</span><span style="color:#808030;">)</span> <span style="color:#800000;font-weight:bold;">return</span> f<span style="color:#808030;">[</span>x<span style="color:#808030;">]</span><span style="color:#808030;">[</span>y<span style="color:#808030;">]</span><span style="color:#800080;">;</span>
    <span style="color:#800000;font-weight:bold;">return</span> f<span style="color:#808030;">[</span>x<span style="color:#808030;">]</span><span style="color:#808030;">[</span>y<span style="color:#808030;">]</span><span style="color:#808030;">=</span>ve<span style="color:#808030;">[</span>x<span style="color:#808030;">]</span><span style="color:#808030;">[</span>y<span style="color:#808030;">]</span><span style="color:#808030;">+</span><span style="color:#603000;">max</span><span style="color:#808030;">(</span>dfs<span style="color:#808030;">(</span>x<span style="color:#808030;">+</span><span style="color:#008c00;">1</span><span style="color:#808030;">,</span>y<span style="color:#808030;">)</span><span style="color:#808030;">,</span>dfs<span style="color:#808030;">(</span>x<span style="color:#808030;">+</span><span style="color:#008c00;">1</span><span style="color:#808030;">,</span>y<span style="color:#808030;">+</span><span style="color:#008c00;">1</span><span style="color:#808030;">)</span><span style="color:#808030;">)</span><span style="color:#800080;">;</span>
<span style="color:#800080;">}</span>

<span style="color:#800000;font-weight:bold;">int</span> <span style="color:#400000;">main</span><span style="color:#808030;">(</span><span style="color:#808030;">)</span>
<span style="color:#800080;">{</span>
    <span style="color:#696969;">//freopen("djs.in","r",stdin);</span>
    <span style="color:#696969;">//freopen("djs.out","w",stdout);</span>
    <span style="color:#800000;font-weight:bold;">int</span> i<span style="color:#808030;">=</span><span style="color:#008c00;">0</span><span style="color:#808030;">,</span>j<span style="color:#808030;">=</span><span style="color:#008c00;">0</span><span style="color:#808030;">,</span>n<span style="color:#808030;">,</span>m<span style="color:#800080;">;</span>

    <span style="color:#603000;">cin</span><span style="color:#808030;">&gt;</span><span style="color:#808030;">&gt;</span>n<span style="color:#800080;">;</span>
    <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span>i<span style="color:#808030;">=</span><span style="color:#008c00;">0</span><span style="color:#800080;">;</span>i<span style="color:#808030;">&lt;</span>n<span style="color:#800080;">;</span>i<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span>
    <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span>j<span style="color:#808030;">=</span><span style="color:#008c00;">0</span><span style="color:#800080;">;</span>j<span style="color:#808030;">&lt;</span><span style="color:#808030;">=</span>i<span style="color:#800080;">;</span>j<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span>       
    <span style="color:#800080;">{</span>           
        <span style="color:#603000;">cin</span><span style="color:#808030;">&gt;</span><span style="color:#808030;">&gt;</span>m<span style="color:#800080;">;</span>
        ve<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">.</span>push_back<span style="color:#808030;">(</span>m<span style="color:#808030;">)</span><span style="color:#800080;">;</span>
        <span style="color:#800000;font-weight:bold;">if</span><span style="color:#808030;">(</span>i<span style="color:#808030;">=</span><span style="color:#808030;">=</span>n<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">)</span> f<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#808030;">=</span>m<span style="color:#800080;">;</span>
    <span style="color:#800080;">}</span>
    <span style="color:#603000;">cout</span><span style="color:#808030;">&lt;</span><span style="color:#808030;">&lt;</span>dfs<span style="color:#808030;">(</span><span style="color:#008c00;">0</span><span style="color:#808030;">,</span><span style="color:#008c00;">0</span><span style="color:#808030;">)</span><span style="color:#808030;">&lt;</span><span style="color:#808030;">&lt;</span><span style="color:#603000;">endl</span><span style="color:#800080;">;</span> 

    <span style="color:#800000;font-weight:bold;">return</span> <span style="color:#008c00;">0</span><span style="color:#800080;">;</span>
<span style="color:#800080;">}</span></pre>


# 2.方格取数

## 题目描述

设有N*N的方格图(N&lt;=9)，我们将其中的某些方格中填入正整数，而其他的方格中则放

人数字0。如下图所示（见样例）：

A
 0  0  0  0  0  0  0  0
 0  0 13  0  0  6  0  0
 0  0  0  0  7  0  0  0
 0  0  0 14  0  0  0  0
 0 21  0  0  0  4  0  0
 0  0 15  0  0  0  0  0
 0 14  0  0  0  0  0  0
 0  0  0  0  0  0  0  0
    .                  B

某人从图的左上角的A点出发，可以向下行走，也可以向右走，直到到达右下角的B

点。在走过的路上，他可以取走方格中的数（取走后的方格中将变为数字0）。

此人从A点到B点共走两次，试找出2条这样的路径，使得取得的数之和为最大。

## 输入输出格式

**输入格式：**

输入的第一行为一个整数N（表示N*N的方格图），接下来的每行有三个整数，前两个

表示位置，第三个数为该位置上所放的数。一行单独的0表示输入结束。

**输出格式：**

只需输出一个整数，表示2条路径上取得的最大的和。

## 输入输出样例

**输入样例#1：**
8
2 3 13
2 6  6
3 5  7
4 4 14
5 2 21
5 6  4
6 3 15
7 2 14
0 0  0

**输出样例#1：**
67

## 说明

NOIP 2000 提高组第四题

**代码**：

<pre style="color:#000000;background:transparent;"><span style="color:#004a43;">#</span><span style="color:#004a43;">include</span><span style="color:#800000;">&lt;</span><span style="color:#40015a;">bits/stdc++.h</span><span style="color:#800000;">&gt;</span>
<span style="color:#800000;font-weight:bold;">using</span> <span style="color:#800000;font-weight:bold;">namespace</span> <span style="color:#666616;">std</span><span style="color:#800080;">;</span>

<span style="color:#800000;font-weight:bold;">int</span> n<span style="color:#800080;">;</span>
<span style="color:#800000;font-weight:bold;">int</span> a<span style="color:#808030;">[</span><span style="color:#008c00;">10</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span><span style="color:#008c00;">10</span><span style="color:#808030;">]</span><span style="color:#808030;">=</span> <span style="color:#800080;">{</span><span style="color:#008c00;">0</span><span style="color:#800080;">}</span><span style="color:#800080;">;</span>
<span style="color:#800000;font-weight:bold;">int</span> f<span style="color:#808030;">[</span><span style="color:#008c00;">10</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span><span style="color:#008c00;">10</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span><span style="color:#008c00;">10</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span><span style="color:#008c00;">10</span><span style="color:#808030;">]</span><span style="color:#808030;">=</span> <span style="color:#800080;">{</span><span style="color:#008c00;">0</span><span style="color:#800080;">}</span><span style="color:#800080;">;</span>

<span style="color:#800000;font-weight:bold;">int</span> <span style="color:#400000;">main</span><span style="color:#808030;">(</span><span style="color:#808030;">)</span> 
<span style="color:#800080;">{</span>
    <span style="color:#603000;">cin</span><span style="color:#808030;">&gt;</span><span style="color:#808030;">&gt;</span>n<span style="color:#800080;">;</span>
    <span style="color:#800000;font-weight:bold;">while</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">true</span><span style="color:#808030;">)</span> 
    <span style="color:#800080;">{</span>
        <span style="color:#800000;font-weight:bold;">int</span> x<span style="color:#808030;">,</span>y<span style="color:#808030;">,</span>z<span style="color:#800080;">;</span>
        <span style="color:#603000;">cin</span><span style="color:#808030;">&gt;</span><span style="color:#808030;">&gt;</span>x<span style="color:#808030;">&gt;</span><span style="color:#808030;">&gt;</span>y<span style="color:#808030;">&gt;</span><span style="color:#808030;">&gt;</span>z<span style="color:#800080;">;</span>
        <span style="color:#800000;font-weight:bold;">if</span><span style="color:#808030;">(</span>x<span style="color:#808030;">=</span><span style="color:#808030;">=</span><span style="color:#008c00;">0</span><span style="color:#808030;">)</span> <span style="color:#800000;font-weight:bold;">break</span><span style="color:#800080;">;</span>
        a<span style="color:#808030;">[</span>x<span style="color:#808030;">]</span><span style="color:#808030;">[</span>y<span style="color:#808030;">]</span><span style="color:#808030;">=</span>z<span style="color:#800080;">;</span>
    <span style="color:#800080;">}</span>
    <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> i<span style="color:#808030;">=</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>i<span style="color:#808030;">&lt;</span><span style="color:#808030;">=</span>n<span style="color:#800080;">;</span>i<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span> 
        <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> j<span style="color:#808030;">=</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>j<span style="color:#808030;">&lt;</span><span style="color:#808030;">=</span>n<span style="color:#800080;">;</span>j<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span> 
            <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> k<span style="color:#808030;">=</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>k<span style="color:#808030;">&lt;</span><span style="color:#808030;">=</span>n<span style="color:#800080;">;</span>k<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span> 
                <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> l<span style="color:#808030;">=</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>l<span style="color:#808030;">&lt;</span><span style="color:#808030;">=</span>n<span style="color:#800080;">;</span>l<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span> 
                <span style="color:#800080;">{</span>
                    f<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#808030;">[</span>k<span style="color:#808030;">]</span><span style="color:#808030;">[</span>l<span style="color:#808030;">]</span><span style="color:#808030;">=</span><span style="color:#603000;">max</span><span style="color:#808030;">(</span><span style="color:#603000;">max</span><span style="color:#808030;">(</span>f<span style="color:#808030;">[</span>i<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#808030;">[</span>k<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span>l<span style="color:#808030;">]</span><span style="color:#808030;">,</span>f<span style="color:#808030;">[</span>i<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#808030;">[</span>k<span style="color:#808030;">]</span><span style="color:#808030;">[</span>l<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">)</span><span style="color:#808030;">,</span><span style="color:#603000;">max</span><span style="color:#808030;">(</span>f<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">[</span>j<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span>k<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span>l<span style="color:#808030;">]</span><span style="color:#808030;">,</span>f<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">[</span>j<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span>k<span style="color:#808030;">]</span><span style="color:#808030;">[</span>l<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">)</span><span style="color:#808030;">)</span><span style="color:#808030;">+</span>a<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#800080;">;</span>
                    <span style="color:#800000;font-weight:bold;">if</span> <span style="color:#808030;">(</span>i<span style="color:#808030;">!</span><span style="color:#808030;">=</span>k <span style="color:#808030;">&amp;</span><span style="color:#808030;">&amp;</span> j<span style="color:#808030;">!</span><span style="color:#808030;">=</span>l<span style="color:#808030;">)</span> f<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#808030;">[</span>k<span style="color:#808030;">]</span><span style="color:#808030;">[</span>l<span style="color:#808030;">]</span><span style="color:#808030;">+</span><span style="color:#808030;">=</span>a<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#800080;">;</span>
                <span style="color:#800080;">}</span>
    <span style="color:#603000;">cout</span><span style="color:#808030;">&lt;</span><span style="color:#808030;">&lt;</span>f<span style="color:#808030;">[</span>n<span style="color:#808030;">]</span><span style="color:#808030;">[</span>n<span style="color:#808030;">]</span><span style="color:#808030;">[</span>n<span style="color:#808030;">]</span><span style="color:#808030;">[</span>n<span style="color:#808030;">]</span><span style="color:#808030;">&lt;</span><span style="color:#808030;">&lt;</span><span style="color:#603000;">endl</span><span style="color:#800080;">;</span>

    <span style="color:#800000;font-weight:bold;">return</span> <span style="color:#008c00;">0</span><span style="color:#800080;">;</span>
<span style="color:#800080;">}</span></pre>


# 3.传纸条

## 题目描述

小渊和小轩是好朋友也是同班同学，他们在一起总有谈不完的话题。一次素质拓展活动中，班上同学安排做成一个m行n列的矩阵，而小渊和小轩被安排在矩阵对角线的两端，因此，他们就无法直接交谈了。幸运的是，他们可以通过传纸条来进行交流。纸条要经由许多同学传到对方手里，小渊坐在矩阵的左上角，坐标(1,1)，小轩坐在矩阵的右下角，坐标(m,n)。从小渊传到小轩的纸条只可以向下或者向右传递，从小轩传给小渊的纸条只可以向上或者向左传递。

在活动进行中，小渊希望给小轩传递一张纸条，同时希望小轩给他回复。班里每个同学都可以帮他们传递，但只会帮他们一次，也就是说如果此人在小渊递给小轩纸条的时候帮忙，那么在小轩递给小渊的时候就不会再帮忙。反之亦然。

还有一件事情需要注意，全班每个同学愿意帮忙的好感度有高有低（注意：小渊和小轩的好心程度没有定义，输入时用0表示），可以用一个0-100的自然数来表示，数越大表示越好心。小渊和小轩希望尽可能找好心程度高的同学来帮忙传纸条，即找到来回两条传递路径，使得这两条路径上同学的好心程度只和最大。现在，请你帮助小渊和小轩找到这样的两条路径。

## 输入输出格式

**输入格式：**

输入文件message.in的第一行有2个用空格隔开的整数m和n，表示班里有m行n列（1&lt;=m,n&lt;=50）。

接下来的m行是一个m*n的矩阵，矩阵中第i行j列的整数表示坐在第i行j列的学生的好心程度。每行的n个整数之间用空格隔开。

**输出格式：**

输出文件message.out共一行，包含一个整数，表示来回两条路上参与传递纸条的学生的好心程度之和的最大值。

## 输入输出样例

**输入样例#1：**
3 3
0 3 9
2 8 5
5 7 0

**输出样例#1：**
34

## 说明

【限制】

30%的数据满足：1&lt;=m,n&lt;=10

100%的数据满足：1&lt;=m,n&lt;=50

NOIP 2008提高组第三题

**代码**：

<pre style="color:#000000;background:transparent;"><span style="color:#004a43;">#</span><span style="color:#004a43;">include</span><span style="color:#800000;">&lt;</span><span style="color:#40015a;">bits/stdc++.h</span><span style="color:#800000;">&gt;</span>
<span style="color:#800000;font-weight:bold;">using</span> <span style="color:#800000;font-weight:bold;">namespace</span> <span style="color:#666616;">std</span><span style="color:#800080;">;</span>

<span style="color:#800000;font-weight:bold;">const</span> <span style="color:#800000;font-weight:bold;">int</span> up<span style="color:#808030;">=</span><span style="color:#008c00;">55</span><span style="color:#800080;">;</span>
<span style="color:#800000;font-weight:bold;">int</span> ans<span style="color:#808030;">[</span>up<span style="color:#808030;">]</span><span style="color:#808030;">[</span>up<span style="color:#808030;">]</span><span style="color:#808030;">,</span>dis<span style="color:#808030;">[</span>up<span style="color:#808030;">]</span><span style="color:#808030;">[</span>up<span style="color:#808030;">]</span><span style="color:#808030;">[</span>up<span style="color:#808030;">]</span><span style="color:#808030;">[</span>up<span style="color:#808030;">]</span><span style="color:#800080;">;</span>

<span style="color:#800000;font-weight:bold;">int</span> <span style="color:#400000;">main</span><span style="color:#808030;">(</span><span style="color:#808030;">)</span>
<span style="color:#800080;">{</span>
    <span style="color:#800000;font-weight:bold;">int</span> n<span style="color:#808030;">,</span>m<span style="color:#800080;">;</span>
    <span style="color:#603000;">cin</span><span style="color:#808030;">&gt;</span><span style="color:#808030;">&gt;</span>m<span style="color:#808030;">&gt;</span><span style="color:#808030;">&gt;</span>n<span style="color:#800080;">;</span>
    <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> i<span style="color:#808030;">=</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>i<span style="color:#808030;">&lt;</span><span style="color:#808030;">=</span>m<span style="color:#800080;">;</span>i<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span>
        <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> j<span style="color:#808030;">=</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>j<span style="color:#808030;">&lt;</span><span style="color:#808030;">=</span>n<span style="color:#800080;">;</span>j<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span> <span style="color:#603000;">cin</span><span style="color:#808030;">&gt;</span><span style="color:#808030;">&gt;</span>ans<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#800080;">;</span>
    <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> i<span style="color:#808030;">=</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>i<span style="color:#808030;">&lt;</span><span style="color:#808030;">=</span>m<span style="color:#800080;">;</span>i<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span>
        <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> j<span style="color:#808030;">=</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>j<span style="color:#808030;">&lt;</span><span style="color:#808030;">=</span>n<span style="color:#800080;">;</span>j<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span>
            <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> k<span style="color:#808030;">=</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>k<span style="color:#808030;">&lt;</span><span style="color:#808030;">=</span>m<span style="color:#800080;">;</span>k<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span>
                <span style="color:#800000;font-weight:bold;">for</span><span style="color:#808030;">(</span><span style="color:#800000;font-weight:bold;">int</span> l<span style="color:#808030;">=</span><span style="color:#008c00;">1</span><span style="color:#800080;">;</span>l<span style="color:#808030;">&lt;</span><span style="color:#808030;">=</span>n<span style="color:#800080;">;</span>l<span style="color:#808030;">+</span><span style="color:#808030;">+</span><span style="color:#808030;">)</span>
                <span style="color:#800080;">{</span>
                    dis<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#808030;">[</span>k<span style="color:#808030;">]</span><span style="color:#808030;">[</span>l<span style="color:#808030;">]</span><span style="color:#808030;">=</span><span style="color:#603000;">max</span><span style="color:#808030;">(</span><span style="color:#603000;">max</span><span style="color:#808030;">(</span>dis<span style="color:#808030;">[</span>i<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#808030;">[</span>k<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span>l<span style="color:#808030;">]</span><span style="color:#808030;">,</span>dis<span style="color:#808030;">[</span>i<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#808030;">[</span>k<span style="color:#808030;">]</span><span style="color:#808030;">[</span>l<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">)</span><span style="color:#808030;">,</span><span style="color:#603000;">max</span><span style="color:#808030;">(</span>dis<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">[</span>j<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span>k<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span>l<span style="color:#808030;">]</span><span style="color:#808030;">,</span>dis<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">[</span>j<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">[</span>k<span style="color:#808030;">]</span><span style="color:#808030;">[</span>l<span style="color:#808030;">-</span><span style="color:#008c00;">1</span><span style="color:#808030;">]</span><span style="color:#808030;">)</span><span style="color:#808030;">)</span><span style="color:#808030;">+</span>ans<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#800080;">;</span>
                    <span style="color:#800000;font-weight:bold;">if</span><span style="color:#808030;">(</span>i<span style="color:#808030;">!</span><span style="color:#808030;">=</span>k <span style="color:#808030;">&amp;</span><span style="color:#808030;">&amp;</span> j<span style="color:#808030;">!</span><span style="color:#808030;">=</span>l<span style="color:#808030;">)</span> dis<span style="color:#808030;">[</span>i<span style="color:#808030;">]</span><span style="color:#808030;">[</span>j<span style="color:#808030;">]</span><span style="color:#808030;">[</span>k<span style="color:#808030;">]</span><span style="color:#808030;">[</span>l<span style="color:#808030;">]</span><span style="color:#808030;">+</span><span style="color:#808030;">=</span>ans<span style="color:#808030;">[</span>k<span style="color:#808030;">]</span><span style="color:#808030;">[</span>l<span style="color:#808030;">]</span><span style="color:#800080;">;</span>
                <span style="color:#800080;">}</span>
    <span style="color:#603000;">cout</span><span style="color:#808030;">&lt;</span><span style="color:#808030;">&lt;</span>dis<span style="color:#808030;">[</span>m<span style="color:#808030;">]</span><span style="color:#808030;">[</span>n<span style="color:#808030;">]</span><span style="color:#808030;">[</span>m<span style="color:#808030;">]</span><span style="color:#808030;">[</span>n<span style="color:#808030;">]</span><span style="color:#808030;">&lt;</span><span style="color:#808030;">&lt;</span><span style="color:#603000;">endl</span><span style="color:#800080;">;</span>

    <span style="color:#800000;font-weight:bold;">return</span> <span style="color:#008c00;">0</span><span style="color:#800080;">;</span>
<span style="color:#800080;">}</span></pre>
