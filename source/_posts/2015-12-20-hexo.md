title: Hexo博客搭建
date: 2015-12-20 01:55:53
tags:
	- hexo
	- 博客
---
作为第一篇博客，我就写一些这个博客是怎么制作的吧！
![这个是个图片](/images/blogImg/hexo-github.png)
## [Hexo](https://hexo.io/)是什么?
Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。
>向这个团队表示一下感谢！感谢！感谢！    ————重要的事吼三遍

## Hexo有哪些特点？

* ### 超快速度
    > **Node.js 所带来的超快生成速度，让上百个页面在几秒内瞬间完成渲染。**

* ### 支持 Markdown
	> **Hexo 支持 GitHub Flavored Markdown 的所有功能，甚至可以整合 Octopress 的大多数插件。**

* ### 超级方便的一键部署
	> **只需一条指令即可部署到 GitHub Pages, Heroku 或其他网站。**

* ### 丰富的插件
	> **Hexo 拥有强大的插件系统，安装插件可以让 Hexo 支持 Jade, CoffeeScript。**
---

<!-- more -->

## 安装前提
* [Node.js](https://nodejs.org/)
* [Git](http://git-scm.com/downloads)

# 开始我们的安装之旅：
## 第一步-建立一个自己域名的仓库

在github上，建立与你用户名对应的仓库，仓库名必须为【your_user_name.github.io】
按以下步骤：
![](/images/blogImg/github1.png)
![](/images/blogImg/github2.png)
![](/images/blogImg/github3.png)
![](/images/blogImg/github4.png)
![](/images/blogImg/github5.png)
![](/images/blogImg/github6.png)

### 参考地址：http://blog.csdn.net/renfufei/article/details/37725057/
## 第二步(安装hexo)

``` bash
npm install hexo-cli -g 
hexo init blog
cd blog
npm install
hexo server //开启服务器，然后访问http://localhost:4000/
```

然后访问http://localhost:4000/
![](http://blog.fens.me/wp-content/uploads/2014/05/hexo-web.png)
## 第三步-安装git插件
安装hexo 的 git 插件
``` bash
npm install hexo-deployer-git --save
```
## 第四步-配置
在跟目录下,找到配置文件_config.yml
``` bash
deploy:
  type: git
  repo: https://github.com/meiminjun/meiminjun.github.io.git
  branch: master
```
Tips:
* `配置的时候“：”后面空一格，否则无法提交到github`(**重点**)
* 网上很多都是用ssh进行的，其实搞起来还是挺麻烦的，自己有兴趣的可以玩玩！

提供一下以ssh配置的方式安装的参考：

http://jingyan.baidu.com/article/d8072ac47aca0fec95cefd2d.html

http://jingyan.baidu.com/article/a65957f4e91ccf24e77f9b11.html

如果要配置主题和插件的话:
Plugins: http://hexo.io/plugins/
Themes: http://hexo.io/themes/


## 第五步-命令行(重点来了)

``` bash
hexo new "My New Post"	// 创建文章(在./source/_posts/)
hexo new post wexinSdk // 新建一个布局为post(在scaffolds中)的名字为“wexinSdk”的文章
hexo new page pageTest // 新建一个pageTest的目录
hexo publish [layout] <title>   // 新建一个草稿
hexo generate // 生成文章
hexo server // 开启服务器 
hexo deploy  // 发布到github
```

hexo支持简单命令格式,每次发布前的三个步骤：

>  * hexo g    // 生成文章
>  * hexo s    // 开启本地服务器预览(可选，方便本地预览)
>  * hexo d    // 发布到github,然后在进入到.gitignore文件夹中去手动提交到自己名字的github

Tip:
1. 如果不行进入到.gitignore文件夹中去手动提交github
2. 后面添加 -- debug 可看报错信息

参考：
http://blog.fens.me/hexo-blog-github/

http://hexo.io


## 有问题？
在使用中有任何问题，欢迎反馈给我，可以用以下联系方式跟我交流
* 邮件(251222845@qq.com, 把#换成@)
* QQ: 251222845