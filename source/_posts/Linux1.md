---
title: Linux入门1-基本操作、指令与在线求助
date: 2024-04-27 16:46:39
categories:
- Linux
tags:
- Linux
---
<meta name="referrer" content="no-referrer" />

<!-- toc -->

# 1 登录/注销系统

在Linux系统中由于是多人多工的环境，所以系统随时都有很多不同的用户所下达的任务在进行， 因此正确的开关机非常很重要。不正常的关机可能会导致档案系统错乱，造成资料的毁损，这也是为什么通常我们的Linux主机都会加挂一个不断电系统。

一般不建议直接使用 root 的身份登入系统。请使用一般账号登入，等到有需要修改或者是建立系统相关的管理工作时， 才切换身份成为 root。因为系统管理员的权限太高了，而 Linux 底下很多的指令行为是'没有办法复原'的。所以， 使用一般账号时，'手滑'的灾情会比较不严重。

因此，一个称职的网络/系统管理人员，通常都会具有两个账号，平时以自己的一般账号来使用Linux主机的任何资源， 有需要动用到系统功能修订时，才会转换身份成为root。所以，鸟哥强烈建议你建立一个普通的帐号来供自己平时使用。

## 1.1 终端接口登入linux

自动登录或输入密码

## 1.2 离开/注销Linux：

```
$ exit
```

就能够注销Linux了。 但是请注意：'离开系统并不是关机！' 基本上，Linux本身已经有相当多的工作在进行，你的登入也仅是其中的一个'工作'而已， 所以当你离开时，这次这个登入的工作就停止了，但此时Linux其他的工作是还是继续在进行的。本章后面我们再来提如何正确的关机，这里先建立起这个概念即可。



# 2 基础指令

我们都是通过'程序'在跟系统作沟通的，本章上面提到的窗口管理员或文字模式都是一组或一只程序在负责我们所想要完成的任务。 文字模式登录后所取得的程序被称为壳（Shell），这是因为这支程序负责最外面跟用户（我们）沟通，所以才被戏称为壳程序。

指令结构

```
$ command  [-options]  parameter1  parameter2 ...
     指令     選項        參數(1)     參數(2)
```

1. 一行指令中第一个输入的部分绝对是'指令（command）'或'可执行文件（例如批次脚本，script）'
2. command 为指令的名称，例如变换工作目录的指令为 cd 等等;
3. 中刮号[]并不存在于实际的指令中，而加入选项设定时，通常选项前会带 - 号，例如 -h;有时候会使用选项的完整全名，则选项前带有 -- 符号，例如 --help;
4. parameter1 parameter2.. 为依附在选项后面的参数，或者是 command 的参数;
5. 指令， 选项， 参数等这几个咚咚中间以空格来区分，不论空几格 shell 都视为一格。 所以空格是很重要的特殊字符！;
6. 按下[Enter]按键后，该指令就立即执行。 [Enter]按键代表着一行指令的开始启动。
7. 指令太长的时候，可以使用反斜线 （\） 来跳脱 [Enter] 符号，使指令连续到下一行。 注意！反斜线后就立刻接特殊字符，才能跳脱！
8. 其它：在 Linux 系统中，英文大小写字母是不一样的。 举例来说， CD 与 CD 并不同。



### 2.1 显示日期的指令： date

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

### 2.2 显示日历的指令： cal

```
$ cal [month] [year]
```



```
$ cal
```

```
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
```

```
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
```

```
      May 2001
Su Mo Tu We Th Fr Sa
       1  2  3  4  5
 6  7  8  9 10 11 12
13 14 15 16 17 18 19
20 21 22 23 24 25 26
27 28 29 30 31
```



### 2.3 简单好用的计算机： bc

```
$ bc
```

