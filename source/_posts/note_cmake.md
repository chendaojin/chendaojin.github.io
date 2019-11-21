---
title: cmake使用笔记
date: 2019-11-19 15:00
updated: 2019-11-19 16:00
tags: [c++]
categories: 技术
mathjax: true
description: 个人笔记，便于查阅
---

使用CLion创建一个项目`beam_route`，默认的CMakeList文件内容如下：

```cmake
cmake_minimum_required(VERSION 3.14)
project(beam_route)

set(CMAKE_CXX_STANDARD 11)

add_executable(beam_route main.cpp)
```

1. 添加头文件目录

```cmake
include_directories(../include)
```

2. 链接的库文件目录

```cmake
# 相当于g++命令的-L选项的作用，也相当于环境变量中增加LD_LIBRARY_PATH的路径的作用
link_directories("/usr/lib/x86_64-linux-gnu")
```

3. 链接的库文件路径 

```cmake
# 直接是全路径
link_libraries("/usr/lib/x86_64-linux-gnu/libproj.a")
# 下面的例子，只有库名，cmake会自动去所包含的目录搜索
link_libraries(proj)
# 也可以链接多个
link_libraries("/usr/lib/x86_64-linux-gnu/libproj.so" "/usr/lib/x86_64-linux-gnu/libpthread.so")

target_link_libraries(beam_route proj)       # 连接libproj.so库，默认优先链接动态库
target_link_libraries(beam_route libproj.a)  # 显示指定链接静态库
target_link_libraries(beam_route libproj.so) # 显示指定链接动态库
```

5. target_link_libraries和link_libraries 的区别
   - link_libraries用在 add_executable 之前，target_link_libraries 要在 add_executable 之后
   - [不建议使用link_libraries](https://cmake.org/cmake/help/v3.0/command/link_libraries.html)
6. 设置默认静态链接

```cmake
set(CMAKE_CXX_FLAGS "-static ${CMAKE_CXX_FLAGS}")
```

7. 查找当前目录下的所有源文件

```cmake
# 将名称保存到 DIR_SRCS 变量
aux_source_directory(${CMAKE_CURRENT_LIST_DIR} DIR_SRCS)
```

参考资料：

[1. cmake 添加头文件目录，链接动态、静态库](https://www.cnblogs.com/binbinjx/p/5626916.html)

[☆2. 使用CMake组织C++工程：CMake 常用命令和变量](https://elloop.github.io/tools/2016-04-10/learning-cmake-2-commands)

8. 打印信息

```cmake
MESSAGE(STATUS "operation system is ${CMAKE_SYSTEM}")
```

9. 判断平台

```cmake
IF (CMAKE_SYSTEM_NAME MATCHES "Linux")
	MESSAGE(STATUS "current platform: Linux ")
ELSEIF (CMAKE_SYSTEM_NAME MATCHES "Windows")
	MESSAGE(STATUS "current platform: Windows")
ELSEIF (CMAKE_SYSTEM_NAME MATCHES "FreeBSD")
	MESSAGE(STATUS "current platform: FreeBSD")
ELSE ()
	MESSAGE(STATUS "other platform: ${CMAKE_SYSTEM_NAME}")
ENDIF (CMAKE_SYSTEM_NAME MATCHES "Linux")


IF (WIN32)
	MESSAGE(STATUS "Now is windows")
ELSEIF (APPLE)
	MESSAGE(STATUS "Now is Apple systens.")
ELSEIF (UNIX)
	MESSAGE(STATUS "Now is UNIX-like OS's.")
ENDIF ()
```