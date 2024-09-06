---
title: Charles from 0 to 1, A Beginner's Guide
date: 2024-07-28 00:00:00
lang: zh
duration: 12min
description: A Beginner's Guide to Charles.
---

[[toc]]

### 写在前面

最近内购了公司电脑，换了台新的mac，在重新配置环境的过程中，突然意识到在当前公司已经呆了快 3 年了。于是想着对过去这三年做一些总结，包括日常用到的一些工具、框架的学习，以及工作业务上、业务推进上的一些思考。

本篇是 charles 的安装、使用教程（入门级），记录的原因是重新安装这个工具，发现有些点还是容易踩坑的，同时有些功能特性很有用，但是很多人不知道怎么用。

### 简介

Charles 是一个非常知名的代理、抓包工具，它集成了非常多好用的功能，接下来我将基于 macos 版本来带领你从 0 - 1 入门该工具。

Charles 官网：<https://www.charlesproxy.com/>

### 安装

官网下载地址：<https://www.charlesproxy.com/download/>

当然你可以网上找一些破解版。

### 初始化配置

#### SSL 代理、抓包设置

1.  点击打开 Proxy - SSL Proxying Settings...

![](/images/Charles-from-0-to-1-01.png)

1.  配置可代理、抓包的白名单列表，\*号代表所有域名和端口

![](/images/Charles-from-0-to-1-02.png)

3.  点击 Proxy - Proxy Settings...

![](/images/Charles-from-0-to-1-03.png)

4.  设置代理、抓包时 charles 所用的端口号

![](/images/Charles-from-0-to-1-04.png)

#### PC证书安装

1.  点击打开 Help - SSL Proxying

![](/images/Charles-from-0-to-1-05.png)

2.  点击 install Charles Root Certificate

![](/images/Charles-from-0-to-1-06.png)

3.  弹出 “添加证书” 弹框，钥匙串选择 “登录”，并点击 “添加”【我的证书已经添加，没有这类弹框弹出，就不贴截图了】
4.  已添加的证书，展开 “信任” ，并对其中的所有子项选择始终信任

![](/images/Charles-from-0-to-1-07.png)

#### 移动端证书安装

1.  点击 install Charles Root Certificate on a Mobile Device or Remote Browser

![](/images/Charles-from-0-to-1-08.png)

2.  手机 wifi 与电脑保持同一局域网，设置代理 ip（图片中的172.23.28.20，即电脑的本地局域网ip） 和 端口（8888），并在浏览器中访问打开 chls.pro/ssl ，下载证书文件

![](/images/Charles-from-0-to-1-09.png)

3.  安装证书（不同机型会有不同，以下以小米11和 iphone11 pro 为例）

    - 安卓：

      - 设置 - 安全 - 更多安全设置 - 加密与凭据 - 安装证书 - CA证书
      - 选择证书文件安装
      - 设置 - 安全 - 更多安全设置 - 加密与凭据 - 信任的凭据，点击刚安装的证书，并进行 “信任操作”

    - iOS：

      - 设置 - 顶部的 “描述文件” ，点击描述文件进行安装
      - 设置 - 通用 - 描述文件与设备管理，选择刚安装的证书，并切换到 “信任”

### 抓包

#### PC端本地应用抓包

Proxy - macOS Proxy 点击勾选即可。

![](/images/Charles-from-0-to-1-10.png)

#### 移动端应用抓包

wifi 配置好 proxy ip 和端口后，charles会弹框提示如下：

![](/images/Charles-from-0-to-1-11.png)

点击 Allow 即可。

如果不小心点击了 Deny 怎么办呢？charles 重启一下即可。

而如果想要一次性设置多个 ip 可 通过 charles 进行代理/抓包，则可以进行以下的操作：

- 点击 Proxy - Access Control Settings...

![](/images/Charles-from-0-to-1-12.png)

- 在弹框列表中添加你想要加白的ip地址

![](/images/Charles-from-0-to-1-13.png)

### 代理

针对非 h5 网页的代理，你可以使用 map remote 或 map local 。针对 h5 网页的代理，可以尝试使用这两种方式，但我过来人的经验，没有成功过，最终用的是 path rewrite 。

#### map remote

如果你想要将某个接口代理到另一个接口，或者将某个域名代理到另一个域名，你可以使用 map remote ，设置入口如下：

![](/images/Charles-from-0-to-1-14.png)

并在弹框中设置类似如下的配置：

![](/images/Charles-from-0-to-1-15.png)

另外，一般常用的代理场景主要有以下几种：

- 域名代理：

  - from: <https://online.server.com>
  - to: <https://dev.server.com>

- 路径代理：

  - from: <https://online.server.com/list>
  - to: <https://dev.server.com/list-dev>

- 模糊匹配代理到准确路径：

  - form: `https://online.server.com/*/pages/*`
  - to: `https://online.server.com/1.0.0/pages/`

#### map local

如果你想要将某个接口的 response 代理到本地的 mock 数据，你可以使用 map local 。

和 map remote 类似，入口如下：

![](/images/Charles-from-0-to-1-16.png)

弹框中配置如下：

![](/images/Charles-from-0-to-1-17.png)

#### path rewrite

如果你使用上面两种方式都不能代理成功，那你当前的应用可能是 H5 ，其设置入口如下：

![](/images/Charles-from-0-to-1-18.png)

弹框中进行以下操作：

![](/images/Charles-from-0-to-1-19.png)

接下来设置 rewrite 的数据：

![](/images/Charles-from-0-to-1-19.png)

上面只是列举的是接口 rewrite 的 case ，当然也是可以 rewrite html 字符串。

### 总结

以上是 Charles 的一些基础用法，能够满足绝大部份同学的需求，其他更高阶的用法，请移步 <https://www.charlesproxy.com/documentation/welcome/> 官方文档查阅。
