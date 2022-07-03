---
title: use cmake
date: 2022-07-03 20:46:42
tags: cmake boost linux
---



## How to compile by using cmake on Ubuntu

This article explained how I succeeded to compile a project (C/C++) with `CMake` on Ubuntu



<!-- more-->



### Choose `boost` library with care

---

首先要根据当前`gcc`的版本，选择`boost`版本，对应的`boost`版本不能太旧，也不能太新，否则很容易出现当前版本的`gcc`在编译时遇到不兼容的情况（boost源代码）

比如，当前我Ubuntu的`gcc`版本如下：

```bash
gcc (Ubuntu 9.3.0-17ubuntu1~20.04) 9.3.0
Copyright (C) 2019 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```

它看起来是2019年发布的，因此，根据此年份，在`boost` official website上查找对应年份的release版本，找到大概差不多的版本是`1.69.0`，所以选择这个版本。



### Compile `boost` library

---

参考文章：[Install Boost library on Linux]()，编译对应的`boost`版本，注意其中提到的`--layout`option的问题，为了`cmake`能够正确查找到`boost`库，这里需要编译出来的库不要带编译器、boost版本信息等字符串（即声明`--layout=system`）



### CMake with project

---

需要编译的project是[cpp11](https://github.com/Pyrad/cpp11)这个git repo

对应的`CMakeLists.txt`如下，需要注意的是，

- 要将`CMAKE_CXX_STANDARD`设定为`14`，否则有些语法在`C++11`中不能正确识别
- 记得设定`BOOST_ROOT`

```cmake
# Set the minimun version of CMake
CMAKE_MINIMUM_REQUIRED(VERSION 3.10)

# Set the project name
PROJECT(MYCPP11TEST VERSION 0.1)

# specify the C++ standard
SET(CMAKE_CXX_STANDARD 14)
SET(CMAKE_CXX_STANDARD_REQUIRED True)

# If you'd like to build in a Unix way in windows platform,
# add the following
# SET(MY_MINGW64_HOME "/mingw64")
# SET(CMAKE_MAKE_PROGRAM "${MY_MINGW64_HOME}/bin/mingw32-make.exe")
# SET(CMAKE_C_COMPILER "${MY_MINGW64_HOME}/bin/gcc.exe")
# SET(CMAKE_CXX_COMPILER "${MY_MINGW64_HOME}/bin/g++.exe")

MESSAGE(STATUS "[PYRAD] This is the BINARY directory: " ${MYCPP11TEST_BINARY_DIR})
MESSAGE(STATUS "[PYRAD] This is the SOURCE directory: " ${MYCPP11TEST_SOURCE_DIR})

# Let cmake know where the root of boost library is
set(BOOST_ROOT /home/pyrad/procs/boost_1_69_0)

# Let cmake search for boost libraries
find_package(Boost 1.65.0 REQUIRED COMPONENTS filesystem regex)

#check if boost was found
if(Boost_FOUND)
	include_directories(${Boost_INCLUDE_DIRS})
    message(STATUS "[PYRAD] boost library is found")
	message(STATUS "[PYRAD] Boost_INCLUDE_DIRS = ${Boost_INCLUDE_DIRS}.")
    message(STATUS "[PYRAD] Boost_LIBRARIES = ${Boost_LIBRARIES}.")
    message(STATUS "[PYRAD] Boost_LIB_VERSION = ${Boost_LIB_VERSION}.")
else()
    message (FATAL_ERROR "Cannot find Boost")
endif()


AUX_SOURCE_DIRECTORY(./ MY_DIR_SRC)

# Add the executable
#ADD_EXECUTABLE(mymainrun main.cpp)
ADD_EXECUTABLE(mymainrun ${MY_DIR_SRC})
```



### Compile

---

在这个目录下面建一个`build`目录来供`CMake`生成一些临时文件等，然后编译

```bash
$ cmake ../src/ -G "Unix Makefiles"
$ cmake --build ..
```



