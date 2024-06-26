---
title: 基于PicGo与Gitee的Typora写作环境搭建之图床配置
date: 2024-04-27 14:19:29
categories:
- configure
tags: 
- MarkDown
- 环境配置
---

<meta name="referrer" content="no-referrer" />

<!-- toc -->

## 0.意义

在markdown写作时，文章引用的图片往往存放于本地，易受路径改变影响且上传blog时不方便。针对这种情况，使用图床将图片上传到网上并生成链接插入md文件显得尤其方便快捷。本文介绍使用可以快速上传图片并获取图片 URL 链接的工具**PicGo**和国内的代码托管平台**Gitee**两种工具，实现在typora中可以直接插入图片时，自动上传到Gitee并生成URL。

## 1.软件安装

### 1.1 Gitee注册

> Gitee地址：[工作台 - Gitee.com](https://gitee.com/)

注册/登陆以后选择新建仓库

<img src="https://gitee.com/tosfk/blog-pic/raw/master/202404271400303.png" alt="image-20240427140006262" style="zoom: 67%;" />

配置参数：

<img src="https://gitee.com/tosfk/blog-pic/raw/master/202404271400487.png" alt="image-20240427140058428" style="zoom: 50%;" />

创建好以后进入个人设置

<img src="https://gitee.com/tosfk/blog-pic/raw/master/202404271415276.png" style="zoom:50%;" />

选择安全设置中的私人令牌：

<img src="https://gitee.com/tosfk/blog-pic/raw/master/202404271402661.png" alt="image-20240427140226627" style="zoom:80%;" />

生成新令牌，配置参数

<img src="https://gitee.com/tosfk/blog-pic/raw/master/202404271403925.png" alt="image-20240427140302883" style="zoom: 67%;" />

令牌明文只展示一次，存储下来，准备填入PicGo



### 1.2 PicGo

> 项目地址：[Molunerfinn/PicGo: :rocket:A simple & beautiful tool for pictures uploading built by vue-cli-electron-builder (github.com)](https://github.com/Molunerfinn/PicGo)

选择合适的版本下载并安装

![image-20240427135711366](https://gitee.com/tosfk/blog-pic/raw/master/202404271357417.png)

插件设置，搜索gitee-uploader并安装

<img src="https://gitee.com/tosfk/blog-pic/raw/master/202404271406770.png" alt="image-20240427140611714" style="zoom:50%;" />

选择图床设置 -> gitee设置，填入选项

<img src="https://gitee.com/tosfk/blog-pic/raw/master/202404271409956.png" alt="image-20240427140919901" style="zoom:50%;" />

进行设置

<img src="https://gitee.com/tosfk/blog-pic/raw/master/202404271408771.png" alt="image-20240427140816710" style="zoom:50%;" />

<img src="https://gitee.com/tosfk/blog-pic/raw/master/202404271410561.png" alt="image-20240427141035496" style="zoom:50%;" />

<img src="https://gitee.com/tosfk/blog-pic/raw/master/202404271411736.png" alt="image-20240427141107678" style="zoom:50%;" />

<img src="https://gitee.com/tosfk/blog-pic/raw/master/202404271411923.png" alt="image-20240427141121870" style="zoom:50%;" />



### 1.3 Typora设置

打开文件 -> 偏好设置，按下图配置，然后验证图片上传选项，检验是否成功。

<img src="https://gitee.com/tosfk/blog-pic/raw/master/202404271414499.png" alt="image-20240427141429429" style="zoom:67%;" />



## [DLC1] hexo搭建的blog中图片不显示问题

上传到blog中，出现图片不显示问题

<img src="https://gitee.com/tosfk/blog-pic/raw/master/202404271448552.png" alt="image-20240427144849488" style="zoom:50%;" />

解决办法：在md文件头加上

```
<meta name="referrer" content="no-referrer" />
```

重新上传后问题解决

<img src="https://gitee.com/tosfk/blog-pic/raw/master/202404271450593.png" alt="image-20240427145018519" style="zoom:50%;" />



## [DLC2] hexo搭建的blog中图片不显示问题

`[toc]`仅仅在typora中可以生成目录，但是默认的hexo无法渲染目录结构，要实现hexo中目录功能，需要

首先安装插件

```
npm install hexo-toc --save
```

配置根目录下的_config.yml文件

```
toc:
  maxdepth: 3
```

然后添加目录，在需要展示目录的地方添加：

```
<!-- toc -->
```

> 注意：显示的目录只会包含代码段` < !-- toc -->`之后的内容