---
title: vim使用笔记
date: 2019-06-28 15:00
updated: 2019-06-28 16:00
tags: [vim]
categories: 随笔
mathjax: true
description: 日常vim配置&操作记录
---

# vim快捷键

![vim_shortcut_key_ZH-CN](note_vim/vim_shortcut_key_ZH-CN.gif)

# vim参数配置

vim配置路径： `~/.vimrc`

|            命令             |           功能            |             备注             |
| :-------------------------: | :-----------------------: | :--------------------------: |
|        set tabstop=4        |     设置tab所占的列数     |           默认为8            |
|      set shiftwidth=4       |        设置缩进为4        |           默认为8            |
|        set expandtab        |  输入的tab自动转化为空格  |         noexpandtab          |
|       set softtabstop       | 敲入tab键时实际占有的列数 |       由space和tab组成       |
|       set autoindent        |      回车后自动缩进       |                              |
|                             |                           |                              |
|          set list           |    显示tab，space字符     |        不显示：nolist        |
| set listchars=tab:▸\ ,eol:¬ |    设置tab和换行符显示    |                              |
|         set number          |         显示行数          |       不显示：nonumber       |
|      set laststatus=2       |       总显示状态行        |  0: 不显示，1:多余一个显示   |
|         set nowrap          |        不自动换行         |                              |
|        set showmatch        |    高亮显示匹配的括号     |                              |
|          set ruler          |    右下角显示光标位置     |                              |
|       set visualbell        |     出错时，屏幕闪烁      |                              |
|                             |                           |                              |
|          syntax on          |         开启高亮          |                              |
|     hi GROUP KET=VALUE      |     高亮设置，见后文      |                              |
|                             |                           |                              |
|       nnoremap / /\v        |        快捷键映射         | \v: 任何元字符都不用加反斜杠 |
|       vnoremap / /\v        |                           |  \V: 任何元字符都要加反斜杠  |
|                             |                           |                              |
|        set hlsearch         |         高亮搜索          |                              |
|         set mouse=a         |   鼠标可以点选、滚动等    |       关闭：set mouse=       |

<!--more-->

# vim九个高亮分组

```shell
Comment    : 注释
Constant   : 常量，例如数字、引号内字符串、布尔值。
Identifier : 变量标识符名称。
Statement  : 编程语言的声明，一般是像“if”或“while”这样的关键字。
PreProc    : 预处理，例如C语言中的“#include”。
Type       : 变量类型，例如“int”。
Special    : 特殊符号，通常是类似字符串中的“\n”。
Underlined : 文本下划线。
Error      : 显示编程语言错误的文本。
```

设置方式：hi GROUP KEY=VALUE，KEY和部分VALUE如下：

```shell
# term、cterm和gui，代表黑白终端、彩色终端和图形界面
# 除了term以外，另外两个基本键还有两个扩展键名base-namefg和base-namebg
term/cterm/gui: bold, underline, reverse, italic, none

ctermfg/ctermbg: red, yellow, green , blue, magenta, cyan, white, blcak, gray

guifg/guibg: 以上所有颜色，而且还可以使用#rrggbb格式色彩。
```



# 个人设置

参考自：https://gist.github.com/simonista/8703722 

