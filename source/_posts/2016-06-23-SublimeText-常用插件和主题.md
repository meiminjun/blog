title: 史上最强Sublime 笔记系列---精选插件和UI主题
date: 2016-06-23 21:57:13
categories:
  - 工具
tags:
  - 工具
  - sublime
---

![](http://ww1.sinaimg.cn/large/69a9ed59gw1f56cg7zmfvj20hm08kdhc.jpg)

这篇文章主要讲的是Sublime Text 3一些`高效率的插件`和`漂亮的主题`。

1. ** [史上最强Sublime 笔记系列---常用快捷键](/2016/06/24/SublimeText-常用快捷键/)(持续更新中。。。) **

2. ** [史上最强Sublime 笔记系列---精选插件和UI主题](/2016/06/23/SublimeText-常用插件和主题/)(持续更新中。。。) **

3. ** [史上最强Sublime 笔记系列---我的常用配置](/2016/06/22/SublimeText-我的常用配置/)(持续更新中。。。)  **

<!-- more -->

***

# 安装package control插件(安装之后才能安装其他插件)

``` bash

import urllib.request,os; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ','%20')).read())

```

打开sublime text 3，按 ctrl+~或者菜单 View > Show Console打开命令窗口，粘贴以上代码并回车即可。

然后，**ctrl + shift + p**  下载相关插件
![](http://ww3.sinaimg.cn/large/69a9ed59gw1f568lvwdzug20b606o40a.gif)


# 推荐插件(基本上都是插件官网前100名以内的插件)

## 1. JsFormat (javascript代码格式化)

> ** 默认快捷键：ctrl + shift + f **

## 2. Terminal (快速打开cmd)

### 由于默认快捷键 `ctrl + shift + t ` 会发生冲突,替换为：ctrl + shift + c

添加快捷键，如下:

```
{
    "keys": ["alt+m"],
    "command": "markdown_preview",
    "args": {"target": "browser", "parser":"markdown"}
}

```



## 3. [docblockr](https://packagecontrol.io/packages/DocBlockr)(代码注释)

![docblockr](/images/blogImg/2016/06/2016-06-22-01.gif)
![docblockr](/images/blogImg/2016/06/2016-06-22-02.gif)
![docblockr](/images/blogImg/2016/06/2016-06-22-03.gif)
![docblockr](/images/blogImg/2016/06/2016-06-22-04.gif)

## 4. [SublimeTmpl](https://packagecontrol.io/packages/SublimeTmpl)(快速构建模板)

> ** 默认快捷键：**   
> * **ctrl+alt+h 生成html ** 
> * **ctrl+alt+j 生成javascript **
> * **ctrl+alt+c 生成css **
> * **ctrl+alt+p 生成php **
> * **ctrl+alt+r 生成ruby **
> * **ctrl+alt+shift+p 生成python **

中文文档地址:**http://www.fantxi.com/blog/archives/sublime-template-engine-sublimetmpl/**

### 由于`ctrl + alt + p` 会发生冲突,暂时禁止

配置如下(首选项>插件设置>SublimeTmpl>Settings-User):

``` bash 
{
    "disable_keymap_actions": "php", // "all"; "html,css"
    "date_format" : "%Y-%m-%d %H:%M:%S",
    "attr": {
        "author": "Meiminjun",
        "email": "251222845@qq.com",
        "link": "http://example.org"
    }
}

```

### ctrl + alt + j 有可能会发生失效,所以我就切换成另外的快捷键

添加配置如下(首选项>插件配置>SublimeTmpl>Key Bindings-User):

``` bash

{
    "keys": ["ctrl+alt+s"],
    "command": "sublime_tmpl",
    "args": {"type": "js"}
  }

```

## 5. [BracketHighlighter](https://packagecontrol.io/packages/BracketHighlighter)(语法高亮)

![图片](/images/blogImg/2016/06/2016-06-22-05.png)

## 6. [Markdown Preview](https://packagecontrol.io/packages/Markdown%20Preview)(Markdown 预览)

添加快捷键配置：

```
{
    "keys": ["alt+m"],
    "command": "markdown_preview",
    "args": {"target": "browser", "parser":"markdown"}
}

```


## 我的快捷键配置汇总:(首选项>按键绑定-用户):

``` bash

[
  { "keys": ["ctrl+shift+c"], "command": "open_terminal" },
  { "keys": ["ctrl+shift+alt+c"], "command": "open_terminal_project_folder" },
  {
    "keys": ["ctrl+alt+s"],
    "command": "sublime_tmpl",
    "args": {"type": "js"}
  },
  {
    "keys": ["alt+m"],
    "command": "markdown_preview",
    "args": {"target": "browser", "parser":"markdown"}
  }
]

```