```
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



# 3 重要热键 [Tab]， [ctrl]-c， [ctrl]-d

### 3.1 [Tab]按键

功能：**命令补全** 与 **档案补齐**

- [Tab] 接在一串指令的第一个字的后面，则为『命令补全』;
- [Tab] 接在一串指令的第二个字以后时，则为『档案补齐』！
- 若安装 bash-completion 软件，则在某些指令后面使用 [tab] 按键时，可以进行『选项/参数的补齐』功能！

```
$ g[Tab][Tab]
```

```
Display all 131 possibilities? (y or n)
g++                    gcc-ranlib-11          getconf                gold                   gpupdate.exe
g++-11                 gcc-ranlib.exe         getent                 gpapi.dll              gpupvdev.dll
g++.exe                gcc.exe                getevent.types.ps1xml  gpasswd                grb.rs
g711codc.ax            gcdef.dll              getkeycodes            gpedit.dll             grep
....(以下省略)....
```

### 3.2 [Ctrl]-c 按键

功能：将正在运作中的指令中断

### 3.3 [Ctrl]-d 按鍵

键盘输入结束（End Of File， EOF 或 End Of Input）

可以用来取代exit的输入

### 3.4 [shift]+{[PageUP]|[ Page Down]}按键

功能：使用 [Shift]+[Page Up] 来往前翻页，也能够使用 [Shift]+[Page Down] 来往后翻页



# 4 在线求助man page与info page

## 4.1 指令--help求助说明

```
$ date --help
```

```
Usage: date [OPTION]... [+FORMAT]
  or:  date [-u|--utc|--universal] [MMDDhhmm[[CC]YY][.ss]]
Display the current time in the given FORMAT, or set the system date.

Mandatory arguments to long options are mandatory for short options too.
  -d, --date=STRING          display time described by STRING, not 'now'
      --debug                annotate the parsed date,
                              and warn about questionable usage to stderr
  -f, --file=DATEFILE        like --date; once for each line of DATEFILE
....(省略)....

FORMAT controls the output.  Interpreted sequences are:

  %%   a literal %
  %a   locale's abbreviated weekday name (e.g., Sun)
  %A   locale's full weekday name (e.g., Sunday)
....(省略)....
 
By default, date pads numeric fields with zeroes.
The following optional flags may follow '%':

  -  (hyphen) do not pad the field
  _  (underscore) pad with spaces
  0  (zero) pad with zeros
....(省略)....

After any flags comes an optional field width, as a decimal number;
then an optional modifier, which is either
E to use the locale's alternate representations if available, or
O to use the locale's alternate numeric symbols if available.

Examples:
Convert seconds since the epoch (1970-01-01 UTC) to a date
  $ date --date='@2147483647'

Show the time on the west coast of the US (use tzselect(1) to find TZ)
  $ TZ='America/Los_Angeles' date

Show the local time for 9AM next Friday on the west coast of the US
  $ date --date='TZ="America/Los_Angeles" 09:00 next Fri'
```

通常` --help` 用在协助你查询『你曾经用过的指令所具备的选项与参数』而已， 如果要使用的是从来没有用过得指令，或者要查询的根本就不是指令，而是文件的'格式'时，那就得要透过 man page。



## 4.2  man page

```
$ man date
```

进入man指令的功能后，你可以按下'空白键'往下翻页，可以按下' q '按键来离开man的环境。

指令的完整全名，如下所示為date且說明簡單用途為設定與顯示日期/時間：

```
NAME
       date - print or set the system date and time
```

指令的基本語法如下所示：

```
SYNOPSIS
       date [OPTION]... [+FORMAT]
       date [-u|--utc|--universal] [MMDDhhmm[[CC]YY][.ss]]
```

詳細說明剛剛語法談到的選項與參數的用法：

```
DESCRIPTION  
       Display the current time in the given FORMAT, or set the system date.

       Mandatory arguments to long options are mandatory for short options too.

       -d, --date=STRING  <==左邊-d為短選項名稱，右邊--date為完整選項名稱
              display time described by STRING, not 'now'
              ....(中間省略)....
