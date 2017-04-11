title: Vysor最新版本破解
date: 2017-03-30 22:57:13
tags:
  - chrome
  - vysor
---

## Vysor最新版本破解


Vysor是一个Chrome插件, 他 可以把android手机屏幕投影到电脑上方便操作. 操作方便个人感觉是目前最好的了.

Vysor普通版相对专业版多了一些限制, 例如无法最大化. 但是专业版要收费, 点支付宝支付这边一直卡住, 没法, 只能翻开源码研究一下.

网上说了一堆说只能破解1.6.6以前版本，于是我自己就研究了一下，截止目前来说，我正在使用的当前版本1.7.2(最新版本)也是可以破解的

首先，谷歌商店下载[最新版本](https://chrome.google.com/webstore/detail/vysor/gidgenkbbabolejbgbpnhbimgjbffefm?hl=zh-CN),并安装（谷歌商店需要翻墙）

然后在本地查找插件代码路径:

### Windows

```
C:\Users\Administrator\AppData\Local\Google\Chrome\User Data\Default\Extensions\gidgenkbbabolejbgbpnhbimgjbffefm\1.7.2_0

```

windows里面，我的用户名是 Administrator, 系统盘是C:, 按照自己情况来设置路径

### Mac OS

```
/Users/larben/Library/Application Support/Google/Chrome/Default/Extensions/gidgenkbbabolejbgbpnhbimgjbffefm/1.7.2_1
```

macos里面，我的用户名是 larben, 这里要按照自己情况来设置路径

在路径下打开 uglify.js文件, 搜索 _il变量, 将 _il:Te.a() 替换为 _il:true, 然后重启chrome和vysor. 可以发现Vysory已经变为专业版了

![](https://ww2.sinaimg.cn/large/006tNc79gy1fe4on59c4kj30rw1dejvx.jpg)

开心。。。
