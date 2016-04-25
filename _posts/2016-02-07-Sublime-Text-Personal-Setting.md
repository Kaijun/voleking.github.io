---
layout:     post
title:      "Sublime Text 个人配置"
date:       2016-02-07
author:     "Voleking"
header-img: "/img/post-sublimetext.jpg"
tags:
    -  Sublime Text
    -  文本编辑器
---



# 前言  

作为本人第一款上手的文本编辑器（目前也是唯一一个😅），Sublime Text 满足了我对于文本编辑器的大部分期望：精简、迅速、**跨品台**、插件丰富、**高度可定制化**。唯一的遗憾大概是从前年起开发者就一直放羊，最后一次更新还是去年三月。希望是在憋大招，又或者以后能开源。  

个人觉得新手用 IDE 可以使其专注于语言本身，但像我这样有一定基础的又不满足于使用臃肿 IDE 来单文件编程。学习曲线低，容易上手（当时不选 Vim 其实是因为颜值太低🙈）的 Sublime Text 便成了我的选择。从最开始连 C 都不知如何编译输入到现在可以简单定制，博客笔记都在上面写。Sublime Text 让我卸了 MacDown，以后还有望卸了 Evernote(已卸)。

这几天又配置了一遍（仅仅是因为一个小问题不爽卸了😢）网上介绍 Sublime text 文章千千万，不如自己写一遍。声明这篇文章是写给我的自己的，十分简略，环境是 Mac，当然如果能给你带来帮助我也是很开心的。



# Install  

