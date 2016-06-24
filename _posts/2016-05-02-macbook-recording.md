---
layout:     post
title:      "Mac OS 工作环境配置"
subtitle:   ""
date:       2016-05-02
author:     "Voleking"
header-img: "http://7xqllw.com1.z0.glb.clouddn.com/post-macbook.jpg"
tags:
    -  MacOS
    -  Tools
    -  Recording
---

# 写在前面 #

用了半年多的 MacBook，越来越喜欢 MacOs 了，压根不想转回 Windows 阵营，一来有非常多极度优秀的应用，二来类 Unix 系统各种捣鼓各种嗨，就是内容实在太多，着实记不下来折腾了什么，经常弄崩许久才能复原（我该用 Time Machine 的，~~只是一直懒得买移动硬盘~~），故撰此文权当记录。

# Basics Settings #

写的挺细的一篇文章，[高效 MacBook 工作环境配置](http://blog.jobbole.com/89013/)

TOC

-  将功能键( F1-F12 )设置为标准的功能键
-  设置 Trackpad（触摸板）轻触为单击
-  将 Dock 停靠在屏幕左边
-  全键盘控制模式
-  快速锁定屏幕
-  系统常用快捷键学习(绝对提升效率的事情，就是换回 win 不习惯了)

### Others ###

#### 固定桌面顺序 ####

需要在很多桌面切换的时候，顺序突然就改变了，此时的内心是崩溃的，所以我们需要固定其顺序

System Preferences → Mission Control → Automatically rearrange Spaces based on most recent use

#### 更改崩溃报告显示方式 ####

让崩溃报告在「通知中心」显示

    > defaults write com.apple.CrashReporter UseUNC 1

恢复对话框形式

    > defaults write com.apple.CrashReporter UseUNC 0

[Reference](http://www.tuicool.com/articles/qIrAFny)

#### caps lock 映射 control ####

System Preferences → Keyboard → Modified Key

#### 繁简转换 ####

[Reference](http://www.tuicool.com/articles/amyENr3)

----

基本设置主要还是看个人喜好吧，少数派「一日一技」有时还不错可以订阅一下。

# Software Recommanded #

#### Alternote ####

轻巧漂亮的第三方 Evernote 客户端。

#### Alfred ####

神器，使用参考：

- [从零开始学习 Alfred（上）：基础功能及设置](http://sspai.com/32979)
- [杀手级功能WorkFlows介绍(1)-Alfred使用手册2](http://wellsnake.com/jekyll/update/2014/08/16/001/)

然后就是找找 WorkFlows，不过最近发现很多时候 shell 都可以替代。

#### AppCleaner ####

强迫症卸载专用

#### Bartender ####

同强迫症专用，让状态栏回归清爽

#### BetterZip ####

不错的一款解压软件

#### Caffeine ####

屏幕常亮

#### calibre ####

Calibre是一款电子图书管理软件，其提供的“一站式”的电子书解决方案，可以全面满足对电子书需求，甚至可以利用它组织成属于自己的电子图书馆，它的功能更是多种多样，不仅可以用它对图书进行格式转换，归类整理电子书，还可以将文本图像材料、在线内容（RSS）加入并转换为电子书。更重要的是Calibre是免费的、开源的，拥有跨平台的设计，可在Linux， OS X和Windows操作系统中运行，堪称电子书管理神器！

#### CheatSheet ####

长按 cmd 显示当前可用快捷键

#### CleanMyMac 3 ####

偶尔清理一下，不用就 quit 了，有时 Appcleaner 无法卸载的一般用这个。

#### Clearview ####

电子书阅读软件，主要拿来看 mobi。

#### DaisyDisk ####

设计极其漂亮的磁盘文件使用情况，只是很多时候不知道什么可以删。。。

#### 鼠须管（Squirrel） ####

**开源**，快速、流畅、稳定、小巧，基于 RIME／中州韵输入法引擎，是一个跨平台的输入法框架（ Linux 下，名为 中州韵，Windows 则为 小狼毫）。该套算法支持朙月拼音、仓颉五代、五笔86、粤拼、吴语、中古全拼／三拼、国际音标输入法及 emoji 表情等几乎所有音码和形码输入法。高度可定制，就是使用比较 Geek ，当然可以照办别人配置，讲真，国内百度搜狗输入法根本不放心，更别说都不知道究竟是不是在做输入法。

+ Reference
    * 介绍[鼠须管，“神级”输入法](http://www.ifanr.com/156409)
    * 官网 [Rime](http://rime.im/) ，有详细指南。吐槽一下百度根本没抓取，完全找不到。
    * [「鼠鬚管」的调教笔记](http://www.jianshu.com/p/ef2d9442fb0c)，有现成配置。

#### Google Chrome ####

以前为了不装 flash ，应负不支持 Safari 的情况。后来发现简直是烧电狂魔，而且 flash 问题可以通过 Develop → Use Agent →  Ipad、Iphone、Chrome 随便选一个（需先在 Safari 设置中开启 Develop 选项）强制转换为 HTML5。

#### iTerm ####

包装好的 Tmux，Terminal 的强大替代品。

#### Microsoft Office ####

2016 还是很不错的，也没出现太多不兼容的情况。

#### MPlayer ####

免费的播放器。

#### Parallels Desktop ####

强大的虚拟机软件。

#### PopClip ####

选中文字后弹出复制，粘贴，🔍，跳转到网址等常用功能，以及查词，翻译，命令行等扩展功能。

#### RescueTime ####

电脑使用情况记录。

#### Shorcat ####

用键盘解决问题。

#### Sublime Text ####

优雅，崇高，快速，可扩展性强的强大文本编辑器。

[Reference](http://voleking.me/2016/02/07/Sublime-Text-Personal-Setting/)

#### Tuck ####

将窗口隐藏在屏幕四周，光标移动到屏幕边缘时显示。

#### Yoink ####

停放文件，简化复制粘贴坨拽工作。

#### QQ WeChat ####

没什么好介绍的了

#### Xcode ####

用不上的话也要把 command-line-tool 装了。

#### GoAgentX、Lantern、ShadowsocksX ####

懂的懂，Lantern 免费好用，就是连校园网时要 quit 比较麻烦。

# Development environment #

[my config]()

## Shell ##

+ Homebrew + RubyGems + Node.js
    * [MAC 命令行 HomeBrew ，RubyGems， Node.js详解](http://blog.csdn.net/youxiansanren/article/details/46623173)
+ zsh + oh-my zsh [robbyrussell/oh-my-zsh · GitHub](https://github.com/robbyrussell/oh-my-zsh)
+ tommorow color scheme [chriskempson/tomorrow-theme · GitHub](https://github.com/chriskempson/tomorrow-theme)
+ theme: pure [sindresorhus/pure · GitHub](https://github.com/sindresorhus/pure)
+ zsh-syntax-highlighting [zsh-users/zsh-syntax-highlighting · GitHub](https://github.com/zsh-users/zsh-syntax-highlighting)
+ Tmux + Vim

#### brew list ####

aria2, autojump, reattach-to-user-namespace, tig, tmux, wget, zsh-syntax-highlighting

#### gem list ####

jekyll

#### npm list ####

gitbook, speed-test

#### pip list ####

powerline

