---
layout: post
title: Pre:从零开始的游戏人生(二)
categories: [C++, 学习笔记]
description: 游戏编程
mini-description: 继上一篇，继续学习
keywords: C++, 学习笔记
---

继上一篇，继续学习。

## 开始吧，Windows窗口创建

建立一个完整的窗口，一般需要四步：

1.窗口类的设计

2.窗口类的注册

3.窗口的正式创建

4.窗口的显示与更新

我们挨个学习。

### 窗口类的设计

``` cpp
typedef struct WNDCLASSEX 
{
    UINT cbSize;
    UINT style;
    WNDPROC lpfnWndProc;
    int cbClsExtra;
    int cbWndExtra;
    HINSTANCE hInstance;
    HICON hIcon;
    HCURSOR hCursor;
    HBRUSH hbrBackground;
    LPCTSTR lpszMenuName;
    LPCTSTR lpszClassName;
    HICON hIconSm;
} WNDCLASSEX, *PWNDCLASSEX;
```

上面是较新的WNDCLASSEX的定义，下面将会一步步详细讲解：

首先，先声明一个窗口类

``` cpp
WNDCLASSEX wndClass = {0};
```

第一个参数，UINT的cbSize，表示该结构体的字节数大小,没太大实际意义

``` cpp
wndClass.cbSize = sizeof(WNDCLASSEX);
```

第二个参数，UINT的style，指定窗口的样式，用“CS_”开头的宏

``` cpp
wndClass.style = CS_HREDRAW | CS_VREDRAW;
```

第三个参数，WNDPROC的lpfnWndProc，它是一个函数指针，指向窗口过程函数，而窗口过程函数是一个回调函数。

> 回调函数就是一个通过函数指针调用的函数。如果你把函数的指针（地址）作为参数传递给另一个函数，当这个指针被用来调用其所指向的函数时，我们就说这是回调函数。回调函数不是由该函数的实现方直接调用，而是在特定的事件或条件发生时由另外的一方调用的，用于对该事件或条件进行响应。

> ——百度百科

另外，针对Windows的消息处理机制，窗口过程函数被调用的过程就是这样：

1.设计窗口类的时候，将窗口过程函数的地址赋值给lpfnWndProc成员变量。

2.调用`RegsiterClass(&wndclass)`注册窗口类，那么系统就有了我们所编写的窗口过程函数的地址。

3.当应用程序接收到某一窗口的消息时，调用`DispatchMessage(&msg)`将消息回传给系统。系统则利用先前注册窗口类是得到的函数指针，调用窗口过程函数时对消息进行处理。

值得注意的是，一个Windows程序可以包含多个窗口过程函数，而一个窗口过程函数总是与某一个特定的窗口类相关联，基于该窗口类创建的窗口使用的是同一个窗口过程。

``` cpp
wndClass.lpfnWndProc = WndProc;
```

第四个参数，int的cbClsExtra，表示窗口类的附加内存。一般设为0就好了

``` cpp
wndClass.cbClsExtra = 0;
```

第五个参数，int的cbWndExtra，可以猜到，表示窗口的附加内存。一般也设为0

``` cpp
wndClass.cbWndExtra = 0;
```

第六个参数，HINSTANCE的hInstance，指定包含窗口过程的程序的实例句柄，我们要做的就是把WinMain函数的第一个参数，也就是程序当前运行的实例句柄赋给它

``` cpp
wndClass.hInstance = hInstance;
```

第七个参数，HICON的hIcon，用于指定窗口类的图标句柄。这个成员变量必须是一个图标资源的句柄，如果为NULL，那么系统将会提供一个默认的图标。

在为hIcon赋值时，我们可以调用LoadIcon加载一个图片资源，并将返回值赋回hIcon

``` cpp
HICON WINAPI LoadIcon(
    _In_opt_ HINSTANCE hInstance,
    _In_ LPCTSTR lpIconName
);
```

对于LoadIcon，值得注意的是，如果要使用系统自带的图标，第一个参数必须为NULL。

当然，这样的方法还是有可能使用不了我想用的图片，所以我们可以使用：

``` cpp
wndClass.hIcon = (HICON)::LoadImage(NULL, "icon.ico", IMAGE_ICON, 0, 0, LR_DEFAULTSIZE | LR_LOADFROMFILE);
```

第八个参数，HCURSOR的hCursor，类似于第七个参数，也有个函数

``` cpp
HCURSOR WINAPI LoadCursor(
    _In_opt_ HINSTANCE hInstance,
    _In_ LPCTSTR lpCursorName
);
```

使用默认就好了

``` cpp
wndClass.hCursor = LoadCursor(NULL, IDC_ARROW);
```

第九个参数，HBRUSH的hbrBackground，指定窗口类的背景画刷。前缀hbr表示是一个画刷句柄（handle to brush）。我们同样需要一个函数

``` cpp
HGDIOBJ GetStockObject(
    __in int fnObject
);
```

看起来挺麻烦的，所以就不详述了，直接使用

``` cpp
wndClass.hbrBackground = (HBRUSH)GetStockObject(GRAY_BRUSH);
```

第十个参数，LPCTSTR的lpszMenuName，指定菜单资源的名字，如果不需要下拉菜单，赋值NULL即可