[Sublime Text 2](http://www.sublimetext.com/2)  
[Sublime Text 3 beta](http://www.sublimetext.com/3)（Recommend）



# Build System  

最开始用 sublime text 就是打算用来编译 c 与 cpp 的，结果控制台不能输入，即程序无法从 stdin 读入用户输入。着实郁闷了好久，再加上暑假时对 shell 和 Jason 都一窍不通（现在还是orz），搜索许久才在知乎上找到勉强满意的方案。后来一次无意谷歌到孙耀珠的博客，终于在他的帮助下把 c, cpp, html, md, py, java 的 build system 都弄好了，感激不尽。

解决方案：

### C / C++
我们可以点击 Tools > Build System > New Build System... 新建自己的配置文件 G++.sublime-build，填入以下内容：  

```
{
    "shell_cmd": "g++ -o \"${file_path}/${file_base_name}.out\" \"${file}\"",
    "file_regex": "^(..[^:]*):([0-9]+):?([0-9]+)?:? (.*)$",
    "working_dir": "${file_path}",
    "selector": "source.c++",

    "variants":
    [
        {
            "name": "Run",
            "shell_cmd": "g++ -o \"${file_path}/${file_base_name}.out\" \"${file}\" && open \"${file_path}/${file_base_name}.out\""
        }
    ]
}
```

实际上这就是一个 JSON，相关资料可以参阅 Sublime Text Unofficial Documentation。相应地，C 的配置文件可以新建一个 C.sublime-build，将原先所有的 g++ 替换为 gcc 即可。 
注：加 ".out" 是为了在 SideBar 忽略可执行文件，无后缀名实在不知道怎么表示。


### Python
安装 SublimeREPL 即可，快捷键设置见后文。


### HTML
仿照 C / C++ 的方法自定义  Build System：  

```
{
    "shell_cmd": "open -a Safari.app \"${file}\"",
    "working_dir": "${file_path}",
    "selector": "source.html",
    "variants":
    [
        {
            "name": "Run",
            "shell_cmd": "open -a \"/Applications/Google Chrome.app\" \"${file}\""
        }
    ]
}
```

按下 ⌘B 和 ⇧⌘B 会分别在 Safari 和 Chrome 中打开当前 HTML，这样便可以快捷地预览设计中的页面。

>Updated on April 25，2016

build system 时 html 选 automatic 按 command + B 不行，必须选 html。而 c/c++ 则可以。
大概是需要创建一个新的 .tmLanguage 文件，关联 .html / .htm 扩展名，再在 HTML.sublime-build 指定刚才创建好的 scopeName，比如 "selector": "source.html"。
可以参考[这里](http://stackoverflow.com/questions/14136024/sublime-text-2-build-system-custom-selector)，暂时懒得研究( ・ˍ・)。

### Markdown
同样安装 package ，具体见 Package 部分以及快捷键设置。


### Java 
类似，但 Terminal 不会弹出，不算完美，待研究。



# Reference 

关于 Sublime Text 参考资料觉得看下面这个就基本上够了，跟着过一遍  
[Sublime Text Unofficial Documentation](https://docs.sublimetext.info/en/latest/index.html)    
如果英文不好或者想看快点  
[Sublime Text 非官方文档（中文版）](http://sublime-text.readthedocs.org/en/latest/customization/customization.html)
  


# Package  
适当的 Package 可以让 Sublime Text 更强大更高效：

+ [Package Control](https://packagecontrol.io)：必装神器，package 的包管理器  
+ Alignment：代码自动对齐  
+ ConvertToUTF8：自动转换各种非UTF8格式（GBK兼容）  
+ Codecs33：为了让ConvertToUTF8更好的工作  
+ [Emmet](http://docs.emmet.io)：原名 Zen Coding ，还没学前端～  
+ Evernote：用 Sublime Text 在 Evernote 上记笔记，要先授权。
+ Git：集成 git 常用功能。 
+ Github Tools：待研究。  
+ MarkdownEditing：在 Sublime 中编辑 MarkDown 文件，并自动使用 Color Theme  
+ OmniMarkupPreviwer：在浏览器中即时预览 MarkDown 文件效果  
+ SideBarEnhancements：增强 SideBar 功能
+ Sublime Input：另一种解决控制台无法 Input 的方法
+ [SublimeLinter](https://github.com/SublimeLinter/SublimeLinter-for-ST2/blob/sublime-text-3/README.md)：代码校验插件，找出错误或编写不规范的代码，尚未配置
+ SublimeREPL：目前编译 python，调用 ipython 用
+ Table Editor：编辑 md 更加方便加入表格
+ Terminal：在当前目录打开 Terminal
+ Theme - Spacegray：好看的主题！！！
+ Material Theme：更丰富的主题！！！ 
+ WakaTime：记录 Coding 时间，装13用。需网上注册找到 API 输入

刚使用 Sublime Text 各处找看起来狂拽酷炫吊炸天的 Package，最后都不会用或是没用。几次重新配置后断舍离了一番，只留下了一些要用或是符合我学习期望的。另外神器（Package Control）在手，要用再装嘛



# Personalization

图标换了这个：
<center>
        <img src="http://7xqllw.com1.z0.glb.clouddn.com/Sublime%20Text.png" title="Logo" width="100" />
</center>

目前使用 Theme - Spacegray（比那什么最受欢迎的 Soda Theme 好看多了，不爽咬我呀，口亨），配色不甚满意，字体未换。效果如下：

<figure>
        <img src="http://7xqllw.com1.z0.glb.clouddn.com/post-sublime-text.jpg">
</figure> 

>Updated on April 25，2016

上周换了新的功能更加丰富的 [Material Theme](http://equinusocio.github.io/material-theme/) (图片加载不出来的话可能是被 q 了，最近访问 Github 也越来越慢了)

<figure>
        <img src="https://camo.githubusercontent.com/1ff3f31c6a43cdf5f02e2d54a5afee6802abff23/687474703a2f2f657175696e75736f63696f2e6769746875622e696f2f6d6174657269616c2d7468656d652f6173736574732f6d756c74692e6a7067">
</figure> 

<figure class="half">
        <img src="https://camo.githubusercontent.com/6e29c4974bd477a61274666886fcbd8ae2775024/687474703a2f2f692e696d6775722e636f6d2f4c566852396a712e706e67">
</figure>

# Key Bindings
```
[
    //编译 *.py 
    {
        "keys": ["f5"],
        "caption": "SublimeREPL: Python - RUN current file",
        "command": "run_existing_window_command",
        "args": {
            "id": "repl_python_run",
            "file": "config/Python/Main.sublime-menu"
        }
    },
    //自动对齐
    {
        "keys":["ctrl+alt+a"],
        "command":"alignment"

    },
    //md 即时预览
    {
        "keys": ["super+b"], "command": "omni_markup_preview",
        "context": [{"key": "omnimarkup_is_enabled", "operator": "equal", "operand": ""}]
    },
    {
        "keys": ["super+alt+x"], "command": "omni_markup_export",
        "context": [{"key": "omnimarkup_is_enabled", "operator": "equal", "operand": ""}]
    },
    {
        "keys": ["ctrl+alt+c"], "command": "omni_markup_export",
        "args": { "clipboard_only": true },
        "context": [{"key": "omnimarkup_is_enabled", "operator": "equal", "operand": ""}]
    }
]

```



#  未完待续

虽然有些方案很麻烦，但用弄好了还是很爽的，对于我来说折腾也是一种乐趣。什么时候 Sublime Text 用顺了就是尝试 Vim 和 Emacs 的时候了。


# 参考文档

1. [Sublime Text for Mac 使用配置](http://blog.yzyzsun.me/sublime-text-for-mac/)  