```

表格第一行：

```
DATE(1)                                             User Commands                                             DATE(1)
```

（1）代表的是'一般用户可使用的指令'的意思

| 代号  | 代表内容                                                     |
| ----- | ------------------------------------------------------------ |
| ==1== | 用户在shell环境中可以操作的指令或可执行文件                  |
| 2     | 系统核心可调用的函数与工具等                                 |
| 3     | 一些常用的函数（function）与函式库（library），大部分为C的函式库（libc） |
| 4     | 装置档案的说明，通常在/dev下的档案                           |
| ==5== | 配置文件或者是某些文件的格式                                 |
| 6     | 游戏（games）                                                |
| 7     | 惯例与协议等，例如Linux档案系统、网路协定、ASCII code等等的说明 |
| ==8== | 系统管理员可用的管理指令                                     |
| 9     | 跟kernel有关的文件                                           |

透过这张表格的说明， 未来你如果使用man page在察看某些数据时，就会知道该指令/档案所代表的基本意义是什么了。 举例来说，如果你下达了'man null'时，会出现的第一行是：'NULL（4）'，对照一下上面的数字意义，null竟然是一个'装置档案'。



### 4.2.1 man page结构

| 代号        | 内容说明                                                     |
| ----------- | ------------------------------------------------------------ |
| NAME        | 简短的指令、数据名称说明                                     |
| SYNOPSIS    | 简短的指令下达语法（syntax）简介                             |
| DESCRIPTION | 较为完整的说明，这部分最好仔细看看！                         |
| OPTIONS     | 针对 SYNOPSIS 部分中，有列举的所有可用的选项说明             |
| COMMANDS    | 当这个程序（软件）在执行的时候，可以在此程序（软件）中下达的指令 |
| FILES       | 此程序或数据所使用或参考或链接到的某些文件                   |
| SEE ALSO    | 可以参考的，跟这个指令或资料有相关的其他说明！               |
| EXAMPLE     | 一些可以参考的范例                                           |

可以在任何时候输入『/word』，来主动搜索关键字

当你按下'/'之后，光标就会移动到屏幕的最下面一行， 并等待你输入搜索的字符串了



**常用按键**

| 按键        | 进行工作                                                     |
| ----------- | ------------------------------------------------------------ |
| 空白键      | 向下翻一页                                                   |
| [Page Down] | 向下翻一页                                                   |
| [Page Up]   | 向上翻一页                                                   |
| [Home]      | 去到第一页                                                   |
| [End]       | 去到最后一页                                                 |
| /string     | 向'下'搜寻 string 这个字符串，如果要搜索 vbird 的话，就输入 /vbird |
| ?string     | 向'上'搜寻 string 这个字符串                                 |
| n, N        | 利用 / 或 ？ 搜索字符串时，可以用 n 来继续下一个搜索 （ 不论是 / 或 ？ ） ，可以利用 N 来进行'反向'搜寻。 举例来说，我以 /vbird 搜寻 vbird 字串， 那么可以 n 继续往下查询，用 N 往上查询。 若以 ？vbird 向上查询 vbird 字符串， 那我可以用 n 继续'向上'查询，用 N 反向查询。 |
| q           | 结束这次的 man page                                          |



### 4.2.2 搜索特定命令/文件的man page说明文件

知道要使用某些特定的指令或者是修改某些特定的设定文件，但是偏偏忘记了该指令的完整名称。 有些时候则是你只记得该指令的部分关键词。 这个时候你要如何查出来你所想要知道的man page呢

```
$ man -f man
```

```
man (1)              - an interface to the system reference manuals
man (7)              - macros to format man pages
```

搜索的顺序是记录在/etc/man_db.conf 这个配置文件当中， 先搜寻到的那个说明文件，就会先被显示出来

```
$ man 1 man  <==這裡是用 man(1) 的文件資料
$ man 7 man  <==這裡是用 man(7) 的文件資料
```



使用'man -f 指令'时，man只会找数据中的左边那个指令（或档案）的完整名称

如果想要找的是'关键词'呢？也就是说，想要同时找上面说的两个地方的内容，只要该内容有关键词存在， 不需要完全相同的指令（或档案）就能够找到时，该怎么办？

```
$ man -k man
```

```
fallocate (2)        - manipulate file space
zshall (1)           - the Z shell meta-man page
....(中間省略)....
yum-config-manager (1) - manage yum configuration options and yum repositories
yum-groups-manager (1) - create and edit yum's group metadata
yum-utils (1)        - tools for manipulating repositories and extended package management
```



还有两个指令与man page有关，这两个指令是man的简略写法：

```
$ whatis  [指令或者是資料]   <==相當於 man -f [指令或者是資料]
$ apropos [指令或者是資料]   <==相當於 man -k [指令或者是資料]
```



##  4.3 info page

info与man的用途其实差不多，都是用来查询指令的用法或者是档案的格式。 

但是与man page一口气输出一堆信息不同的是**，info page则是将文件数据拆成一个一个的段落，每个段落用自己的页面来撰写， 并且在各个页面中还有类似网页的'超链接'来跳到各不同的页面中，每个独立的页面也被称为一个节点（node）**。所以，你可以将info page想成是文字模式的网页显示资料



## 4.4 其他有用的文件（documents）

一般而言，指令或者软件制作者，都会将自己的指令或者是软件的说明制作成'线上说明文件'。 还有相当多的说明需要额外的文件。此时，这个所谓的 How-To（如何做的意思）就很重要。还有，某些软件不只告诉你'如何做'，还会有一些相关的原理会说明。

这些说明文件摆在/usr/share/doc这个目录

举例来说，你可能会先想要知道 grub2 这个新版的开机管理软件有什么能使用的指令？那可以到底下的目录瞧瞧：

> /usr/share/doc/grub2-tools-2.02

另外，很多原版软件释出的时候，都会有一些安装须知、预计工作事项、未来工作规划等等的东西，还有包括可安装的程序等， 这些档案也都放置在 /usr/share/doc 当中。而且/usr/share/doc这个目录下的数据主要是以套件（packages）为主的， 例如 nano 这个软件的相关信息在 /usr/share/doc/nano-xxx（xxx表示版本）。



## 4.5 总结

- 在终端模式中，如果你知道某个指令，但却忘记了相关选项与参数，请先善用**--help** 的功能来查询相关信息;
- 当有任何你不知道的指令或档案格式这种玩意儿，但是你想要了解他，请赶快使用**man**或者是**info**来查询！
- 而如果你想要架设一些其他的服务，或想要利用一整组软件来达成某项功能时，请赶快到**/usr/share/doc** 底下查一查有没有该服务的说明档喔！



# 5 简易文书编辑器： nano

nano的使用其实很简单，你可以直接加上文件名就能够开启一个旧档或新档！底下我们就来开启一个名为text.txt的文件名来看看：

```
$ nano text.txt
```

<img src="https://gitee.com/tosfk/blog-pic/raw/master/202404281158612.png" alt="image-20240428115839513" style="zoom:50%;" />

比较重要的几个组合按键：

- [ctrl]-G：取得在线说明（help），很有用的！
- [ctrl]-X：离开nano软件，若有修改过档案会提示是否需要储存喔！
- [ctrl]-O：储存档案，若你有权限的话就能够储存档案了;
- [ctrl]-R：从其他档案读入资料，可以将某个档案的内容贴在本档案中;
- [ctrl]-W：搜索字符串，这个也是很有帮助的指令喔！
- [ctrl]-C：说明目前光标所在处的行数与列数等信息;
- [ctrl]-_：可以直接输入行号，让光标快速移动到该行;
- [alt]-Y：校正语法功能开启或关闭（单击开、再按一下关）
- [alt]-M：可以支持鼠标来移动游标的功能



# 6 正确的关机方法

在 Windows （非 NT 主机系统） 系统中，由于是单人假多工的情况，所以即使你的电脑关机， 对于别人应该不会有影响.不过在 Linux 底下，由于每个程序 （或者说是服务） 都是在在背景下执行的，因此，在你看不到的屏幕背后其实可能有相当多人同时在你的主机上面工作， 例如浏览网页啦、传送信件啦以 FTP 传送档案等，如果你直接按下电源开关来关机时， 则其他人的数据可能就此中断。

此外，最大的问题是，**若不正常关机，则可能造成档案系统的毁损**（因为来不及将数据回写到档案中，所以有些服务的档案会有问题！）。 所以正常情况下，要关机时需要注意底下几件事：

- **观察系统的使用状态**：
  如果要看目前有谁在线上，可以下达'who'这个指令，而如果要看网络的连线状态，可以下达 『 netstat -a 』这个指令，而要看背景执行的程序可以执行『 ps -aux '这个指令。 使用这些指令可以让你稍微了解主机目前的使用状态！当然啰，就可以让你判断是否可以关机了 （这些指令在后面Linux常用指令中会提及喔！）

- **通知在线用户关机的时刻**：
  要关机前总得给线上的用户一些时间来结束他们的工作，所以，这个时候你可以使用 shutdown 的特别指令来达到此一功能。
- **正确的关机指令使用**：
  例如 shutdown 与 reboot 两个指令！



所以底下我们就来谈一谈几个与关机/重新开机相关的指令

- 将数据同步写入硬盘中的命令： sync
- 惯用的关机指令： shutdown
- 重新开机，关机： reboot， halt， poweroff



## 6.1 数据同步写入磁盘： sync

在Linux系统中，为了加快数据的读取速度，所以在预设的情况中， 某些已经加载内存中的资料将不会直接被写回硬盘，而是先暂存在内存当中。

万一系统因为某些特殊情况造成不正常关机时，由于数据尚未被写入硬盘当中，就会造成资料的更新不正常。 这个时候就需要sync这个指令来进行数据的写入动作。

直接在文字界面下输入sync，那么在内存中尚未被更新的数据，就会被写入硬盘中。所以，这个指令在系统关机或重新开机之前，最好多执行几次。虽然目前shutdown/reboot/halt 等等指令均已经在关机前进行了 sync 这个工具的呼叫，不过，多做几次总是比较放心。

```
$ su -   # 這個指令在讓你的身份變成 root ！底下請輸入 root 的密碼！
Password:  # 就這裡！請輸入安裝時你所設定的 root 密碼！
Last login: Mon Jun  1 16:10:12 CST 2015 on pts/0