``` cpp
wndClass.lpszMenuName = NULL;
```

第十一个参数，LPCTSTR的lpszClassName，指定窗口类的名字，随便起一个好了：

``` cpp
wndClass.lpszClassName = "This is a test";
```

第十二个参数，HICON的hIconSm，指定窗口类的小图标句柄，也就是屏幕右下角的托盘区的小图标，虽然这个参数是WNDCLASS与WNDCLASS之间的区别，但是对于游戏编程，我们并不用太理会，可以赋作NULL。

总结起来就是：

``` cpp
WNDCLASSEX wndClass = {0};
wndClass.cbSize = sizeof(WNDCLASSEX);
wndClass.style = CS_HREDRAW | CS_VREDRAW;
wndClass.lpfnWndProc = WndProc;
wndClass.cbClsExtra = 0;
wndClass.hInstance = hInstance;
wndClass.hIcon = (HICON)::LoadImage(NULL, "icon.ico", IMAGE_ICON, 0, 0, LR_DEFAULTSIZE | LR_LOADFROMFILE);
wndClass.hCursor = LoadCursor(NULL, IDC_ARROW);
wndClass.hbrBackground = (HBRUSH)GetStockObject(GRAY_BRUSH);
wndClass.lpszMenuName = NULL;
wndClass.lpszClassName = "This is a test";
wndClass.hIconSm = NULL;
```

### 窗口类的注册

``` cpp
ATON WINAPI RegisterClassEX(
    _In_ const WNDCLASSEX *lpwcx
);
```

就好像注册某个网站的账号，填完注册信息后，当然要选择完成注册一样，设计好窗口类后，需要对其进行注册(使用窗口类声明的类名)

``` cpp
RegisterClassEx(&wndClass);
```

另外，由于我们使用的是升级版（+EX），注册的函数也是升级版（+Ex）。

### 窗口的正式创建

``` cpp
HWND WINAPI CreateWindow(
    _In_opt_ LPCTSTR lpClassName,
    //对应窗口类的名称
    _In_opt_ LPCTSTR lpWindowName,
    //创建的窗口的名字
    _In_ DWORD dwStyle,
    //创建的窗口的样式，跟上文style不同的是，style指定所有窗口的样式，而dwStyle指定某个具体的窗口
    _In_ int x,
    //水平位置
    _In_ int y,
    //竖直位置
    _In_ int nWidth,
    //窗口高度
    _In_ int nHeight,
    //窗口宽度
    _In_opt_ HWND hWndParent,
    //父窗口句柄，可选可不选，一般设为NULL
    _In_opt_ HMENU hMenu,
    //窗口菜单的资源句柄
    _In_opt_ HANDLE hInstance,
    //参见WinMain的参数
    _In_opt_ LPVOID lpParam
    //其实我没看懂，设成NULL好了
);
```

偷懒把讲解写在代码上的感觉真好~

另外，CreateWindow也有Ex后缀的CreateWindowEx，在最前面加了一个参数`DWORD dwExStyle`

代码上就这么写好了：

``` cpp
HWND hWnd = CreateWindow("This is a test", 
    "This is a test",
    WS_OVERLAPPEDWINDOW, CW_USEDEFAULT, CW_USEDEFAULT, 800,
    600, NULL, NULL, hInstance, NULL
);
```

和

``` cpp
HWND hWnd = CreateWindowEx(WS_EX_CLIENTEDGE, "This is a test", 
    "This is a test", 
    WS_OVERLAPPEDWINDOW, CW_USEDEFAULT, CW_USEDEFAULT, 800, 
    600, NULL, NULL, hInstance, NULL
);
```

### 窗口的显示和更新

#### 改变窗口位置和大小

废话少说，直接上函数

``` cpp
BOOL WINAPI MoveWindow(
    _In_ HWND hWnd,
    //设为创建的窗口的句柄
    _In_ int X,
    _In_ int Y,
    _In_ int nWidth,
    _In_ int nHeight,
    //以上四个同上
    _In_ BOOL bRepaint
    //指定了是否重画窗口，如果为true，会使窗口接收到一条WM_PAINT消息；反之，不进行重画
);
```

#### 显示窗口

创建完后，当然需要显示出来，这就需要

``` cpp
BOOL WINAPI ShowWindow(
    _In_ HWND hWnd,
    //同上
    _In_ int nCmdShow
    //参见WinMain的参数
);
```

#### 更新窗口

最后如果要彻底完成窗口的改动，需要在上两个函数后加上以下函数

``` cpp
BOOL UpdateWindow(
    __in HWND hWnd
    //同上上
);
```

用它完成收尾工作，就好比买了新房子要装修一样（作者按：教材书作者生动的比喻）

### 窗口的显示和更新的总结

总结代码如下：

``` cpp
MoveWindow(hWnd, 200, 50, 800, 600, true);
ShowWindow(hWnd, nShowCmd);
UpdateWindow(hWnd);
```

## 全文总结

经过详尽而细致地学习，我对如何创建窗口有了一定的了解。

不过在实际编程中，窗口的创建是每个Windows程序必有的，一般的IDE都会在新建的项目代码中直接加入固定的模（tao）板（lu），所以说，并不需要去背代码（原谅我的懒）

——Soy Juice，2017.5.7~2017.5.16，学校机房。