---
title: Linux入门1-基本指令
date: 2024-04-27 16:46:39
categories:
- Linux
tags:
- Linux
---
<meta name="referrer" content="no-referrer" />

<!-- toc -->

## 1.指令入门

### 1.1 基础指令

- 显示日期与时间的指令： date
- 显示日历的指令： cal
- 简单好用的计算机： bc

#### 1.1.1 显示日期的指令： date

显示当前Linux系统时间

```
$ date
Sat Apr 27 16:02:39 CST 2024
```

data的格式化输出：

```
$ date +%Y/%m/%d
2024/04/27

$ date +%H:%M
16:03
```

#### 1.1.2 显示日历的指令： cal

```
$ cal [month] [year]
```



```
$ cal
     April 2024
Su Mo Tu We Th Fr Sa
    1  2  3  4  5  6
 7  8  9 10 11 12 13
14 15 16 17 18 19 20
21 22 23 24 25 26 27
28 29 30
```



```
$ cal 2024
                            2024
      January               February               March
Su Mo Tu We Th Fr Sa  Su Mo Tu We Th Fr Sa  Su Mo Tu We Th Fr Sa
    1  2  3  4  5  6               1  2  3                  1  2
 7  8  9 10 11 12 13   4  5  6  7  8  9 10   3  4  5  6  7  8  9
14 15 16 17 18 19 20  11 12 13 14 15 16 17  10 11 12 13 14 15 16
21 22 23 24 25 26 27  18 19 20 21 22 23 24  17 18 19 20 21 22 23
28 29 30 31           25 26 27 28 29        24 25 26 27 28 29 30
                                            31

       April                  May                   June
Su Mo Tu We Th Fr Sa  Su Mo Tu We Th Fr Sa  Su Mo Tu We Th Fr Sa
    1  2  3  4  5  6            1  2  3  4                     1
 7  8  9 10 11 12 13   5  6  7  8  9 10 11   2  3  4  5  6  7  8
14 15 16 17 18 19 20  12 13 14 15 16 17 18   9 10 11 12 13 14 15
21 22 23 24 25 26 27  19 20 21 22 23 24 25  16 17 18 19 20 21 22
28 29 30              26 27 28 29 30 31     23 24 25 26 27 28 29
                                            30
....(以下省略)....
```



```
$ cal 5 2001
      May 2001
Su Mo Tu We Th Fr Sa
       1  2  3  4  5
 6  7  8  9 10 11 12
13 14 15 16 17 18 19
20 21 22 23 24 25 26
27 28 29 30 31
```



#### 1.1.3 简单好用的计算机： bc



```
$ bc
bc 1.07.1
Copyright 1991-1994, 1997, 1998, 2000, 2004, 2006, 2008, 2012-2017 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type `warranty'.
99*99
9801

```

- \+ 加法
- \- 减法
- \* 乘法
- / 除法
- ^ 指数
- % 余数
- quit 离开



> 从上面的练习我们大概可以知道在指令列模式里面下达指令时，会有两种主要的情况：
>
> - 一种是该指令会直接显示结果然后回到命令提示字符等待下一个指令的输入;
>
> - 一种是进入到该指令的环境，直到结束该指令才回到命令提示字符环境。
>
>   
>
>   <img src="https://gitee.com/tosfk/blog-pic/raw/master/202404271608543.gif" alt="指令下达的环境" style="zoom: 67%;" />



### 1.2 重要热键 [Tab]， [ctrl]-c， [ctrl]-d

#### 1.2.1 [Tab]按键

功能：**命令补全** 与 **档案补齐**

- [Tab] 接在一串指令的第一个字的后面，则为『命令补全』;
- [Tab] 接在一串指令的第二个字以后时，则为『档案补齐』！
- 若安装 bash-completion 软件，则在某些指令后面使用 [tab] 按键时，可以进行『选项/参数的补齐』功能！

```
$ g[Tab][Tab]
Display all 131 possibilities? (y or n)
g++                    gcc-ranlib-11          getconf                gold                   gpupdate.exe
g++-11                 gcc-ranlib.exe         getent                 gpapi.dll              gpupvdev.dll
g++.exe                gcc.exe                getevent.types.ps1xml  gpasswd                grb.rs
g711codc.ax            gcdef.dll              getkeycodes            gpedit.dll             grep
....(以下省略)....
```

#### 1.2.2 [Ctrl]-c 按键

功能：将正在运作中的指令中断

#### 1.2.3 [shift]+{[PageUP]|[ Page Down]}按键

功能：使用 [Shift]+[Page Up] 来往前翻页，也能够使用 [Shift]+[Page Down] 来往后翻页