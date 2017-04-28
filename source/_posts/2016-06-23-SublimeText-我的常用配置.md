title: 史上最强Sublime 笔记系列---我的常用配置
date: 2016-06-22 15:57:14
categories:
  - 工具
tags:
  - 工具
  - sublime
---

![](http://ww1.sinaimg.cn/large/69a9ed59gw1f56cg7zmfvj20hm08kdhc.jpg)

这篇文章主要讲的Sublime Text 3 的一些用户配置说明，方便使用者的个性化使用

1. ** [史上最强Sublime 笔记系列---常用快捷键](/SublimeText-常用快捷键/)(持续更新中。。。) **

2. ** [史上最强Sublime 笔记系列---精选插件和UI主题](/SublimeText-常用插件和主题/)(持续更新中。。。) **

3. ** [史上最强Sublime 笔记系列---我的常用配置](/SublimeText-我的常用配置/)(持续更新中。。。)  **

4. ** [史上最强Sublime 笔记系列---vim常用命令](/SublimeText-vim常用命令笔记/)(持续更新中。。。)  **

<!-- more -->

***

## 我的推荐字体（**非常漂亮的几款字体**）

>    * Microsoft YaHei Mono
>    * monaco
>    * Courier New
>    * comic sans ms

## 推荐UI主题配置（**非常时尚的两款UI主题**）：

### 1. Flatland（推荐）

``` bash
"color_scheme": "Packages/Theme - Flatland/Flatland Monokai.tmTheme",
"theme": "Flatland Dark.sublime-theme",
```

### 2. Material

``` bash
"theme": "Material-Theme.sublime-theme",
"color_scheme": "Packages/Material Theme/schemes/Material-Theme.tmTheme",
```

### 3. Seti

``` bash
"theme": "Seti.sublime-theme"
```

## 我的配置详情(最美纯净版)

``` bash 
{
    "default_line_ending": "unix", // 使用unix 风格
    "draw_minimap_border": true, // 用于预览添加边框
    // "font_face": "Courier New",
    // "font_face":"comic sans ms",
    "font_face":"monaco",
    "font_size": 13.0,
    "line_padding_bottom": 1,
    "line_padding_top": 1,
    "tab_size": 2,
    "highlight_modified_tabs": true,  // 高亮未保存文件
    "highlight_line": true, // 当前行高亮
    "trim_trailing_white_space_on_save": true, // 保证在文件保存时，移除每行结尾多余空格
    "update_check": false, // 禁止自动更新
    "word_wrap": "true" // 设置自动换行
    "theme": "Flatland Dark.sublime-theme",
    "color_scheme": "Packages/Theme - Flatland/Flatland Monokai.tmTheme",
}


```

## 常用配置详情说明

``` bash

trim_trailing_white_space_on_save，自动移除行尾多余空格，处女座更安心了。

ensure_newline_at_eof_on_save，文件末尾自动保留一个空行，懂的人自然知道它的用处。

font_face 设置字体。Microsoft YaHei Mono 是一款混合字体，专为代码优化，看起来很舒服。当然你也可以使用你自己喜欢的字体，或者删掉本行，使用默认字体。

disable_tab_abbreviations 设置为 true ，禁用 Emmet 的 tab 键功能（请使用 ctrl+e），系统自带的 tab 功能还是可圈可点的。当然你也可以不设置它，以完全使用 Emmet 的 tab 补全功能。

translate_tabs_to_spaces 很明白就是把代码 tab 对齐转换为空格对齐，

tab_size 配合设置空格数。这个需求因人而异了，不喜欢可以去掉。

draw_minimap_border，用于右侧代码预览时给所在区域加上边框，方便识别。

save_on_focus_lost，窗口失焦立即保存文件，嘛嘛再也不用担心你忘记保存了。

highlight_line，当前行高亮。

word_wrap，设置自动换行。

fade_fold_buttons，默认显示行号右侧的代码段闭合展开三角号。

bold_folder_labels，侧边栏文件夹显示加粗，区别于文件。

highlight_modified_tabs，高亮未保存文件。

default_line_ending: “unix”，使用 unix 风格的换行符。

auto_find_in_selection: true ，开启选中范围内搜索（而不是整个文档

translate_tabs_to_spaces :true，Tab转空格

word_separators:true , 词的分符隔定义，加入中文符号

vintage_start_in_command_mode, 启动时，开启vim命令模式

```

## sulimeText 的vim模式

sublime 默认是禁用vim模式的
> "ignored_packages": ["Vintage"]

开启vim模式要配置成：
> "ignored_packages": [""]

在用户配置中：

> "vintage_start_in_command_mode": true //启动时，开启vim命令模式

在用户快捷键中添加配置(进入vim模式)：

```
{
    "keys": ["j", "j"],
    "command": "exit_insert_mode",
    "context":
    [
        { "key": "setting.command_mode", "operand": false },
        { "key": "setting.is_widget", "operand": false }
    ]
}

```

具体参考：http://www.sublimetext.com/docs/3/vintage.html
