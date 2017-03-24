---
layout: post
title: 贪心专练
categories: [贪心]
description: 老文章
keywords: 贪心
---

## 硬币问题

1.有1元、5元、10元、50元、100元与500元的硬币各C<sub>1</sub>、C<sub>5</sub>、C<sub>10</sub>、C<sub>50</sub>、C<sub>100</sub>、C<sub>500</sub>枚，现在要用这些硬币来支付A元，最少需要多少枚硬币？假定至少有支付方案。

分析：尽可能多的使用大面值的硬币，因为同样的价值所需的硬币中，使用大面值一定少于使用小面值的数量（也许这些小面值还可以拼成一个大面值）。

<div id="code_set1" style="display:none;"><span style='color:#800000; font-weight:bold; '>int</span> ans<span style='color:#808030; '>=</span><span style='color:#008c00; '>0</span><span style='color:#800080; '>;</span>
<span style='color:#800000; font-weight:bold; '>for</span><span style='color:#808030; '>(</span><span style='color:#800000; font-weight:bold; '>int</span> i<span style='color:#808030; '>=</span><span style='color:#008c00; '>5</span><span style='color:#800080; '>;</span>i<span style='color:#808030; '>></span><span style='color:#808030; '>=</span><span style='color:#008c00; '>0</span><span style='color:#800080; '>;</span>i<span style='color:#808030; '>-</span><span style='color:#808030; '>-</span><span style='color:#808030; '>)</span>
<span style='color:#800080; '>{</span>
    <span style='color:#800000; font-weight:bold; '>int</span> t<span style='color:#808030; '>=</span><span style='color:#603000; '>min</span><span style='color:#808030; '>(</span>A<span style='color:#808030; '>/</span>V<span style='color:#808030; '>[</span>i<span style='color:#808030; '>]</span><span style='color:#808030; '>,</span>C<span style='color:#808030; '>[</span>i<span style='color:#808030; '>]</span><span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
    A<span style='color:#808030; '>-</span><span style='color:#808030; '>=</span>t<span style='color:#808030; '>*</span>V<span style='color:#808030; '>[</span>i<span style='color:#808030; '>]</span><span style='color:#800080; '>;</span>
    ans<span style='color:#808030; '>+</span><span style='color:#808030; '>=</span>t<span style='color:#800080; '>;</span>
<span style='color:#800080; '>}</span></div>

2.相似的选取最大值，比如UVa 11292 The Dargon of Loowater。

## 区间问题

1.有n项工作，每项工作分别在s<sub>i</sub>时间开始，在t<sub>i</sub>时间结束。对于每项工作，你都可以选择参与与否，但必须全程参与，这意味着时间不能重叠。

分析：每次选择时间结束最早的，在同等条件（仅仅是一个工作）下，选择结束最早的工作，因为完成一个工作后，剩下的时间越长，还可以做的工作就有可能会更多，就一定是最优。

<div id="code_set2" style="display:none;"><span style='color:#800000; font-weight:bold; '>for</span><span style='color:#808030; '>(</span><span style='color:#800000; font-weight:bold; '>int</span> i<span style='color:#808030; '>=</span><span style='color:#008c00; '>0</span><span style='color:#800080; '>;</span>i<span style='color:#808030; '>&lt;</span>N<span style='color:#800080; '>;</span>i<span style='color:#808030; '>+</span><span style='color:#808030; '>+</span><span style='color:#808030; '>)</span>
<span style='color:#800080; '>{</span>
    itv<span style='color:#808030; '>[</span>i<span style='color:#808030; '>]</span><span style='color:#808030; '>.</span>be<span style='color:#808030; '>=</span>S<span style='color:#808030; '>[</span>i<span style='color:#808030; '>]</span><span style='color:#800080; '>;</span>
    itv<span style='color:#808030; '>[</span>i<span style='color:#808030; '>]</span><span style='color:#808030; '>.</span>en<span style='color:#808030; '>=</span>T<span style='color:#808030; '>[</span>i<span style='color:#808030; '>]</span><span style='color:#800080; '>;</span>
<span style='color:#800080; '>}</span>

<span style='color:#800000; font-weight:bold; '>int</span> ans<span style='color:#808030; '>=</span><span style='color:#008c00; '>0</span><span style='color:#808030; '>,</span>t<span style='color:#808030; '>=</span><span style='color:#008c00; '>0</span><span style='color:#800080; '>;</span>
<span style='color:#800000; font-weight:bold; '>for</span><span style='color:#808030; '>(</span><span style='color:#800000; font-weight:bold; '>int</span> i<span style='color:#808030; '>=</span><span style='color:#008c00; '>0</span><span style='color:#800080; '>;</span>i<span style='color:#808030; '>&lt;</span>N<span style='color:#800080; '>;</span>i<span style='color:#808030; '>+</span><span style='color:#808030; '>+</span><span style='color:#808030; '>)</span> <span style='color:#800000; font-weight:bold; '>if</span><span style='color:#808030; '>(</span>t<span style='color:#808030; '>&lt;</span>itv<span style='color:#808030; '>[</span>i<span style='color:#808030; '>]</span><span style='color:#808030; '>.</span>be<span style='color:#808030; '>)</span>
<span style='color:#800080; '>{</span>
    ans<span style='color:#808030; '>+</span><span style='color:#808030; '>+</span><span style='color:#800080; '>;</span>
    t<span style='color:#808030; '>=</span>itv<span style='color:#808030; '>[</span>i<span style='color:#808030; '>]</span><span style='color:#808030; '>.</span>en<span style='color:#800080; '>;</span>
<span style='color:#800080; '>}</span>
<span style='color:#603000; '>printf</span><span style='color:#808030; '>(</span><span style='color:#800000; '>"</span><span style='color:#007997; '>%d</span><span style='color:#0f69ff; '>\n</span><span style='color:#800000; '>"</span><span style='color:#808030; '>,</span><span style='color:#808030; '>&amp;</span>ans<span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
</div>

另外，在证明贪心策略是最优解时，可以广泛的使用归纳法或是反证法（其实它更多用来证明贪心不是最优）。

3.相似的同等条件下最多或最少，比如POJ 3069 Suruman's Army、UVa 11729 Commando War。

## 字典序问题

1.给定长度为N且只有大写字母的字符串S，构造一个长度为N的字符串T，反复选择S的前后字母删除，放入T末尾，构造一个字典序最小的T。

分析：尽可能选取字典序小的字母先放，如果前后相等，那么就选择可以较快取到小的字母的那一边。

<div id="code_set3" style="display:none;"><span style='color:#800000; font-weight:bold; '>int</span> a<span style='color:#808030; '>=</span><span style='color:#008c00; '>0</span><span style='color:#808030; '>,</span>b<span style='color:#808030; '>=</span>N<span style='color:#808030; '>-</span><span style='color:#008c00; '>1</span><span style='color:#800080; '>;</span>
<span style='color:#800000; font-weight:bold; '>while</span><span style='color:#808030; '>(</span>a<span style='color:#808030; '>&lt;</span><span style='color:#808030; '>=</span>b<span style='color:#808030; '>)</span>
<span style='color:#800080; '>{</span>
    <span style='color:#800000; font-weight:bold; '>bool</span> left<span style='color:#808030; '>=</span><span style='color:#800000; font-weight:bold; '>false</span><span style='color:#800080; '>;</span>
    <span style='color:#800000; font-weight:bold; '>for</span><span style='color:#808030; '>(</span><span style='color:#800000; font-weight:bold; '>int</span> i<span style='color:#808030; '>=</span><span style='color:#008c00; '>0</span><span style='color:#800080; '>;</span>a<span style='color:#808030; '>+</span>i<span style='color:#808030; '>&lt;</span><span style='color:#808030; '>=</span>b<span style='color:#808030; '>-</span>i<span style='color:#800080; '>;</span>i<span style='color:#808030; '>+</span><span style='color:#808030; '>+</span><span style='color:#808030; '>)</span> 
        <span style='color:#800000; font-weight:bold; '>if</span><span style='color:#808030; '>(</span>S<span style='color:#808030; '>[</span>a<span style='color:#808030; '>+</span>i<span style='color:#808030; '>]</span><span style='color:#808030; '>&lt;</span>S<span style='color:#808030; '>[</span>b<span style='color:#808030; '>-</span>i<span style='color:#808030; '>]</span><span style='color:#808030; '>)</span>
        <span style='color:#800080; '>{</span>
            left<span style='color:#808030; '>=</span><span style='color:#800000; font-weight:bold; '>true</span><span style='color:#800080; '>;</span>
            <span style='color:#800000; font-weight:bold; '>break</span><span style='color:#800080; '>;</span>
        <span style='color:#800080; '>}</span>
        <span style='color:#800000; font-weight:bold; '>else</span> <span style='color:#800000; font-weight:bold; '>if</span><span style='color:#808030; '>(</span>S<span style='color:#808030; '>[</span>a<span style='color:#808030; '>+</span>i<span style='color:#808030; '>]</span><span style='color:#808030; '>></span>S<span style='color:#808030; '>[</span>b<span style='color:#808030; '>-</span>i<span style='color:#808030; '>]</span><span style='color:#808030; '>)</span> <span style='color:#800000; font-weight:bold; '>break</span><span style='color:#800080; '>;</span>
    <span style='color:#800000; font-weight:bold; '>if</span><span style='color:#808030; '>(</span>left<span style='color:#808030; '>)</span> <span style='color:#603000; '>putchar</span><span style='color:#808030; '>(</span>S<span style='color:#808030; '>[</span>a<span style='color:#808030; '>+</span><span style='color:#808030; '>+</span><span style='color:#808030; '>]</span><span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
    <span style='color:#800000; font-weight:bold; '>else</span> <span style='color:#603000; '>putchar</span><span style='color:#808030; '>(</span>S<span style='color:#808030; '>[</span>b<span style='color:#808030; '>-</span><span style='color:#808030; '>-</span><span style='color:#808030; '>]</span><span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
<span style='color:#800080; '>}</span>
<span style='color:#603000; '>putchar</span><span style='color:#808030; '>(</span><span style='color:#0000e6; '>'\n'</span><span style='color:#808030; '>)</span><span style='color:#800080; '>;</span></div>

2.相似的字典序问题，如POJ 3617 Best Cow Line。

3.类比的两端加权取数，如Vijos 1378 矩阵取数游戏。

## 更多的贪心问题

1.本文仅仅挑选了有代表性的且较为简单的贪心题，然而还有更多且复杂的题目，它们都需要好好地思考一下才能做对。

2.更多的贪心问题，还有代表性的有Vijos 1097 合并果子(POJ 3253 Fence Repair)、UVa 11300 Spreading the Wealth、LA 3708 Graveyard，甚至一些动规问题都可以用贪心处理（当然能拿多少分还是得靠信仰）。

3.本文所有的题目

|来源&题号|题目|
|:--|:--|
|UVa 11292|The Dargon of Loowater|
|POJ 3069|Suruman's Army|
|UVa 11729|Commando War|
|POJ 3617|Best Cow Line|
|Vijos 1378|矩阵取数游戏|
|Vijos 1097|合并果子|
|UVa 11300|Spreading the Wealth|
|LA 3708|Graveyard|
