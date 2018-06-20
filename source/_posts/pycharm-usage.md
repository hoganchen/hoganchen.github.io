---
title: pycharm使用问题记录
date: 2018-06-11 16:17:29
tags: Editor
---

<ol>

##### Pycharm shortcuts reference link
http://blog.csdn.net/u013088062/article/details/50100121
http://www.jianshu.com/p/23e52f7b8ec7

<!-- more -->


##### 编辑
```
1. cmd + /				注释光标所在的当前行
2. cmd + b				跳转到函数声明
3. cmd + mouse click	跳转到函数声明
4. cmd + delete			删除当前行
5. cmd + backspace		删除当前行
6. opt + delete			删除光标前一个字符串
7. cmd + c				复制当前行，仅复制，不粘贴
8. cmd + x				剪切当前行，仅剪切
9. cmd + d				复制并粘贴当前行或块，块操作需要先选择
10. shift + enter		当前光标后新建一行
11. cmd + enter			当前光标前新建一行
```

##### 格式化代码
```
ctrl + alt + L			注意L为大写
```

##### 调试
```
1. ctrl + shift + r		运行模式执行当前程序
2. ctrl + shift + d		调试模式执行当前程序，可设置断点，单步
```

##### FAQ
```
3.1 pycharm 能显示当前 python 文件下的函数和类的列表吗？
3.1.1 左侧 project 工具栏窗口顶部那个齿轮有个 show member 选项，默认是不开的，勾选后 py 文件会显示内部定义的 class 和 method
3.1.2 左边栏： structure
        或者到设置里面 => keymap => file structure
        mac 默认快捷键是 cmd + f12, 我习惯改成 sublime 里面用的 cmd + r
3.1.3 View->Tool Buttons 显示侧边栏
3.1.4 View->Tool Windows->Structure 显示单个文件的class和method结构
```

