---
title: windows批处理使用问题记录
date: 2018-06-11 16:38:50
tags: Bat
---

<!-- more -->

<ol>

##### <li> Echo命令
http://www.jb51.net/article/30987.htm
https://zhidao.baidu.com/question/21121153.html
```
echo off -- 关闭回显
@echo off
```

##### <li> Set命令
http://www.jb51.net/article/18973_all.htm
http://blog.csdn.net/djkin99/article/details/2182206
```
set,E文翻译过来就是“设置”的意思，相当于数学里的“令”。
如：set X=5，就是令X=5的意思。
语法形式：
SET [variable=[string]]
SET /P variable=[promptString]
SET /A expression

一、SET [variable=[string]]

示例1:
@echo off
set
pause
显示所有的变量的值

示例2:

@echo off
set var=我是值
echo %var%
pause
请看 set var=我是值 ,这就是BAT直接在批处理中设置变量的方法!
set 是命令 var是变量名 =号右边的"我是值"是变量的值
在批处理中我们要引用这个变量就把var变量名用两个%(百分号)扩起来,如%var%

二、SET /P variable=[promptString]

有时候我们需要提供一个交互界面,让  用户自己输入变量的值,然后我们在来根据这个值来做相应操作,现在我就来说说这SET的这  种语法,只需要加一个"/P"参数就可以了!
实例1:
@echo off
set /p var=请输入你的名字:
echo 您的名字是:%var%
pause
set /p 是命令语法 var是变量名 =号右边的"请输入变量的值: ",这个是提示语,不是变
量的值了!
运行后,我们在提示语后面直接输入robin,就会显示一行您” 您的名字是:robin”

三、SET /A expression

/A 命令行开关指定等号右边的字符串为被评估的数字表达式。
该表达式解析很简单并以递减的优先权顺序支持下列操作:
() - 分组
! ~ - - 一元运算符
* / % - 算数运算符
+ - - 算数运算符
<< >> - 逻辑移位
& - 按位“与”
^ - 按位“异”
| - 按位“或”
= *= /= %= += -= &= ^= |= <<= >>= - 赋值
, - 表达式分隔符
set的/A参数就是让SET可以支持数学符号进行加减等一些数学运算!
现在开始举例子介绍这些数学符号的用法:
看例子 这里的例子请直接在CMD下拷贝命令运行,不需要保存为BAT!
set /a var=1 + 1
set /a 语法, var变量名 1 + 1 数学式子
  拷贝运行后会直接显示一个2,或者运行完后我们输入echo %var%,也是二,这就是
一个简单的加法运算!
```

##### <li> 批处理的注释语句
http://blog.csdn.net/wh_19910525/article/details/8125762
https://lzw.me/a/bat-rem.html
```
写bat批处理也一样，都要用到注释的功能，这是为了程式的可读性


在批处理中，段注释有一种比较常用的方法：

    goto start
     = 可以是多行文本，可以是命令
     = 可以包含重定向符号和其他特殊字符
     = 只要不包含 :start 这一行，就都是注释
    :start

另外，还有其他各种注释形式，比如：

    1、:: 注释内容（第一个冒号后也可以跟任何一个非字母数字的字符）
    2、rem 注释内容（不能出现重定向符号和管道符号）
    3、echo 注释内容（不能出现重定向符号和管道符号）〉nul
    4、if not exist nul 注释内容（不能出现重定向符号和管道符号）
    5、:注释内容（注释文本不能与已有标签重名）
    6、%注释内容%（可以用作行间注释，不能出现重定向符号和管道符号）
    7、goto 标签 注释内容（可以用作说明goto的条件和执行内容）
    8、:标签 注释内容（可以用作标签下方段的执行内容）
```

##### <li> 变量赋值

##### <li> IF语句
http://www.jb51.net/article/14986.htm
http://blog.163.com/for_dba/blog/static/195623250201183094021245/
http://www.bathome.net/redirect.php?fid=5&tid=8072&goto=nextoldset
http://www.bathome.net/redirect.php?fid=5&tid=1962&goto=nextoldset
```
 　 EQU - 等于
　　NEQ - 不等于
　　LSS - 小于
　　LEQ - 小于或等于
　　GTR - 大于
　　GEQ - 大于或等于
```

##### <li> For循环
http://bbs.bathome.net/thread-2189-1-1.html
http://www.jb51.net/article/93170.htm
http://blog.csdn.net/jeefchen/article/details/5663822
https://yq.aliyun.com/ziliao/89455
http://www.cnblogs.com/liuhy/p/3229319.html

循环语句continue功能实现
http://www.bathome.net/thread-8731-1-1.html
http://www.bathome.net/thread-11422-1-1.html
http://bbs.csdn.net/topics/380068572
```
格式：FOR [参数] %%变量名 IN (相关文件或命令) DO 执行的命令

　　作用：对一个或一组文件，字符串或命令结果中的每一个对象执行特定命令，达到我们想要的结果。
　　注意：在批处理文件中使用 FOR 命令时，指定变量请使用 %%variable,而不要用 %variable。变量名称是区分大小写的，所以 %i 不同于 %I.
　　关于：for命令可以带参数或不带参数，带参数时支持以下参数:/d /l /r /f
　　下面分别解释一下

　　零：无参数时:

　　FOR %variable IN (set) DO command [command-parameters]
　　%variable 指定一个单一字母可替换的参数。
　　(set) 指定一个或一组文件。可以使用通配符。
　　command 指定对每个文件执行的命令。
　　command-parameters
　　为特定命令指定参数或命令行开关。

　　TTT示例：
　　for %%i in (t*.*) do echo %%i --显示当前目录下与t*.*相匹配的文件(只显示文件名，不显示路径)
　　for %%i in (d:\mydocuments\*.doc) do @echo %%i --显示d:\mydocuments\目录下与*.doc相匹配的文件
```

