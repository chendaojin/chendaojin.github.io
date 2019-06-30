---
title: hexo & next 建站笔记
date: 2019-06-28 15:00
updated: 2019-06-18 16:00
tags: [hexo]
categories: 随笔
mathjax: true
description: hero & next博客搭建过程中遇到的问题及解决方法
---

# hexo图片路径的问题

- 问题描述

  hexo中，markdown文件`test.md`的资源文件夹在同级目录下的`test`文件夹中。`test.md`只能以`![](test.jpg)`的形式引入图片，而不能以`![](test/test.jpg)`引入图片。

  这样一来，在typora等编辑器中编写markdown文件时，就不能看到图片了。

- 解决方法

  1. 安装`npm install hexo-asset-image@0.0.2 —save`，1.0.0版本尚不能用
  2. hexo中的_config.yml开启`post_asset_fodler:true`
  3. markdown文件中，这样`test.md`就可以用这些引入图片了：`![]  (./test/test.jpg)`,`![](test/test.jpg)`,`![](test.jpg)`

# NGINX多路径解析

默认配置文件目录: /etc/nginx/nginx.conf

![nginx.conf](note_hexo_and-next/nginx.conf.png)