[root@study ~]# sync
```

sync也可以被一般账号使用。只不过一般帐号用户所更新的硬盘数据就仅有自己的资料，不像root可以更新整个系统中的资料。



## 6.2 惯用的关机指令： shutdown

由于Linux的关机是那么重要的工作，因此除了你是在主机前面以实体终端机 （tty1~tty7） 来登入系统时， 不论用什么身份都能够关机之外，若你是使用远程管理工具（如透过pietty使用ssh服务来从其他电脑登入主机）， 那关机就只有root有权力.

我们较常使用的是shutdown这个指令，而这个指令会通知系统内的各个程序 （processes），并且将通知系统中的一些服务来关闭。 shutdown可以达成如下的工作：

- 可以自由选择关机模式：是要关机或重新开机均可;
- 可以设定关机时间： 可以设定成现在立刻关机， 也可以设定某一个特定的时间才关机。
- 可以自定义关机消息：在关机之前，可以将自己设定的讯息传送给在线 user 。
- 可以仅发出警告讯息：有时有可能你要进行一些测试，而不想让其他的用户干扰，或者是明白的告诉用户某段时间要注意一下！这个时候可以使用 shutdown 来吓一吓用户，但却不是真的要关机啦！

shutdown的语法：

```
# /sbin/shutdown [-krhc] [時間] [警告訊息]
選項與參數：
-k     ： 不要真的關機，只是發送警告訊息出去！
-r     ： 在將系統的服務停掉之後就重新開機(常用)
-h     ： 將系統的服務停掉後，立即關機。 (常用)
-c     ： 取消已經在進行的 shutdown 指令內容。
時間   ： 指定系統關機的時間！時間的範例底下會說明。若沒有這個項目，則預設 1 分鐘後自動進行。
範例：
[root@study ~]# /sbin/shutdown -h 10 'I will shutdown after 10 mins'
Broadcast message from root@study.centos.vbird (Tue 2015-06-02 10:51:34 CST):

