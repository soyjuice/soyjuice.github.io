---
layout: post
title: Pre:从零开始的游戏人生(一)
categories: [C++, 学习笔记]
description: 游戏编程
keywords: C++, 学习笔记
---

从今天起，我会零零星星更新这个分类。我从开始学编程，很大一部分目的就是为了去学习游戏编程，至于到现在，我才决定开始接触。<br/>

我使用的教科书是《逐梦旅程：WINDOWS游戏编程之从零开始》，我会一边看书，一边写点什么。

<pre>
生者，生者，路化冰河。
人生没有四季，唯有寒冬的荒野。
那流出的血泪，倘若不将其拭去，便会冻结成冰。
————浅井权三《G弦上的魔王》
</pre>

这是书上挑选的一句话，而我们所能见到的成型的游戏都是每一个设计师、程序员辛勤工作的结果，是让人尊敬的成果，推荐电影《Indie Game:The Movie》。

游戏类应用程序通常可以被分为图形用户接口(GUI)和引擎(Engine)这两个部分。

万丈高楼，始于平地，我需要更加努力。

## Windows编程体系与游戏编程

编写铁三角：C++、Windows API与图形库（DirectX或者OpenGL）。

而在VS中，有三种方式创建可交互式应用程序：

1.使用Windows API，也是以后学习的重点

2.使用MFC，微软基础类库

3.使用Windows Forms

## 两个术语——API与SDK

### API初识

API是微软提供的便于程序开发的各种各样的函数（可能有1000多种。。。），这些函数是Windows操作系统提供给应用程序的接口，一般情况下，一个好的程序员善于查询某个函数的作用，这就需要MSDN帮助文档了。

### SDK初识

SDK全称是Software Development Kit，就是软件开发包，例如DirectX SDK，它就是用DirectX进行开发的一个资源的打包集合。

