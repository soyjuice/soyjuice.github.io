---
layout: post
title: 动态规划专练（六）
categories: [NOI, 动态规划]
description: 新文章
mini-description: 正儿八经的练习题
keywords: C++, 动态规划
---

# 1.魔族密码

## 描述

风之子刚走进他的考场，就……
花花：当当当当~~偶是魅力女皇——花花！！^^（华丽出场，礼炮，鲜花）
风之子：我呕……（杀死人的眼神）快说题目！否则……-_-###
花花：……咦~~好冷~~我们现在要解决的是魔族的密码问题（自我陶醉：搞不好魔族里面还会有人用密码给我和菜虫写情书咧，哦活活，当然是给我的比较多拉*^_^*）。魔族现在使用一种新型的密码系统。每一个密码都是一个给定的仅包含小写字母的英文单词表，每个单词至少包含1个字母，至多75个字母。如果在一个由一个词或多个词组成的表中，除了最后一个以外，每个单词都被其后的一个单词所包含，即前一个单词是后一个单词的前缀，则称词表为一个词链。例如下面单词组成了一个词链：
i
int
integer
但下面的单词不组成词链：
integer
intern
现在你要做的就是在一个给定的单词表中取出一些词，组成最长的词链，就是包含单词数最多的词链。将它的单词数统计出来，就得到密码了。
风之子：密码就是最长词链所包括的单词数阿……
花花：活活活，还有，这些文件的格式是，第一行为单词表中的单词数N（1<=N<=2000），下面每一行有一个单词，按字典顺序排列，中间也没有重复的单词咧！！你要提交的文件中只要在第一行输出密码就行啦^^看你长得还不错，给你一个样例吧：
## 样例1

### 样例输入1
<pre>
5
i
int
integer
intern
internet
</pre>
### 样例输出1
<pre>
4
</pre>
## 限制

各个测试点1s
## 来源

Vivian Snow
From 正·蠢盟演义——战略版 Fools-League Tactics

## 分析

对于这道题，我是用的Tire树，但是，标签上是DP，So——

我直接使用代码了：

``` cpp
/*
LIS问题~
其实说白了LIS就是满足条件找一条最长链而已
或者换句话说这个题目就是一个DAG上的动态规划
和lrj的紫书（作者按：我叫之小红皮）的嵌套矩形本质是一样的
所以我们只需要判断一下两个单词是否可以链接
因为注意到我们是要严格按照顺序来的
所以我们完全没有必要去建图~
因为两个单词本来最多就只会比较一次
建图反而效率会更低
这样我们就可以直接沿用LIS的模式
只是判断大小变成了是否可以链接
进行尝试转移就好了~
QAQ总体还是挺简单的
*/
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <cstring>
using namespace std;

string a[2003];
int f[2003];
int ans;
int n;

int check(int x,int y)//检查a[y]是否可以连在a[x]上
{
    int l1=a[x].length();
    int l2=a[y].length();
    if(l1<=l2)
        return 0;
    for(int i=0;i<l2;i++)
        if(a[x][i]!=a[y][i])
            return 0;
    return 1;
}

void init()
{
    scanf("%d",&n);
    for(int i=1;i<=n;i++)
        cin>>a[i];
}

void DP()
{
    for(int i=1;i<=n;i++)
    {
        for(int j=i-1;j>=0;j--)//逆序尝试是否可以接在前面的某个string上
            if(check(i,j))
                f[i]=max(f[i],f[j]+1);
        ans=max(ans,f[i]);
    }
    cout<<ans<<endl;
}

int main()
{
    init();
    DP();
}
//作者按：以上代码引用

// Tire树
#include<iostream>
#include<cstdio>
#include<cstring>
#include<algorithm>
using namespace std;

const int alphabet_size=30;
const int up=2000+5;
int maxn=0;char chr[80];

struct Trie
{
    int ch[up][alphabet_size];bool val[up];
    int siz;
    Trie() { siz=1;memset(ch[0],0,sizeof(ch[0]));memset(val,0,sizeof(val)); }
    int idx(char c)  { return c-'a'; }
    void insert(char* s)
    {
        int u=0,n=strlen(s),v=1,c=0,cur=0;
        for(int i=0;i<n;i++)
        {
            c=idx(s[i]);
            if(val[u]) v++;
            if(!ch[u][c])
            {
                memset(ch[siz],0,sizeof(ch[siz]));
                ch[u][c]=siz++;
            }
            u=ch[u][c];
        }
        val[u]=1;
        if(maxn<v) maxn=v;
    }
} stree;

int main()
{
    int n;
    
    scanf("%d",&n);
    for(int i=0;i<n;i++)
    {
        scanf("%s",chr);
        stree.insert(chr);
    }
    printf("%d\n",maxn);
    return 0;
}
```