I will shutdown after 10 mins
The system is going down for power-off at Tue 2015-06-02 11:01:34 CST!
```

如果你什么参数都没有加，单纯执行 shutdown 之后， 系统默认会在 1 分钟后进行'关机'的动作

示例：

```
[root@study ~]# shutdown -h now
立刻關機，其中 now 相當於時間為 0 的狀態
[root@study ~]# shutdown -h 20:25
系統在今天的 20:25 分會關機，若在21:25才下達此指令，則隔天才關機
[root@study ~]# shutdown -h +10
系統再過十分鐘後自動關機
[root@study ~]# shutdown -r now
系統立刻重新開機
[root@study ~]# shutdown -r +30 'The system will reboot' 
再過三十分鐘系統會重新開機，並顯示後面的訊息給所有在線上的使用者
[root@study ~]# shutdown -k now 'This system will reboot' 
僅發出警告信件的參數！系統並不會關機啦！嚇唬人！
```



## 6.3 重新开机，关机： reboot， halt， poweroff

还有三个指令可以进行重新开机与关机的任务，那就是reboot， halt， poweroff。 其实这三个指令呼叫的函式库都差不多，所以当你使用'man reboot'时，会同时出现三个指令的用法给你看。

一般重新开机时，都会下达如下的指令：

```
[root@study ~]# sync; sync; sync; reboot
```



```
[root@study ~]# halt      # 系統停止～螢幕可能會保留系統已經停止的訊息！
[root@study ~]# poweroff  # 系統關機，所以沒有提供額外的電力，螢幕空白！
```



## 6.4 实际使用管理工具 systemctl 关机

目前系统中所有服务的管理是使用哪个指令呢？那就是 systemctl 。这个指令相当的复杂！我们会在很后面系统管理员部份才讲的到！ 目前只要学习 systemctl 当中与关机有关的部份即可。 要注意，上面谈到的 halt， poweroff， reboot， shutdown 等等，其实都是呼叫这个 systemctl 指令。 此指令跟关机有关的语法如下：

```
[root@study ~]# systemctl [指令]
指令項目包括如下：
halt       進入系統停止的模式，螢幕可能會保留一些訊息，這與你的電源管理模式有關
poweroff   進入系統關機模式，直接關機沒有提供電力喔！
reboot     直接重新開機
suspend    進入休眠模式

