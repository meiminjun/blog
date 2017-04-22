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

1. ** [史上最强Sublime 笔记系列---常用快捷键](/SublimeText-常用快捷键/)(持续更新中。。。) **

2. ** [史上最强Sublime 笔记系列---精选插件和UI主题](/SublimeText-常用插件和主题/)(持续更新中。。。) **

3. ** [史上最强Sublime 笔记系列---我的常用配置](/SublimeText-我的常用配置/)(持续更新中。。。)  **

4. ** [史上最强Sublime 笔记系列---vim常用命令](/SublimeText-vim常用命令笔记/)(持续更新中。。。)  **

**各位小伙伴们，还有没有你心目中`酷炫时尚`的插件呢？有的请留言哦！谢谢。。O(∩_∩)O**

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

## [sublimeLinter-jshint]:语法校验

* 需先安装SublimeLinter
* 安装Node.js 
* 在cmd中输入 npm install -g jshint,等待安装就好了

安装成功后，重启就可以检测代码风格了

当然还可以自定义校验规则，在项目目录下新建一个.jshintrc的配置文件
在其中使用JSON格式配置校验风格。

例如：
```
//建议使用===，不使用时会有提示。
{
  "eqeqeq":true
}
```

## [sublimeLinter-elint](https://github.com/roadhump/SublimeLinter-eslint)

让sublime-text 支持es6和react

详细说明：http://cheng.logdown.com/posts/2015/09/15/linting-react-jsx-and-es6-javascript-with-eslint

## [HTML-CSS-JS Prettify](https://packagecontrol.io/packages/HTML-CSS-JS%20Prettify)(代码格式化插件)

HTML-CSSS-JS Prettify插件使用的是node版的js-beautify，因此需要首先安装node，node的安装请自行搜索。
在node安装完成后，使用npm安装js-beautify，命令 npm install -g js-beautify
最后Ctrl+Shift+P输入Install Package，然后输入HTML-CSS-JS Prettify进行安装

### HTML-CSS-JS Prettify配置
HTML-CSS-JS Prettify配置可使用.jsbeautifyrc文件，js-beautify会在被优化代码文件的当前目录查找，如果找不到会向上级目录查找。
因此，可以在项目的根目录新建.jsbeautifyrc文件来配置js-beautify
贴一下我的配置：
``` bash
{
  // Details: https://github.com/victorporof/Sublime-HTMLPrettify#using-your-own-jsbeautifyrc-options
  // Documentation: https://github.com/einars/js-beautify/
  "html": {
    "allowed_file_extensions": ["htm", "html", "xhtml", "shtml", "xml", "svg","aspx","jsp"],
    "brace_style": "collapse", // [collapse|expand|end-expand|none] Put braces on the same line as control statements (default), or put braces on own line (Allman / ANSI style), or just put end braces on own line, or attempt to keep them where they are
    "end_with_newline": false, // End output with newline
    "indent_char": " ", // Indentation character
    "indent_handlebars": false, // e.g. {{#foo}}, {{/foo}}
    "indent_inner_html": false, // Indent <head> and <body> sections
    "indent_scripts": "keep", // [keep|separate|normal]
    "indent_size": 2, // Indentation size
    "max_preserve_newlines": 0, // Maximum number of line breaks to be preserved in one chunk (0 disables)
    "preserve_newlines": true, // Whether existing line breaks before elements should be preserved (only works before elements, not inside tags or for text)
    "unformatted": ["a", "span", "img", "code", "pre", "sub", "sup", "em", "strong", "b", "i", "u", "strike", "big", "small", "pre", "h1", "h2", "h3", "h4", "h5", "h6"], // List of tags that should not be reformatted
    "wrap_line_length": 0 // Lines should wrap at next opportunity after this number of characters (0 disables)
  },
  "css": {
    "allowed_file_extensions": ["css", "scss", "sass", "less"],
    "end_with_newline": false, // End output with newline
    "indent_char": " ", // Indentation character
    "indent_size": 2, // Indentation size
    "newline_between_rules": true, // Add a new line after every css rule
    "selector_separator": " ",
    "selector_separator_newline": false // Separate selectors with newline or not (e.g. "a,\nbr" or "a, br")
  },
  "js": {
    "allowed_file_extensions": ["js", "json", "jshintrc", "jsbeautifyrc", "csslintrc"],
    "brace_style": "collapse", // [collapse|expand|end-expand|none] Put braces on the same line as control statements (default), or put braces on own line (Allman / ANSI style), or just put end braces on own line, or attempt to keep them where they are
    "break_chained_methods": false, // Break chained method calls across subsequent lines
    "e4x": false, // Pass E4X xml literals through untouched
    "end_with_newline": false, // End output with newline
    "indent_char": " ", // Indentation character
    "indent_level": 0, // Initial indentation level
    "indent_size": 2, // Indentation size
    "indent_with_tabs": false, // Indent with tabs, overrides `indent_size` and `indent_char`
    "jslint_happy": false, // If true, then jslint-stricter mode is enforced
    "keep_array_indentation": false, // Preserve array indentation
    "keep_function_indentation": false, // Preserve function indentation
    "max_preserve_newlines": 0, // Maximum number of line breaks to be preserved in one chunk (0 disables)
    "preserve_newlines": true, // Whether existing line breaks should be preserved
    "space_after_anon_function": false, // Should the space before an anonymous function's parens be added, "function()" vs "function ()"
    "space_before_conditional": true, // Should the space before conditional statement be added, "if(true)" vs "if (true)"
    "space_in_empty_paren": false, // Add padding spaces within empty paren, "f()" vs "f( )"
    "space_in_paren": false, // Add padding spaces within paren, ie. f( a, b )
    "unescape_strings": false, // Should printable characters in strings encoded in \xNN notation be unescaped, "example" vs "\x65\x78\x61\x6d\x70\x6c\x65"
    "wrap_line_length": 0 // Lines should wrap at next opportunity after this number of characters (0 disables)
  }
}

```
主要的改动就是

* 修改了"html"的"allowed_file_extensions"，增加了aspx和jsp的支持
* 修改了"css"的"selector_separator_newline"，个人觉得没必要每个选择器都要占一行
* 修改了"js"的"allowed_file_extensions"，增加了.csslintrc文件的支持
* 修改了"html"、"css"、"js"的"indent_size"，我的代码缩进为2个空格

### HTML-CSS-JS Prettify使用
使用Ctrl+Shift+H，优化当前代码文件。
使用js文件测试一下，优化前
![图片](https://segmentfault.com/img/bVsDMo)

优化后
![图片](https://segmentfault.com/img/bVsDMp)

js-beautify对css的格式化，有个问题是，会在注释下面插入一行空白字符

如下图，优化前
![图片](https://segmentfault.com/img/bVsDMq)

优化后
![图片](https://segmentfault.com/img/bVsDMr)

[sublime text 3 插件：HTML-CSS-JS Prettify](http://frontenddev.org/article/sublime-does-text-three-plug-ins-html-and-css-js-prettify.html)文中给出了解决方法，大家可以参考


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