```shell
" Don't try to be vi compatible
set nocompatible

" Helps force plugins to load correctly when it is turned back on below
filetype off

" TODO: Load plugins here (pathogen or vundle)

" Turn on syntax highlighting
syntax on

" For plugins to load correctly
filetype plugin indent on

" TODO: Pick a leader key
" let mapleader = ","

" Security
set modelines=0

" Show line numbers
set number

" Show file stats
set ruler

" Blink cursor on error instead of beeping (grr)
set visualbell

" Encoding
set encoding=utf-8

" Whitespace
set wrap
set textwidth=79
set formatoptions=tcqrn1
set tabstop=4
set shiftwidth=4
set softtabstop=4
set expandtab
set noshiftround

" Cursor motion
set scrolloff=3
set backspace=indent,eol,start
set matchpairs+=<:> " use % to jump between pairs
runtime! macros/matchit.vim

" Move up/down editor lines
nnoremap j gj
nnoremap k gk

" Allow hidden buffers
set hidden

" Rendering
set ttyfast

" Status bar
set laststatus=2

" Last line
set showmode
set showcmd

" Searching
nnoremap / /\v
vnoremap / /\v
set hlsearch
set incsearch
set ignorecase
set smartcase
set showmatch
map <leader><space> :let @/=''<cr> " clear search

" Remap help key.
inoremap <F1> <ESC>:set invfullscreen<CR>a
nnoremap <F1> :set invfullscreen<CR>
vnoremap <F1> :set invfullscreen<CR>

" Textmate holdouts

" Formatting
map <leader>q gqip

" Visualize tabs and newlines
set listchars=tab:▸\ ,eol:¬
" Uncomment this to enable by default:
" set list " To enable by default
" Or use your leader key + l to toggle on/off
map <leader>l :set list!<CR> " Toggle tabs and EOL

" Color scheme (terminal)
set t_Co=256
set background=dark
let g:solarized_termcolors=256
let g:solarized_termtrans=1
" put https://raw.github.com/altercation/vim-colors-solarized/master/colors/solarized.vim
" in ~/.vim/colors/ and uncomment:
" colorscheme solarized

" mouse
set mouse=a

" ctags
" set tags=./tags,tags;$HOME
" set autochdir
```

# 其他

1. 查看使用哪个的vim：`which vim`
2. 在`.vimrc`文件中，使用双引号进行注释

## vim 多窗口

1. 多窗口切换

   ```shell
   vim -o file1 file2
   vim -O file1 file2
   # 以上通过 Ctrl+ww 进行切换
   
   vim file1 file2
   # :ls 键入命令查看文件
   # :b<n> 进行切换，如 :b2
   ```

2. 关闭当前窗口`:bd`，关闭所有窗口 `:qa`, `:wqa`等

## 多行注释与取消

- 注释

  `Ctrl+v`进入块可视模式，选中需要注释的行

  `Shift+i`，然后输入`#`，第一行行首出现`#`

  连按两次`esc`，所有行都注释掉了

- 取消注释

  `Ctrl+v`选中所有的`#`

  `dd`删除

## 代码跳转

Ctags finds the definition of a symbol or a function. Cscope can find all the places calling a function. using both of them makes navigation in large source trees very easy.

### ctags

1. 下载安装 `jumbo install ctags`
2. 在代码目录里生成tags `ctags -R *`
3. 在代码里 `CTRL + ]` 跳转，按`CTRL+T`跳回

4. `~/.vimrc`文件：`set tags=./tags,tags;$HOME`

   ctag的一些[用法](https://stackoverflow.com/questions/563616/vim-and-ctags-tips-and-tricks)

### cscope

一个比较清爽的[教程](https://invisprints.wordpress.com/2016/09/24/ctagscscope/)

1. 下载安装`jumbo isntall cscope`

2. 缺省状态下 cscope 只扫描 *.c, *.h, *.l, *.y 文件。其实它也支持 C++ 和 Java。如果希望解析这些文件，则需要把这些文件的路径保存在 cscope.files 文件中，这样 cscope 就会为这些文件生成索引。通常用 `find` 命令生成 cscope.files。

   ```
   find . -name "*.h" -o -name "*.cpp" > cscope.files
   cscope -Rbkq 
   ```

   

3. 生成索引文件`cscope -Rbkq`

   其中，R表示搜索子目录，b表示不进入cscope界面，q表示生成cscope.in.out和cscope.po.out文件，加快cscope的索引速度

4. 给vim添加数据库和查询已添加的数据库

   ```
   :cs add [数据库路径]
   :cs show
   ```

   

- s: 查找C语言符号，即查找函数名、宏、枚举值等出现的地方
- g: 查找函数、宏、枚举等定义的位置，类似ctags所提供的功能
- d: 查找本函数调用的函数
- c: 查找调用本函数的函数
- t: 查找指定的字符串
- e: 查找egrep模式，相当于egrep功能，但查找速度快多了
- f: 查找并打开文件，类似vim的find功能
- i: 查找包含本文件的文件