##### <li> 变量扩展
http://www.bathome.net/thread-2899-1-1.html
http://bbs.bathome.net/thread-354-1-1.html
http://bbs.bathome.net/thread-112-1-1.html
http://bbs.bathome.net/thread-2898-1-1.html
http://bbs.bathome.net/thread-3083-1-1.html

http://blog.csdn.net/subkiller/article/details/7344509

```
在批处理中,我们可以用setloacl ENABLEDELAYEDEXPANSION这个命令来启用"延迟环境变量扩展"

在我们启用了"延迟环境变量扩展"后,当CMD在解释涵有嵌套格式的命令时,他会把嵌套的命令一条一条的先执行一次,然后再进行匹配操作,这样我们的赋值操作就会完成.并且再"延迟环境变量扩展"启用后,CMD会用!号来判断这是不是一个变量,如没启用来变量用%name%这样的格式判断,启用后就用!name!这样的格式判断了,这个符号我们需要注意!


先来说说变量延迟扩展吧。当然，放狗一搜，就能看到满天飞的关于变量延迟扩展的文章，所以，我这里就简单介绍一下。先来看一段批处理：

[cpp] view plain copy

    set str=test

    if %str%==test (
        set str=another test
        echo %str%
    )

上面的代码段极其简单，给str赋值，判断其值是否为test，如果是，重新赋值为another test，再显示str的值。

作为正常人的思维，这里显示的肯定是another test了，但其实不是，其显示的仍然是test，这是为什么？因为：windows在解释执行此代码段时，在遇到if语句后的括号后，只把它当一条语句处理而不是两条语句，所以，在第二条语句中的%str%会被替换成它目前的值test，上面的代码相当于下面的代码的效果：

[cpp] view plain copy

    set str=test

    if %str%==test (
        set str=another test
        echo test    ::注意这里
    )

所以，输出自然是test了。

这样编程的灵活性就大大降低了，于是，M$就想了一个workground的方法，那就是变量延迟，很简单，看如下代码：

[cpp] view plain copy

    @echo off
    setlocal enabledelayedexpansion    ::注意这里

    set str=test

    if %str%==test (
        set str=another test
        echo !str!      ::注意这里
        echo %str%  ::区别
    )


现在会输出什么呢？试一下就知道，第一行输出another test，第二行输出test。

现在解释一下，setlocal enabledelayedexpansion用于开启变量延迟，这是告诉解释器，在遇到复合语句的时候，不要将其作为一条语句同时处理，而仍然一条一条地去解释。但是这时必须用!str!来引用变量，如果仍然用%str%引用是不起作用的。

好了，变量延迟扩展解释完了，至少这就是我知道的变量延迟扩展。
```

##### <li> 批处理字符串处理
http://blog.csdn.net/benkaoya/article/details/7784013
http://www.cnblogs.com/ZC_Mo-Blog/archive/2009/12/28/1633766.html
http://blog.csdn.net/elimago/article/details/4145800
http://www.jb51.net/article/52744.htm
```
@echo off
set ifo=abcdefghijklmnopqrstuvwxyz0123456789
echo 原字符串（第二行为各字符的序号）：
echo %ifo%
echo 123456789012345678901234567890123456
echo 截取前5个字符：
echo %ifo:~0,5%
echo 截取最后5个字符：
echo %ifo:~-5%
echo 截取第一个到倒数第6个字符：
echo %ifo:~0,-5%
echo 从第4个字符开始，截取5个字符：
echo %ifo:~3,5%
echo 从倒数第14个字符开始，截取5个字符：
echo %ifo:~-14,5%
pause


@echo off
set str1=This is string1
::设置str1中存储的字符串
set str2=%str1:~8,6%
set str3=%str1:~0,4%
set str4=%str1:~5%
::字符串截取
echo 原字符串：
echo str1=%str1%
echo 截取得到的字符串：
echo str2=%str2%
echo str3=%str3%
echo str4=%str4%
::输出执行结果
echo 输出完毕，按任意键退出&&pause>nul&&exit
```

##### <li> 批处理读取文件内容
http://josephdong.blog.163.com/blog/static/1774389720093402836603/
http://www.jb51.net/article/39990.htm
http://luhongyuaaa.blog.163.com/blog/static/217554222010213101959533/
https://zhidao.baidu.com/question/746207667158208932.html

##### <li> Tips
http://bbs.bathome.net/thread-37612-1-1.html
```
批处理循环中赋值，因为他在括号里面，算是复合句。复合句里面设置变量要用变量扩展


@echo off
set aFile=bak-%DATE:~4,4%%DATE:~9,2%%DATE:~12,2%
set bFile=bak-%TIME:~0,2%%TIME:~3,2%%TIME:~6,2%
set cFile=bak-%DATE%
echo Afile=%aFile%
echo Bfile=%bFile%
echo Cfile=%cFile%

方法一

for /f %%i in (.\tmp.txt) do (echo %%i)  & echo %%i

方法二

set /P OEM=<tmp.txt

```

##### <li> Example
根据file_filter.txt中的文件列表，删除未在列表中的文件
```
@echo off

setlocal ENABLEDELAYEDEXPANSION

set Found=0

for /f %%i in ('dir *.py /b') do (
    set Found=0
    for /f %%j in (file_filter.txt) do (
        if !Found! == 0 (
            if %%i equ %%j (
                REM echo %%i
                set Found=1
                REM echo !Found!
            )
        )
    )

    if !Found! == 0 (
        del %%i
    )
)

pause
```