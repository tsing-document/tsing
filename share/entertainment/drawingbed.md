#### 制作免费图床
![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/tsing/制作免费图床.png)

### 目录
#### 1.1 概述
#### 1.2 生成GitHub中的token
#### 1.3 介绍PicGo
#### 1.4 安装PicGo
#### 1.5 配置PicGo
#### 1.6 测试
---

#### 1.1 概述
在编写各种文章的时候，我们需要插入各种图片，这个时候如果有一个能统一管理我们图片的网站该有多好啊。经过百度之后发现了一个比较不错的方式，下面分享给大家，教程中需要的工具的下载连接我会放在文章的结束出。本文章将使用`PicGo、GitHub`结合制作图床。

#### 1.2 生成GitHub中的token
先注册[GitHub](https://github.com/)账号，然后在主页点击用户头像，选择【Settings】-【Developer settings】-【Personal access tokens】-【Generate new token】，填写好描述【Note】，勾选【repo】，然后点击【Generate token】生成一个Token，注意这个Token只会显示一次，先保存至记事本。
![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9saWhhbzE5OTEuZ2l0ZWUuaW8vaW1hZ2VzLWJlZC9pbWcvMjAxOTExMjMxNDU4MjMucG5n?x-oss-process=image/format.png)

#### 1.3 介绍PicGo
PicGo是一个用于快速上传图片并获取Url链接的工具。它现在支持的图床平台有：七牛、腾讯云、又拍云、GitHub、SM.MS、阿里云OSS、Imgur。你可以自行开发第三方图床插件。

#### 1.4 安装PicGo
下载链接在文章的最后，安装就是傻瓜式安装方式。

#### 1.5 配置PicGo
选择【图床设置】-【GitHub图床】
![](https://static01.imgkr.com/temp/82536da9c2ce4ab1a66ec141a3e1aaef.png)
- 设定仓库名：用户名/仓库名
- 设定分支名：刚开始创建的都是master
- 设定token: 在`1.2`步骤中保存的值
- 指定存储路径：这个会在仓库中生成目录
- 自定义域名：https://cdn.jsdelivr.net/gh/用户名/仓库名

#### 1.6 测试
上传一张图片到`GitHub`上，上传成功会提示，上传成功。然后到你创建的`GitHub`仓库上会发现有一张图片已经存在了。

### 工具下载链接
[点我PicGo下载](https://github.com/Molunerfinn/PicGo/releases)