后面讲到游戏引擎时，可以使用[ogre](http://www.ogre3d.org)，下载最新版本的ogre SDK。

## Windows程序中的main函数

Windows程序中也有类似于DOS程序中main()函数的WinMain()函数，WinMain()函数是所有Windows程序的入口点函数。

``` cpp
int WINAPI WinMain
(
    _In_ HINSTANCE hInstance,
    _In_ HINSTANCE hPrevInstance,
    _In_ LPSTR lpCmdLine,
    _In_ int nCmdShow
);
```

其中int后的WINAPI可以忽略，它在WinDef.h中定义是：

``` cpp
#define WINAPI __stdcall
#define CALLBACK __stdcall
```

可以看出也可以用CALLBACK代替。

另外函数的每个参数前的_In可以理解为一个宏，表示需要我们进行自行输入（input）的一个参数，与其对应的是_Out,表示这个参数是函数本身向外输出（output）的一个参数。

下面是各个参数的作用：

|类型|参数|介绍|
|:--:|:--:|----|
|HINSTANCE|hInstance|表示该程序当前运行的实例句柄|
|HINSTANCE|hPrevInstance|表示当前实例的前一个实例的句柄|
|LPSTR|lpCmdLine|一个以空终止的字符串，指定传递给运用程序的命令行参数|
|int|nCmdShow|指定程序窗口如何显示，如SW_HIDE(0,隐藏),SW_MAXIMIZE(3,最大化),|

另外，通过对nCmdShow这个值进行设置，可以使游戏窗口更加个性化。

## 简单的实验1-1

我们现在可以尝试着写一个小小的程序，为此我们需要新建一个项目。

在一个IDE上一般都会有新建项目，而项目就相当于一个收纳箱，里面是某个程序所需要的所有内容和组件。

``` cpp
#include<windows.h>

int WINAPI WinMain(HINSTANCE hInstance, HINSTANCE hPrevInstance, LPSTR lpCmdLine, int nCmdShow)
{
    MessageBox(NULL, "开始学习吧，Soy Juice！", "简单的实验", 0);
    
    return 0;
}
```

其中的MessageBox就是大家经常见到的消息框，函数原型是：

``` cpp
int WINAPI MessageBox(
    _In_opt_ HWND hWnd,
    _In_opt_ LPCTSTR lpText,
    _In_opt_ LPCTSTR lpCaption,
    _In_ UINT uType
);
```

_In_opt后面的_opt_，表示可选的（Optional）,二个词合在一起就表示“可选的输入参数”，也就是说可以像上面那样自己填内容。

|类型|参数|介绍|
|:--:|:--:|----|
|HWND|hWnd|表示我们显示消息框所属的窗口的句柄|
|LPCTSTR|lpText|显而易见|
|LPCTSTR|lpCaption|同样显而易见|
|UINT|uType|表示消息框的样式（可以自己查一下有哪些，不写了，打字太累，请原谅一个蒟蒻的懒）|

还有一个重要的事是，当要输入带双引号的字符串时，切记根据IDE的使用的字符集而适时添加L在双引号前，如`L"开始学习吧，Soy Juice！"`

## Windows程序窗口初识

窗口（Window）是一个Windows程序非常重要的一个东西，是程序与用户进行交互的接口，使程序可以接受用户输入、显示用户输出。

（相信大家都非常了解窗口是什么，所以就不赘述了）

## Windows资源的“坐标”——句柄

> 句柄（HANDLE），有多种意义，其中第一种是指程序设计，第二种是指Windows编程。现在大部分都是指程序设计/程序开发这类。

> 第一种解释：句柄是一种特殊的智能指针 。当一个应用程序要引用其他系统（如数据库、操作系统）所管理的内存块或对象时，就要使用句柄。

> 第二种解释：整个Windows编程的基础。一个句柄是指使用的一个唯一的整数值，即一个4字节(64位程序中为8字节)长的数值，来标识应用程序中的不同对象和同类中的不同的实例，诸如，一个窗口，按钮，图标，滚动条，输出设备，控件或者文件等。应用程序能够通过句柄访问相应的对象的信息，但是句柄不是指针，程序不能利用句柄来直接阅读文件中的信息。如果句柄不在I/O文件中，它是毫无用处的。

> 句柄是Windows用来标志应用程序中建立的或是使用的唯一整数，Windows大量使用了句柄来标识对象。

> ——百度百科

总而言之，句柄很常用，例如窗口由窗口句柄（HWND）标识，我们要对某个窗口进行操作，首先要得到它的句柄；句柄的种类也很多，比如画刷句柄（HBRUSH）、图标句柄（HICON）、光标句柄（HCURSOR）等。

想要更多地了解句柄，参见[句柄_百度百科](http://baike.baidu.com/item/%E5%8F%A5%E6%9F%84){:target="_blank"}、[句柄 - 维基百科，自由的百科全书](https://zh.wikipedia.org/wiki/%E5%8F%A5%E6%9F%84?){:target="_blank"}。

## Windows程序的“邮局”——消息与消息队列

Windows程序是基于事件驱动方式的程序设计模式，Windows程序与操作系统之间的通信主要是基于消息的，消息产生后进入消息队列（FIFO表），然后一个个处理。

### 消息的表示形式——MSG结构体

``` cpp
typedef struct tagMSG
{
    HWND hwnd; //指定消息所属窗口
    UINT message; //指定消息的标识符
    WPARAM wParam; //指定此消息的附加信息
    LPARAM lParam; //指定此消息的附加信息
    DWORD time; //指定投递到消息队列的时间
    POINT pt; //指定投递到消息队列中时鼠标的当前位置
} MSG;
```

关于`UINT message;`，也是可以使用特定的宏，如`WM_RBUTTONDOWN`（鼠标右键按下的消息）、`WM_LBUTTONDOWN`（鼠标左键按下的消息）、`WM_QUIT`（退出消息）、`WM_KEYDOWN`（键盘按下的消息）。

### 消息队列

顾名思义，是个队列。

——Soy Juice，2017.4.18~2017.4.25，学校机房。
