---
title: vim使用笔记
date: 2019-06-28 15:00
updated: 2019-06-28 16:00
tags: [vim]
categories: 随笔
mathjax: true
description: 
---

<!--more-->

# vim参数配置

vim配置路径： `~/.vimrc`

|       命令       |            功能             |       备注       |
| :--------------: | :-------------------------: | :--------------: |
|  set tabstop=4   |      设置tab所占的列数      |     默认为8      |
| set shiftwidth=4 |         设置缩进为4         |     默认为8      |
|  set expandtab   | 输入tab时自动将其转化为空格 |   noexpandtab    |
| set softtabstop  |  敲入tab键时实际占有的列数  | 由space和tab组成 |
|  set autoindent  |       回车后自动缩进        |                  |
|                  |                             |                  |
|     set list     |     显示tab，space字符      |  不显示：nolist  |
|    set number    |          显示行数           | 不显示：nonumber |
|                  |                             |                  |

# vim快捷键

![vim_shortcut_key_ZH-CN](note_vim/vim_shortcut_key_ZH-CN.gif)

# 个人设置

```shell
set tabstop=4
set shiftwidth=4
set expandtab
set number
set autoindent
set list
```

# 其他

# 其他

1. 查看使用哪个的vim：`which vim`
2. 