[root@study ~]# systemctl reboot    # 系統重新開機
[root@study ~]# systemctl poweroff  # 系統關機
```



# 7 课后题

## 7.1 情境模拟题

我们在纯文字界面，例如tty2里面看到的欢迎画面，就是在那个login：之前的画面（CentOS Linux 7 ...） 是怎么来的？

- 目标：了解到终端机接口的欢迎讯息是怎么来的？
- 前提：欢迎讯息的内容，是记录到/etc/issue当中的
- 需求：利用man找到该档案当中的变量内容



**解决步骤:**

1. 欢迎画面是在/etc/issue档案中，你可以使用'**nano /etc/issue**』看看该档案的内容（注意，不要修改这个档案内容，看完就离开），这个档案的内容有点像底下这样：

   ```
   \S
   Kernel \r on an \m
   ```

2. 与tty3比较之下，发现到核心版本使用的是 \r 而硬件等级则是 \m 来取代，这两者代表的意义为何？ 由于这个文件的文件名是issue，所以我们使用'**man issue**'来查阅这个文件的格式;

   

3. 透过上一步的查询我们会知道反斜线（\）后面接的字符是与agetty（8）及mingetty（8）有关，故进行'**man agetty**'这个指令的查询。

   

4. 由于反斜线（\）的英文为'escape'因此在上个步骤的man环境中，你可以使用'**/escape**'来搜寻各反斜线后面所接字符所代表的意义为何。

   

5. 请自行找出：如果我想要在/etc/issue档案内表示'时间（localtime）'与'tty号码（如tty1， tty2的号码）'的话， 应该要找到那个字符来表示（透过反斜线的功能）？（答案为：\t 与 \l）



## 7.2 简答题

1. 简单的查询一下，Physical console / Virtual console / Terminal 的说明为何？

> console 有'控制台'的意思在里面，因此你可以这样看的：
>
> - 实体控制台：实体的屏幕、键盘、鼠标等界面，让你可以使用该配备来操作系统的环境，就称为实体控制台 （Physical console）
> - 虚拟控制台：由系统衍生出的虚拟控制台，你可以透过该虚拟控制台搭配你自己系统的实体配备，来操作远程系统的环境。 每个虚拟控制台都是独立运作的。
> - 终端机：你可以用该界面来取得一个可以控制系统的 shell 环境。
>
> 由这些定义来看，一般来说，我们取得可以与系统互动的环境，大致上都称为 terminal 就是了。



2. 请问如果我以文字模式登录Linux主机时，我有几个终端机界面可以使用？如何切换各个不同的终端机接口？

> 共有六个， tty1 ~ tty6 ，切换的方式为 Ctrl + Alt + [F1]~[F6]



3. 在Linux系统中，/VBird与/vbird是否为相同的档案？

> 两者为不同的档案，因为 Linux 系统中，大小写字母代表意义不一样！



4. 我想要知道 date 如何使用，应该如何查询？

> 最简单的方式就是使用 man date 或 info date 来查看，如果该套件有完整说明的话，那么应该也可以在 /usr/share/doc 里面找到说明文件！



5. 我想要在今天的 1：30 让系统自己关机，要怎么做？

```
shutdown -h 1:30
```



6. 如果我 Linux 的 X Window 突然发生问题而挂掉，但 Linux 本身还是好好的，那么我可以按下哪三个按键来让 X window 重新启动？

```
[ctrl]+[alt]+[backspace]
```



7. 我想要知道 2010 年 5 月 2 日是星期几？该怎么做？

> 最简单的方式直接使用 cal 5 2010 即可找出 2010 年 5 月份的月历。



8. 使用 man date 然后找出显示目前的日期与时间的参数，成为类似：2015/10/16-20：03

```
date +%Y/%m/%d-%H:%M
```



9. 若以 X-Window 为预设的登入方式，那请问如何进入 Virtual console 呢？

> 可以按下 [Ctrl] + [Alt] + [F2] ~ [F6] 进入 Virtual console （ 共六个 ）; 而按下 [Ctrl] + [Alt] + [F1] 可回到 X-Window 的 desktop 中！



10. 简单说明在 bash shell 的环境下， [tab] 按键的用途？

> [Tab] 按键可作为命令补齐或文件补齐的功能，与所接的指令位置有关。 接在一串指令的第一个单词后面，则为命令补齐，否则则为档案补齐！ 目前尚有选项/参数补齐的功能。



11. 如何强制中断一个程序的进行？（利用按键，非利用 kill 命令）

> 可以利用 [Ctrl] + c 来中断！



12. Linux 提供相当多的在线查询，称为 man page，请问，我如何知道系统上有多少关于 passwd 的说明？又，可以使用其他的程序来取代 man 的这个功能吗？

> 可以利用 man -f passwd 来查询，另外，如果有提供 info 的文件数据时 （在 /usr/share/info/ 目录中） ，则能够利用 info passwd 来查询之！



13. 在 man 的时候， man page 显示的内容中，指令（或文件）后面会接一组数字，这个数字若为 1， 5， 8，表示该查询的指令（或文件）意义为何？

> 代表意义为 1） 一般用户可以使用的指令或可执行文件 5）一些配置文件的文件内容格式 8）系统管理员能够使用的管理指令。



14. man page 显示的内容的文件是放置在哪些目录中？

> 放置在 /usr/share/man/ 与 /usr/local/man 等默认目录中。



15. 请问这一串指令' foo1 -foo2 foo3 foo4 '中，各代表什么意义？

> foo1 一定是指令， -foo2 则是 foo1 这个指令的选择项目参数， foo3 与 foo4 则不一定， 可能是 foo1 的参数设置，也可能是额外加入的 parameters。



16. 当我输入man date时，在我的终端机却出现一些乱码，请问可能的原因为何？如何修正？

> 如果没有其他错误的发生，那么发生乱码可能是因为语系的问题所致。 可以利用 export LANG=en_US.utf8 或者是 export LC_ALL=en_US.utf8 等设定来修订这个问题。



17. 我输入这个指令『ls -al /vbird』，系统回复我这个结果：『ls： /vbird： No such file or directory』 请问发生了什么事？』

> 不要紧张，很简单的英文，因为系统根本没有 /vbird 这个文件的存在啊！ ^_^



18. 我想知道目前系统有多少指令是以 bz 为开头的，可以怎么作？

> 直接输入 bz\[tab][tab] 就可以知道了！



19. 承上题，在出现的许多指令中，请问 bzip2 是干嘛用的？

> 在使用man bzip2 之后，可以发现到，其实 bzip2 是用来作为压缩与解压缩档案用的！



20. 在终端机里面登入后，看到的提示字符 $ 与 # 有何不同？平时操作应该使用哪一个？

> \# 代表以 root 的身份登录系统，而 $ 则代表一般身份用户。 依据提示字符的不同， 我们可以约略判断登入者身份。 一般来说，建议日常操作使用一般身份用户登入，亦即是 $ ！



21. 我使用dmtsai这个账号登入系统了，请问我能不能使用reboot来重新开机？ 若不能，请说明原因，若可以，请说明指令如何下达？

> 理论上reboot仅能让root执行。 不过，如果dmtsai是在主机前面以图形界面登入时，则dmtsai还是可以透过图形介面功能来关机。