# 2.小胖的水果

## 描述

xuzhenyi到大同水果店去买水果，但老板huyichen告诉他每次只能买一种，但是xuzhenyi想吃两种，于是在讨价还价之后，huyichen说只要xuzhenyi能把他想要的两种水果合并成一种，就能成功。你能帮他吗？
## 格式

### 输入格式

输入文件包含两个要组合的水果名字。所有的名字最多有100个字母。(有若干行）
### 输出格式

对每一组测试数据，打印出一个最短的组合长度.
## 样例1

### 样例输入1

<pre>
apple peach
ananas banana
pear peach
</pre>

### 样例输出1

<pre>
8
7
6
</pre>

## 来源

huyichen

## 分析

答案就是字符串的长度减去两者的LCS的长度即可
所以直接写一个LCS的DP模板就好啦
然后答案就出来咯（作者按：此段引用）

代码：

``` cpp
#include<cstdio>
#include<iostream>
#include<algorithm>
#include<cstring>
#define lnt long long
using namespace std;

const int up=100+5;
char a[up],b[up];
int f[up][up];

int main()
{
    int len1,len2;

    while(~scanf("%s %s",a+1,b+1))
    {
        len1=strlen(a+1),len2=strlen(b+1);//又忘了
        memset(f,0,sizeof f);
        for(int i=1;i<=len1;i++)
            for(int j=1;j<=len2;j++)
                if(a[i]==b[j]) f[i][j]=f[i-1][j-1]+1;
                else f[i][j]=max(f[i-1][j],f[i][j-1]);
        printf("%d\n",len1+len2-f[len1][len2]);
    }

    return 0;
}
```

# 3.合唱队形

## 描述

N位同学站成一排，音乐老师要请其中的(N-K)位同学出列，使得剩下的K位同学排成合唱队形。
合唱队形是指这样的一种队形：设K位同学从左到右依次编号为1，2…，K，他们的身高分别为T1，T2，…，TK， 则他们的身高满足T1<...<Ti>Ti+1>…>TK(1<=i<=K)。
你的任务是，已知所有N位同学的身高，计算最少需要几位同学出列，可以使得剩下的同学排成合唱队形。
## 格式

### 输入格式

输入的第一行是一个整数N(2<=N<=100)，表示同学的总数。第一行有n个整数，用空格分隔，第i个整数Ti(130<=Ti<=230)是第i位同学的身高(厘米)。
### 输出格式

输出包括一行，这一行只包含一个整数，就是最少需要几位同学出列。
## 样例1

### 样例输入1

<pre>
8
186 186 150 200 160 130 197 220
</pre>

### 样例输出1

<pre>
4
</pre>

## 限制

每个测试点1s
## 来源

NOIp 2004

## 分析

正反两遍LIS，再取最大值

``` cpp
#include<iostream>
#include<cstdio>
#include<cstring>
#include<algorithm>
using namespace std;

const int up=100+5;
int a1[up],a2[up],f1[up],f2[up],g[up];

int main()
{
    int n,k,maxn=0;
    scanf("%d",&n);
    for(int i=1;i<=n;i++)
    {
    	scanf("%d",&a1[i]);
    	a2[n-i+1]=a1[i];
    }
    memset(g,0x7f,sizeof g);
    for(int i=1;i<=n;i++)
    {
    	k=lower_bound(g+1,g+n+1,a1[i])-g;
    	f1[i]=k;
    	g[k]=a1[i];
    }
    memset(g,0x7f,sizeof g);
    for(int i=1;i<=n;i++)
    {
    	k=lower_bound(g+1,g+n+1,a2[i])-g;
    	f2[n-i+1]=k;
    	g[k]=a2[i];
    }
    for(int i=1;i<=n;i++) maxn=max(maxn,f1[i]+f2[i]);
    printf("%d",n+1-maxn);
}
```