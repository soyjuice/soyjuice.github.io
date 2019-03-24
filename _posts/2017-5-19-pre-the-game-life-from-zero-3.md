---
layout: post
title: Pre:从零开始的游戏人生(三)
categories: [C++, 学习笔记]
description: 游戏编程
mini-description: 看来得加快速度了
keywords: C++, 学习笔记
---

在本文开始以前，先来看两个函数：

``` cpp
WINUSERAPI WINBOOL WINAPI GetMessage(
    LPMSG lpMsg,
    HWND hWnd,
    UINT wMsgFilterMin,
    UINT wMsgFilterMax
);
WINUSERAPI WINBOOL WINAPI PeekMessage(
    LPMSG lpMsg,
    HWND hWnd,
    UINT wMsgFilterMin,
    UINT wMsgFilterMax,
    UINT wRemoveMsg
);
```

## 很重要的消息循环体系

完成窗口的创建以后，我们还需要编写一个消息循环，不断从消息队列中取出消息，并进行响应。

而这就利用到了上面两个函数，利用它们的优劣完成消息接收部分。

### 以GetMessage为核心的消息循环体系

回到上面那个函数

``` cpp
WINUSERAPI WINBOOL WINAPI GetMessage(
    LPMSG lpMsg, //指向一个消息（MSG）结构体
    HWND hWnd, //指定接收哪一个窗口的消息
    UINT wMsgFilterMin, 
    UINT wMsgFilterMax //指定获取消息的最小值和最大值，通常设置为0，而如果两个都为0的话，就代表全部接收
);
```

于是就有了以下代码：

``` cpp
MSG msg = {0};
while(GetMessage(&msg, NULL, 0, 0))
{
    TranslateMessage(&msg);
    DispatchMessage(&msg);
}
```

首先先声明一个消息结构体的msg，接下来不断从消息队列中取出消息

### STOP!!!

此处是2019.3.24，隔了一年这篇还是没有写完，所以我也不打算现在写，毕竟有的是时间嘛。

To be continued.
