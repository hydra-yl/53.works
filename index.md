---
layout: default
title: "53.works"
---

# 初衷
GitHub，作为开源代码库以及版本控制系统，拥有千万的开发者用户。

然而国内开发者却面对这样的窘境，想要clone一个代码仓库到本地，“git clone git@github.com.xxxx”，下载速度10kB/s，100MB的文件，需要下载10000s，2.7小时。

由于在国内访问GitHub速度很慢，从GitHub clone代码成为一个耗时巨长的工程。

解决方案有很多种，例如[通过GlobalSSH加速github推拉速度](https://mozz.in/github/2020/08/16/ucloud-globalssh.html)。

但还可以更简单。

# 加速效果

测试数据如下，加速前后速度提升了436倍，433MB的文件，原本需要16653s传输完成，加速后仅需要38s即可完成。

#### 加速前

![](/images/01.png)

#### 加速后

![](/images/02.png)


# 原理

#### 现象

主机上无需做额外配置，执行dig github.com时，你会发现解析出一个内网IP地址，这是专门为访问GitHub的加速地址。

![](/images/03.png)

clone代码时有两种方法，HTTPS和SSH。TSL/SSL加密在客户端和GitHub服务器之间进行，每个连接会生成唯一的加密密钥，且传输的内容是经过完整性校验，客户端会对服务端的主机名和证书进行有效性验证。SSH使用公私钥对进行认证和加密传输，客户端到GitHub服务端的连接是基于非对称加密，实现端到>端的加密传输。


# 写在最后

该项目的发起，起源于我们自己真实的clone代码时的崩溃，于是通过技术来解决这一问题。

`time git clone https://github.com/dgraph-io/dgraph.git`

![](/images/04.png)

更多的优化和功能我们在不断探索中，更多的想法可以在git中提issue进行交流。
