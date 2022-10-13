> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/xiaoxianer321/article/details/124388016)

笔记神器 Markdown 之完美实现[图床](https://so.csdn.net/so/search?q=%E5%9B%BE%E5%BA%8A&spm=1001.2101.3001.7020)
===================================================================================================

1、使用 Markdown 编写笔记
==================

    使用 Markdown 编写笔记非常方便，但是想把自己的博客笔记同步到多个平台，确是非常让人头疼的问题，虽然现在大多数的平台都支持 Markdown 格式，但是每个平台的格式多多少少会有一些格式上的问题。

    比如：知乎，对表格的兼容性太差，CSDN 的 Markdown 生成的目录不够好，掘金呢对 Markdown 的支持算好一点的，但是你直接在上面写博客，会默认生成带水印的图片。

    所以如何处理 Markdown 图片，减少自己在图片处理上花费的时间显得很有必要了，这样可以帮我们节省很多时间，而且不必要把图片都保存在本地。

    我自己比较喜欢用 [Typora](https://so.csdn.net/so/search?q=Typora&spm=1001.2101.3001.7020) 写 Markdown 笔记。为什么选择 PicGo 呢? 其实在 Markdown 偏好设置中就提供了对 PicGo 的支持。

    关于 Typora 就不多介绍了。Typora 下载地址：[Typora](https://typoraio.cn/ "Typora")

    接下来就是 Typora+PicGo+[Github](https://so.csdn.net/so/search?q=Github&spm=1001.2101.3001.7020) 完美实现图床的步骤。

2、完美实现图床步骤
==========

2.1、第一步 - 下载并安装 PicGo
---------------------

GithubPicGo 项目地址：[https://github.com/Molunerfinn/PicGo](https://github.com/Molunerfinn/PicGo "https://github.com/Molunerfinn/PicGo")

下载地址：[PicGo](https://molunerfinn.com/PicGo/ "PicGo") （比较慢）

镜像下载地址：[https://github.com/Molunerfinn/picgo/releases](https://github.com/Molunerfinn/picgo/releases "https://github.com/Molunerfinn/picgo/releases")（比较快）

安装好后在图床设置区域，完美看到要填写一些信息，接下来进行第二步。

![](https://img-blog.csdnimg.cn/img_convert/6d4bf46c14bf76629caf668201af7071.png)

2.2、第二步 - 创建一个 Github 仓库
------------------------

### 2.2.1、创建 Github 仓库

    登录 Github，在右上角的 + 号点击 New repository, 填写相关信息即可。如果对 Github 不太熟悉的话，可以找我以前在 CSDN 上的文字看。

    创建好的仓库如下：

![](https://img-blog.csdnimg.cn/img_convert/ea0782002de1903daf0e24013a768deb.png)

### 2.2.2、申请私人 token(令牌)

    什么是 token？

    如果你接触过公众号开发，也许会了解一点什么是 token，如果获取和使用 token。

token 的意思是 “令牌”，是服务端生成的一串字符串，作为客户端进行请求的一个标识。

    当用户第一次登录后，服务器生成一个 token 并将此 token 返回给客户端，以后客户端只需带上这个 token 前来请求数据即可，无需再次带上用户名和密码。

    简单 token 的组成；uid(用户唯一的身份标识)、time(当前时间的时间戳)、sign（签名，token 的前几位以哈希算法压缩成的一定长度的十六进制字符串。为防止 token 泄露）

    github 在主页的头像下有个 Settings 选项，具体的地址是：[https://github.com/settings/tokens](https://github.com/settings/tokens "https://github.com/settings/tokens")

![](https://img-blog.csdnimg.cn/img_convert/73368778447b5ae297ecd72e6c6d8e9b.png)

    申请号后会生产一串加密的字符串。有了这些信息就可以开始第三步。

3、配置 PicGo 和 Typora
===================

3.1、配置 PicGo
------------

### 3.1.1、Github 图床设置

![](https://img-blog.csdnimg.cn/img_convert/320803a8bd85cf401d3af4e3004c31be.png)

    自定义域名: 我们用 jsDelivr（是一个免费、开源的加速 CDN 公共服务，比如有时候我们开发网页的时候，引入 jquery，其实就有这个东西）。

    什么是 CDN 这里简单提一下。

    为什么有时候明明自己的网速很快，但观看取看一些视频时，会慢会卡？

    影响访问速度的原因其实有很多：1）比如看韩剧、美剧这些资源不一定在国内有，这样链路比较长，速度就比较慢；2）服务器负载能力，如果一些实力不够的服务商，或者突发流量陡增的情况，就会造成拥塞，从而导致卡顿和延时。

    关于往来卡顿的问题，一位麻省理工学院应用数学教授 Berners-Lee，请研究生 **Danny C. Lewin** 和其他几位顶级研究人员一起破解这个技术难题。于是他他们开发了利用数学运算法则来处理内容的动态路由算法技术，缩短访问链路，有效地解决了这个难题。这个技术，就是 CDN（Content Delivery Network 的简称，即 “内容分发网络” 的意思）。

    后来他们还为此专门成立了公司这个公司，就是后来鼎鼎大名的 CDN 服务鼻祖——**Akamai 公司**。

    大家可能觉得，这个不就是 **“镜像服务器”** 嘛？

    其实不一样，镜像服务器是源内容服务器的完整复制。而 CDN，是部分内容的缓存，智能程度更高。确切地说，**CDN = 更智能的镜像 + 缓存 + 流量导流**。

    但是 CDN 只适用于静态的内容，**不适用动态的内容**。如果供应商和内容服务商为了**保护自身的数据私密**，不允许第三方公司 CDN 缓存他们的数据也是有可能的。

### 3.1.2、PicGo 设置

    在 PicGo 设置中，开启日志、时间戳重命名、上传后自动赋值 URL。其他的可以自己选择性的配置。

3.2、配置 Typora
-------------

    在 Typora 的偏好设置中设置：

![](https://img-blog.csdnimg.cn/img_convert/0d6aa4b6eab50a767524d7adf8c35310.png)

4、测试我们的配置
=========

![](https://img-blog.csdnimg.cn/img_convert/bebbdd8580812ec72c4a14d515504de7.gif)

在 PicGo 相册中其实也能看到我们上传成功的图片

![](https://img-blog.csdnimg.cn/img_convert/04a61fb74caee8474ca8df1784e4f2e4.png)