---
title: Bash使用问题记录
date: 2018-06-11 15:31:24
tags: Bash
---

<ol>

##### 多行注释 & here document
```
https://stackoverflow.com/questions/27201004/line-54-warning-here-document-at-line-42-delimited-by-end-of-file-wanted-eof
https://stackoverflow.com/questions/18660798/here-document-gives-unexpected-end-of-file-error

: <<EOF
......code line
......code line
EOF

: << EOF
......code line
......code line
EOF

或者如下，<<号后的-表示去除匹配行的<tab>键，注意，后面一个EOF必须以一个或者多个tab键对齐，如果EOF前面是空格，会去找以<tab>对齐的EOF
            : <<-EOF
            ......code line
            ......code line
<tab><tab>EOF
```

<!-- more -->

##### 命令与变量
```
命令执行结果可以用`cmd`，也可以用$(cmd)
变量的引用需要用${variable}

for dirlist in $(ls ${workdir})
test_path=`pwd` or test_path=$(pwd)
test_path=$(dirname $(dirname $(pwd)))/code/test
cd ${test_path}
```

##### 空语句
```
： # 冒号
```

##### unary operator expected error
```
如果$2为空，执行如下语句，会得到unary operator expected error
if [ 'gcovr' = $2 ]
then
    LCOV_FALG=0
fi

修改为:
if [[ 'gcovr' = $2 ]]
then
    LCOV_FALG=0
fi
```

##### bash脚本不需要命令输出
```
which ls > /dev/null
```

##### 命令行循环语句
http://blog.csdn.net/column/details/wanbash.html
```
while :; do ls -lrth; sleep 2; done
while true; do ls -lrth; sleep 2; done
while [ 1 ]; do ls -lrth; sleep 2; done
while [ 0 ]; do ls -lrth; sleep 2; done

循环复制文件
for i in {10..20}; do cp test_log.txt HTC_test_${i}.txt; done

循环执行测试
rm -rf st_main.log; for i in {1..10}; do condapython -u st_main.py >> ./st_main.log 2>&1; done
for i in {1..10}; do condapython -u st_main.py >> ./st_main_$(date '+%Y%m%d%H%M').log 2>&1; done
datetime=$(date '+%Y%m%d%H%M'); for i in {1..10}; do condapython -u st_main.py >> ./st_main_${datetime}.log 2>&1; done

tail -f $(ls -rth | tail -1)

命令行循环语句
hogan@hogan:~/Docs/codes/python/practise$ for i in 1 2 3 4 5 6 7 8 9 10; do ls; done
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
hogan@hogan:~/Docs/codes/python/practise$ for i in $(seq 10); do ls; done
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
hogan@hogan:~/Docs/codes/python/practise$ for i in {1..10}; do ls; done
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
hogan@hogan:~/Docs/codes/python/practise$ for((i=0; i<=10; i++)); do ls; done
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
calc_prime.py  lintcode_001.py  lintcode_k_point.py  prime_number.py
hogan@hogan:~/Docs/codes/python/practise$


命令行检查多个目录git状态
for file in $(ls); do cd ${file}; echo -e "enter the ${file} folder..."; git st; cd ..; done
```

##### 获取脚本名字和脚本路径
```
basename $0 # 脚本名字
dirname $0 #脚本路径
```

##### Shell变量作用域
```
(1)Shell脚本中定义的变量是global的，其作用域从被定义的地方开始，到shell结束或
被显示删除的地方为止。

例1：脚本变量的作用域
#!/bin/bash
#define the function ltx_func
ltx_func()
{
    echo $v1
    #modify the variable v1
    v1=200
}
#define the variable v1
v1=100
#call the function ltx_func
ltx_func
echo $v1

结果：
100
200
解析：脚本变量v1的作用域从被定义的地方开始，到shell结束。调用函数ltx_func的地方在变量v1的作用域内，所以能够访问并修改变量v1。

(2)Shell函数定义的变量默认是global的，其作用域从“函数被调用时执行变量定义的地方”开始，到shell结束或被显示删除处为止。函数定义的变量可以被显示定义成local的，其作用域局限于函数内。但请注意，函数的参数是local的。

例2：函数定义的global变量
#!/bin/bash
#define the function ltx_func
ltx_func()
{
    #define the variable v2
    v2=200
}
#call the function ltx_func
ltx_func
echo $v2

结果：
200
解析：函数变量v2默认是global的，其作用域从“函数被调用时执行变量定义的地方”开始，到shell结束为止。注意，不是从定义函数的地方开始，而是从调用函数的地方开始。打印命令在变量v2的作用域内，所以能够访问变量v2。

例3：函数定义的local变量
#!/bin/bash
#define the function ltx_func
ltx_func()
{
    #define the local variable v2
    local v2=200
}
#call the function ltx_func
ltx_func
echo $v2

结果：
（空）
解析：函数变量v2显示定义为local的，其作用域局限于函数内。打印命令在函数外，不在变量v2的作用域内，所以能够不能访问变量v2。

例4：函数参数是local变量
#!/bin/bash
#define the function ltx_func
ltx_func()
{
    echo "param 1: $1"
}
#call the function ltx_func
ltx_func 100

结果：
100
解析：函数参数是local的，通过位置变量来访问。打印命令输出函数的第一个参数。

(3)如果同名，Shell函数定义的local变量会屏蔽脚本定义的global变量。

例5：同名local变量屏蔽global变量
#!/bin/bash
#define the function ltx_func
ltx_func()
{
    echo $v1
    #define the local variable v1
    local v1=200
    echo $v1
}
#define the global variable v1
v1=200
#call the function ltx_func
ltx_func
echo $v1

结果：
100
200
100
解析：global变量v1的作用域从被定义的地方开始，到shell结束。调用函数ltx_func的地方在变量v1的作用域内，所以能够变量v1。函数又定义了同名的local变量v1，同名local变量屏蔽global变量，所以函数第二次打印访问的是local变量。退出函数后再次打印v1，此时函数定义的local变量已经消失，访问的是global变量。

来源  http://blog.csdn.net/ltx19860420/article/details/5570902
```

##### 删除变量和函数
```
unset variable_nameaa
unset function_name
```

##### 命令执行结果以及变量赋值
```
current_path=`pwd`
current_path=$(pwd)

dup_current_path=${current_path}
dup_current_path=$current_path

new_relative_path="/tools"
new_path=${current_path}${new_relative_path}
new_path="${current_path}/tools"

# 以上命令的执行结果存放在变量中，只保存标准输出，标准错误输出不会保存在变量中，标准输出和标准错误输出保存变量可采用以下的方式
gitout=$(git pull --rebase 2>&1)
```

##### 查看当前shell
```
ps -p $$
```

##### cut命令
https://www.ibm.com/support/knowledgecenter/zh/ssw_aix_72/com.ibm.aix.cmds1/cut.htm#cut__row-d3e151685
http://blog.csdn.net/Frozen_fish/article/details/2260804
http://www.cnblogs.com/dong008259/archive/2011/12/09/2282679.html
```
cut 命令从文件的每一行剪切字节、字符和字段并将这些字节、字符和字段写至标准输出。
如果不指定 File 参数，cut 命令将读取标准输入。必须指定 -b、-c 或 -f 标志之一。

主要参数
-b ：以字节为单位进行分割。这些字节位置将忽略多字节字符边界，除非也指定了 -n 标志。
-c ：以字符为单位进行分割。
-d ：自定义分隔符，默认为制表符。
-f  ：与-d一起使用，指定显示哪个区域。
-n ：取消分割多字节字符。仅和 -b 标志一起使用。如果字符的最后一个字节落在由 -b 标志的 List 参数指示的<br />范围之内，该字符将被写出；否则，该字符将被排除。


命令用法：
       cut -b list [-n] [file ...]
       cut -c list [file ...]
       cut -f list [-d delim][-s][file ...]

上面的-b、-c、-f分别表示字节、字符、字段（即byte、character、field）；
list表示-b、-c、-f操作范围，-n常常表示具体数字；
file表示的自然是要操作的文本文件的名称；
delim（英文全写：delimiter）表示分隔符，默认情况下为TAB；
-s表示不包括那些不含分隔符的行（这样有利于去掉注释和标题）


上面三种方式中，表示从指定的范围中提取字节（-b）、或字符（-c）、或字段（-f）。

范围的表示方法：

N		只有第N项
N-		从第N项一直到行尾
N-M		从第N项到第M项(包括M)
-M		从一行的开始到第M项(包括M)
-		从一行的开始到结束的所有项


用途

帮助分割文件的行。
语法

cut {  -b List [  -n ] |  -c List |  -f List [  -s ] [  -d Character ] } [ File ... ]
描述

cut 命令从文件的每一行剪切字节、字符和字段并将这些字节、字符和字段写至标准输出。如果不指定 File 参数，cut 命令将读取标准输入。

必须指定 -b、-c 或 -f 标志之一。List 参数为一个以逗号分隔、以空格分隔或连字符分隔的整数的列表（顺序递增）。连字符分隔符表示范围。以下条目是 List 参数的一些示例，它可以用来指代字节、字符或字段：

1,4,7
1-3,8
-5,10
3-

其中 -5 为从第一个到第五个的简写形式，3- 为从第三个到最后一个的简写形式。

如果将 cut 命令用于字段，那么由 List 参数指定的字段的长度可以从字段到字段，从行到行发生变化。字段定界字符（比如制表符）的位置，确定字段长度。

您还可以使用 grep 命令来对一个文件进行水平剪切，和使用 paste 命令来将文件复原。要更改文件中列的次序，使用 cut 和 paste 命令。
标志
项目 	描述
-b List 	指定字节位置。这些字节位置将忽略多字节字符边界，除非也指定了 -n 标志。
-c List 	指定字符位置。例如，如果您指定 -c 1-72，cut 命令将写出文件每一行的前 72 个字符。
-d Character 	使用 Character 变量指定的字符作为指定 -f 标志时的字段定界符。您必须在对 shell 有特殊意义的字符（比如空格字符）上加上引号。
-f List 	指定文件中设想被定界字符（缺省情况下为制表符）隔开的字段的列表。例如，如果您指定 -f 1,7，cut 命令将仅写出每个行的第一和第七个字段。如果行中不包含字段定界符，cut 命令将通过它们而不对其进行任何操作（对表格的副标题有用），除非指定了 -s 标志。
-n 	取消分割多字节字符。仅和 -b 标志一起使用。如果字符的最后一个字节落在由 -b 标志的 List 变量指示的范围之内，该字符将被写出；否则，该字符将被排除。
-s 	取消不包含定界符的行。仅和 -f 标志一起使用。


echo "Hello world" | cut -c 1
H
echo "Hello world" | cut -c 1-
Hello world
echo "Hello world" | cut -c -2
He
echo "Hello world" | cut -c 1-3,5,8
Heloo

ifconfig wlan0 | grep 'inet addr' | awk '{print $2}' | cut -c 6-
173.17.40.143
```

##### tr命令
http://man.linuxde.net/tr
http://www.runoob.com/linux/linux-comm-tr.html
https://www.ibm.com/support/knowledgecenter/zh/ssw_aix_61/com.ibm.aix.cmds5/tr.htm
http://bijian1013.iteye.com/blog/2358792 (一句话脚本获取IP地址)
```
tr命令可以对来自标准输入的字符进行替换、压缩和删除。它可以将一组字符变成另一组字符，经常用来编写优美的单行命令，作用很强大。
语法
tr(选项)(参数)

选项
-c或——complerment：取代所有不属于第一字符集的字符；
-d或——delete：删除所有属于第一字符集的字符；
-s或--squeeze-repeats：把连续重复的字符以单独一个字符表示；
-t或--truncate-set1：先删除第一字符集较第二字符集多出的字符。

参数
字符集1：指定要转换或删除的原字符集。当执行转换操作时，必须使用参数“字符集2”指定转换的目标字符集。但执行删除操作时，不需要参数“字符集2”；
字符集2：指定要转换成的目标字符集。

来自: http://man.linuxde.net/tr

ifconfig wlan0 | grep 'inet addr' | awk '{print $2}' | tr -d 'addr:'
173.17.40.143
```

##### Sed命令
参考:
http://sed.sourceforge.net/sed1line_zh-CN.html
https://www.zhukun.net/archives/6975
http://coolshell.cn/articles/9104.html
https://www.ibm.com/support/knowledgecenter/zh/ssw_aix_61/com.ibm.aix.cmds5/sed.htm
http://bbs.chinaunix.net/thread-63273-1-1.html
http://bbs.chinaunix.net/thread-605570-1-1.html
http://wiki.jikexueyuan.com/project/unix/regular-expressions.html
http://wiki.jikexueyuan.com/project/shell-learning/sed-search-and-replace.html

```
hogan@hogan:~$ temp=/home/test/; var=aa
hogan@hogan:~$ echo $var
aa
hogan@hogan:~$ echo $temp
/home/test/
hogan@hogan:~$ echo $temp | sed 's/\//$var/g'
$varhome$vartest$var
hogan@hogan:~$ echo $temp | sed "s/\//$var/g"
aahomeaatestaa
hogan@hogan:~$ echo $temp | sed "s/\//\$var/g"
$varhome$vartest$var
hogan@hogan:~$ echo $temp | sed "s/.*$/&$var/g"
/home/test/aa
hogan@hogan:~$ echo $temp | sed "s/^.*$/&$var/g"
/home/test/aa
hogan@hogan:~$ echo $temp | sed "s/$/&$var/g"
/home/test/aa
hogan@hogan:~$ echo $temp | sed "s/^/&$var/g"
aa/home/test/
hogan@hogan:~$ echo "</td>Hello World" | sed "s/<[^>]\+>//g"
Hello World

ifconfig wlan0 | grep 'inet addr' | awk '{print $2}' | sed 's/addr://g'
173.17.40.143

hogan@hogan:~$ ifconfig wlan0
wlan0     Link encap:Ethernet  HWaddr e5:b4:19:6c:5e:8d
          inet addr:173.17.40.143  Bcast:173.17.40.255  Mask:255.255.255.0
          inet6 addr: fe80::e6b3:18ff:fe6b:5d8c/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:307829 errors:0 dropped:8 overruns:0 frame:0
          TX packets:86929 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:64552812 (64.5 MB)  TX bytes:20122109 (20.1 MB)

hogan@hogan:~$ ifconfig wlan0 | sed -n '/inet addr/s/^[^:]*:\([0-9.]\{7,15\}\).*/\1/p'
173.17.40.143
```

##### bash不同引号区别
http://www.igigo.net/post/archives/128

##### bash正则表达式
https://www.ibm.com/developerworks/cn/education/aix/au-unixtips3/index.html
http://wiki.jikexueyuan.com/project/linux-command/chap20.html
http://blog.csdn.net/hittata/article/details/8911117
https://www.jianshu.com/p/49d5ee46de47
https://blog.zengrong.net/post/1563.html
http://yidao620c.iteye.com/blog/1879755
```
字符集 	说明
[:alnum:] 	字母数字字符。在 ASCII 中，等价于：[A-Za-z0-9]
[:word:] 	与[:alnum:]相同, 但增加了下划线字符。
[:alpha:] 	字母字符。在 ASCII 中，等价于：[A-Za-z]
[:blank:] 	包含空格和 tab 字符。
[:cntrl:] 	ASCII 的控制码。包含了0到31，和127的 ASCII 字符。
[:digit:] 	数字0到9
[:graph:] 	可视字符。在 ASCII 中，它包含33到126的字符。
[:lower:] 	小写字母。
[:punct:] 	标点符号字符。在 ASCII 中，等价于：
[:print:] 	可打印的字符。在[:graph:]中的所有字符，再加上空格字符。
[:space:] 	空白字符，包括空格，tab，回车，换行，vertical tab, 和 form feed.在 ASCII 中， 等价于：[ \t\r\n\v\f]
[:upper:] 	大写字母。
[:xdigit:] 	用来表示十六进制数字的字符。在 ASCII 中，等价于：[0-9A-Fa-f]
```

##### bash按行读取命令输出
http://gohom.win/2015/08/16/readlineBash/
https://linux.cn/article-6119-1.html

http://blog.csdn.net/stormbjm/article/details/19173011
https://fukun.org/archives/01282174.html
```
Bash中按行读取和处理

Bash的处理文档能力肯定是不如python友好了.但是要是能用Bash来处理, 那也是十分赞的. Bash还能配合awk, sed等一起操作, 用熟了应该不比python差.但是python的扩展库多,语言友好, bash就限定在那几个程序了…好吧, 那还是要学好的.
for + cat 循环读取

使用cat 再for的缺点是, 要是有空格/tab, 就不会按行处理! 因为分隔符默认是空格,tab,换行! 这个问题再6-26号生日的博客中提及过了. 有两种写法去处理. 这里举例说明:

#! /bin/bash --login

# Backup the IFS
OLDIFS=$IFS
# Method 1:
IFS="
"
# Method 2:
IFS=$'\n'

echo > ambertype.log
for dir in `cat $1`
do
mol2pqr.sh ${dir}.mol2 pqrt no amber mbondi

for line in $(cat ${dir}.pqrt)
do
if [[ ${line:0:4} == "ATOM" || ${line:0:6} == "HETATM" ]];then
echo ${line:78:10} >> ambertype.log
fi
done

done

# Set back the IFS
IFS=$OLDIFS

这个脚本是操作文件内序号来读取文件,并提取行内信息的. 如果不设置IFS,读取结果是空白! 因为按空格和换行分隔了每个项…
while read 循环读取

比较常用的方法, 但有缺陷: 由于IFS定界符的原因, 多个定界符会合为一个进行处理. 要是使用重定义定界符的方法可以避免. 可以使用重定向输入或管道的方法进行,重定向的效率和速度更快!

# testfile:
#1   2  3
#4 5  6

# -r取消反义, 按实际显示行来输入
# 将每行内容给line, 要是line1 line2 line3则根据定界符分隔每行赋给每个变量
while read -r line
do
    echo $line
done < $testfile
# 返回
#1 2 3
#4 5 6

IFS=$'\n'
# 或者用管道
cat $testfile | while read -r line
do
    echo $line
done
#返回
#1   2  3
#4 5  6

也可以使用文件句柄的方法指明输入:

#! /bin/bash
afile=$1
bfile=$2
# 将afile文件与bfile中的每行内容拼接起来.
# 注意因为两个都要为真, 因此一个文件读完后循环将停止, 即使另一文件没读完.
while read -u3 i && read -u4 j;do
echo $i $j
done 3<$afile 4<$bfile

还有人这么做重定向..使用输入3接受标准输入,再使用文件内容重定向给标准输入(相当于保存了内容到输入3),然后再将输入3传给标准输入作为read的输入…(就不能直接0<$FILENAME写后面么..经测试,还真不行..)

#! /bin/bash
exec 3<&0
exec 0<$FILENAME
while read line
do
echo $line
done
exec 0<&3

使用自定义函数

这里使用特殊的大写字母作为变量传递.

function while_read_LINE_bottm(){
OLDIFS=$IFS
IFS=$'\n'
While read LINE
do
echo $LINE
done  < $FILENAME
IFS=$OLDIFS
}


如题，将某命令的输出结果赋值给一个变量 a

如果使用 echo $a 输出变量，则变量中的 换行都会被忽略掉，所有内容输出到一行

而使用 echo "$a"  可正常输出变量中的换行

当我们要将命令的输出保存到一个变量，再对每一行遍历进行某些操作时不能使用
    for item in "$a"; do
        ## do something
    done

语法,这样取到的变量 item  不是$a 中的一行，而是以空格分隔的一个个字符串


这种情况可以使用以下语法解决
    echo "$a" | while read i
    do
		## do something
    done
```

##### Bash Shell 解析路径获取文件名和目录名
http://blog.csdn.net/wzy_1988/article/details/40590747
http://blog.csdn.net/ljianhui/article/details/43128465
```
前言
还是今天再写一个自动化打包脚本，用到了从路径名中获取最后的文件名。这里记录一下实现过程。当然，最后我也会给出官方的做法。（ps：很囧，实现完了才发现原来Bash Shell有现成的函数）

获取文件名
假设给定的路径名为：
[plain] view plain copy

    /tmp/csdn/zhengyi/test/zhengyi.txt

awk解法
用“/”做分隔符，然后打印出最后的那一部分。实现代码如下：
[plain] view plain copy

    resFile=`echo /tmp/csdn/zhengyi/test/adb.log | awk -F "/" '{print $NF}'`

官方解法(basename)
Bash Shell本身提供了basename命令，可以直接获取路径名最后的文件名，实现代码如下：
[plain] view plain copy

    resFile=`basename /tmp/csdn/zhengyi/test/adb.log`


获取目录名
官方解法(dirname)
Bash Shell本身提供了dirname命令，特别方便，可以直接获取路径对应的目录名，实现代码如下：
[plain] view plain copy

    dirPath=`dirname /tmp/csdn/zhengyi/test/adb.log`


awk解法
可以灵活的使用分隔符，混合正则表达式：
[plain] view plain copy

    dirPath=`echo /tmp/csdn/zhengyi/test/adb.log | awk -F '/[^/]*$' '{print $1}'`


awk+for循环的方法：
[plain] view plain copy

    echo /tmp/csdn/zhengyi/test/adb.log | awk 'BEGIN{res=""; FS="/";}{ for(i=2;i<=NF-1;i++) res=(res"/"$i);} END{print res}
```

##### bash字符串操作
https://my.oschina.net/aiguozhe/blog/41557
http://blog.wtlucky.com/blog/2013/05/02/start-write-shell/

##### bash数组
https://blog.zengrong.net/post/1518.html
https://blog.zengrong.net/post/1591.html
https://nicesu.gitbooks.io/shell-guide/content/chapter4/46.html
http://blog.csdn.net/qq_31821675/article/details/74331607

##### sed命令
http://sed.sourceforge.net/sed1line_zh-CN.html
https://www.ibm.com/developerworks/cn/education/aix/au-unixtips3/index.html
https://zhengheng.me/2015/11/12/sed-course/
https://coolshell.cn/articles/9104.html
http://wiki.jikexueyuan.com/project/shell-learning/sed-search-and-replace.html
http://wiki.jikexueyuan.com/project/unix/regular-expressions.html
http://www.runoob.com/linux/linux-comm-sed.html
http://man.linuxde.net/sed
https://www.ibm.com/support/knowledgecenter/zh/ssw_aix_61/com.ibm.aix.cmds5/sed.htm
http://huchaowei.com/2017/05/24/Linux%20sed%E5%91%BD%E4%BB%A4%E8%AF%A6%E8%A7%A3/

##### sed命令unknown option to 's'解决办法
http://hadesmo.com/2015/07/20/sed.html
https://stackoverflow.com/questions/9366816/sed-unknown-option-to-s
http://blog.csdn.net/qq1124794084/article/details/76419464

##### diff命令
http://www.ruanyifeng.com/blog/2012/08/how_to_read_diff.html

##### grep命令
http://www.cnblogs.com/ggjucheng/archive/2013/01/13/2856896.html
http://mufool.com/2016/07/13/linux-grep/
https://www.teakki.com/p/57e237d4104112321cd7c91e
https://linuxstory.org/grep-regular-expressions/
https://linux.cn/article-6941-1.html
https://www.ibm.com/support/knowledgecenter/zh/ssw_aix_61/com.ibm.aix.cmds2/grep.htm
http://www.runoob.com/linux/linux-comm-grep.html
```
git st | grep -E "(Untracked files)|(Changes not staged for commit)"
git st | grep -E "Untracked files|Changes not staged for commit"
git st | grep -e "Untracked files" -e "Changes not staged for commit"
```

##### bash参数和参数扩展
https://www.ibm.com/developerworks/cn/linux/l-bash-parameters.html
http://blog.51cto.com/huangyandong/1281327
```
(1). 传递参数

   $0,$1,$2.......$N  :都是位置参数，其中$0可以表示为脚本名称(若在函数中调用则表示函数名称)。

   $* 和 $@ : 都表示除$0外的所有参数，两者在不用双引号包含时是1、一样的，也就是$*和$@是等价的，使用在双引号中扩展则不同，$*表示所有参数都作为1个单词，且受IFS特殊变量的影响(即所有参数由IFS进行分割连接)，而$@把

每个参数都扩展为1个单词即"$@"等价于"$1" "$2" ..."$N".

   $# :表示参数数量(不含$0)

注:Shell 脚本处理参数的方式与函数处理参数的方式相同。


(2).获取参数的子集(子字符串)

   一般形式: ${参数名称:开始位置:长度}

   注:开始位置和长度为整数，且从0开始

   实例: x="hello world";

         echo ${x:6:5}  #输出world

(3).获取变量值的长度

   一般形式:${#变量名称}

   实例: x="hello world";

         echo ${#x} #输出11

(4).模式匹配(可以使用通配符)

   [1].从左开始删除:

       ${变量名#要删除的字}   #表示从左边开始删除最短的匹配要删除的字

       ${变量名##要删除的字}  #表示从左边开始删除最长的匹配要删除的字

       实例:  x="a1e b1e c2 d3 e4"

              echo ${x#*1}  #则将a1删除,输出为 e b1e c2 d3 e4

              echo ${x##*1} #则删除a1e b1,输出为e c2 d3 e4

   [2].从右开始删除

       ${变量名%要删除的字}   #表示从右边开始删除最短的匹配要删除的字

       ${变量名%%要删除的字}  #表示从右边开始删除最长的匹配要删除的字

       实例: x="a1e b1e c2 d3 e4"

             echo ${x%1*} #则删除1e c2 d3 e4，输出为a1e b

             echo ${x%%1*}#则删除1e b1e c2 d3 e4,输出为a

   [3].替换字符

       ${变量名/要替换的字/新字} #将变量值中指定的字替换为新字，只做1次替换

       ${变量名//要替换的字/新字} #将变量值中指定的字替换为新字，做所有替换

       实例: x="a1e b1e c2 d3 e4"

             echo ${x/1/one} #输出aonee b1e c2 d3 e4

             echo ${x//1/one}#输出为aonee bonee c2 d3 e4

(5).设置默认值

   ${变量名:-默认值}  若指定的变量为空或者没有设置，则shell扩展默认值并替换结果，但是指定变量名的值没有更改。

       例如: a=${b:-Val1}  #则变量$a的值为Val1而变量b还是没有设置

   ${变量名:+默认值}  若指定的变量值设置且不为空则shell扩展默认值并替换结果，但是指定的变量值没有改变。

       例如:  b='val1'; a=${b:+val2}  #则$a值为val2而$b值为val1

   ${变量名:=默认值}  若指定的变量为空或者没有设置，则shell扩展默认值并替换结果，且指定变量名的值也更改为默认值。

       实例: a=${b:=val1} #则$a为val1且$b为val1

   ${变量名:?默认值} 若指定的变量为空或者没有设置，则shell扩展默认值并将结果写入标准错误中。可用于判断变量b是否为空，若为空则错误输出指定的信息。

       实例:a=${b:?} #则shell中错误输出-bash: b: error
```

##### shell内置变量
http://blog.csdn.net/gaoming655/article/details/7238695s
http://blog.csdn.net/ljianhui/article/details/43128465
https://www.gnu.org/software/bash/manual/bashref.html#Special-Parameters
http://wiki.jikexueyuan.com/project/linux-command/chap33.html
http://www.runoob.com/linux/linux-shell-passing-arguments.html
http://coney.github.io/2013/07/parse-cli-arguments-in-shell-script/
变量     | 含义
--------|--------
&#36;0      | 脚本名字
&#36;1      | 位置参数 #1
&#36;2 - $9 | 位置参数 #2 - #9
&#36;{10}   | 位置参数 #10
&#36;#      | 位置参数的个数
&#36;&#42;      | 所有的位置参数(作为单个字符串) &#42; (&#42; 必须被引用起来, 否则默认为"&#36;&#64;". )
&#36;&#64;      | 所有的位置参数(每个都作为独立的字符串)
&#36;&#123;#&#42;&#125; | 传递到脚本中的命令行参数的个数
&#36;&#123;#&#64;&#125; | 传递到脚本中的命令行参数的个数
&#36;&#63;      | 命令执行结果的返回值
&#36;&#36;      | 脚本的进程ID(PID)
&#36;-      | 传递到脚本中的标志(使用set)
&#36;_      | 之前命令的最后一个参数
&#36;&#33;      | 运行在后台的最后一个作业的进程ID(PID)

```
$* 与 $@ 区别：

    相同点：都是引用所有参数。
    不同点：只有在双引号中体现出来。假设在脚本运行时写了三个参数 1、2、3，，则 " * " 等价于 "1 2 3"（传递了一个参数），而 "@" 等价于 "1" "2" "3"（传递了三个参数）。
```

##### Shell脚本调试技巧
http://coolshell.cn/articles/1379.html
https://www.ibm.com/developerworks/cn/linux/l-cn-shell-debug/index.html
http://bbs.chinaunix.net/forum.php?mod=viewthread&tid=1356019
```
1. 跟踪脚本执行
bash -x script_name
#! /bin/bash -x

2. 跟踪输入行号
export PS4='+${BASH_SOURCE}:${LINENO}:${FUNCNAME[0]}: '
export PS4='+${FUNCNAME[0]}:${LINENO}: '
export PS4='+${LINENO}: '

3. 调试部分脚本(set command)
#!/bin/bash
echo "Hello $USER,"
set -x
echo "Today is $(date %Y-%m-%d)"
set +x

4. 日志输出控制
_log() {
    if [ "$_DEBUG" == "true" ]; then
        echo 1>&2 "$@"
    fi
}
5.
```

##### Linux的script命令——隐藏在终端的记录器
http://blog.jobbole.com/70563/
```
script是将终端会话制成打印稿的命令。对于想重现终端输入输出历史的人来说，十分管用。而且，这些记录还能被保存或打印。

一般地，我们可以通过在终端上敲入script来启动它。敲击ctrl+d或exit，可以停止记录。你会发现写入记录是发生在停止之后的。
```

##### Grep匹配中括号
https://regexr.com/
https://regex101.com/

http://www.regular-expressions.info/
https://www.gitbook.com/book/luke0922/learnregularexpressionin30minutes/details

https://stackoverflow.com/questions/30044199/how-can-i-match-square-bracket-in-regex-with-grep
https://stackoverflow.com/questions/928072/whats-the-regular-expression-that-matches-a-square-bracket
http://teliute.org/linux/abs-3.9.1/x13673.html
http://www.cnblogs.com/zeweiwu/p/5485711.html
http://wubinary.blog.51cto.com/8570032/1362549
http://bbs.chinaunix.net/thread-3563141-1-1.html
http://kuanghy.github.io/2015/10/26/grep-regex
http://www.infoq.com/cn/news/2011/01/regular-expressions-1
http://www.cftea.com/c/2010/08/5hwu2a5er4wbimkf.asp
https://ask.helplib.com/335235
http://www.cnblogs.com/hustskyking/p/how-regular-expressions-work.html
http://www.jarjar.cn/regular-expression-quick-start/

https://linuxstory.org/grep-regular-expressions/
https://www.ibm.com/support/knowledgecenter/zh/ssw_aix_61/com.ibm.aix.cmds2/grep.htm
https://linux.cn/article-2250-1.html
https://linux.cn/article-5453-1.html
http://www.runoob.com/linux/linux-comm-grep.html
http://www.oracle.com/technetwork/cn/topics/calish-find-096463-zhs.html
https://www.ibm.com/developerworks/community/wikis/home?lang=en#!/wiki/Linux
```
hogan@hogan:~$ echo "fdsl[]" | grep -Eo "[][ a-z]+"
fdsl[]

hogan@hogan:~/ebook$ find . -type f | sed 's/.*\///g' | grep -E "[][}{]"
[www.java1234.com]LINUX SHELL脚本攻略(第二版).pdf
[测试之美].Beautiful.Testing.文字版.pdf
[www.eimhe.com][计算机软件测试（原书第二版）].Cem.Kaner等.pdf
[www.eimhe.com]敏捷软件测试：测试人员与敏捷团队的实践指南_.pdf
[www.eimhe.com]笑傲测试-软件测试流程方法与实施.pdf
[www.eimhe.com]Web入侵安全测试与对策.pdf
[www.eimhe.com]软件测试新技术与实践.pdf
[www.eimhe.com]《软件安全测试艺术》ch01.pdf
[www.eimhe.com]web应用性能测试指南.pdf

```


##### Linux命令备份
```
查找文件名中的特殊字符
hogan@hogan:~/knowledge$ find ./ -name "*
> *"
hogan@hogan:~/knowledge$ find ./ -name "* *"
hogan@hogan:~/Downloads$ find ./ -name "*[\ \
> ]*"

查找window系统不允许的特殊文件名
hogan@hogan:~$ find ./ -name "*[\\\:\*\?\"\<\>\|
> ]*"

中文特殊字符
hogan@hogan:~$ find ./ -name "*[\ \\\:\：\*\?\"\“\”\<\>\《\》\|
> ]*"
中文特殊字符
hogan@hogan:~$ find ./ -name "*[\ \\\/\:\：\*\?\"\“\”\<\>\《\》\|
> ]*"
中文特殊字符
hogan@hogan:~/ebook$ find . -type f | sed 's/.*\///g' | grep -E "[][\\\/\:\*\?\"\<\>\|\`\~)(}{;\'\,\～ （）【】、；：‘’“”，。《》？ -]"

重复文件查找
for file in $(find . -path ./.git -prune -o -print); do if [ -f ${file} ]; then md5sum ${file}; fi done > /tmp/md5.log
cat /tmp/md5.log | sort | uniq -D -w 33

time  find . \! -type d -exec md5sum '{}' ';' | sort | uniq -D -w 33

文件大小排序
du -a -m ebook/ | sort -n

Find查找(忽略test_result目录，然后查找特定后缀名文件)
http://blog.csdn.net/pcyph/article/details/41683383
使用find命令在linux系统中查找文件时，有时需要忽略某些目录，可以使用 -prune 参数来进行过滤。
不过必须注意：要忽略的路径参数要紧跟着搜索的路径之后，否则该参数无法起作用。
find ./ -path "./test_result/*" -prune -o -regextype posix-extended -regex ".*\.(gcno|gcda)" -print

find命令实现tree命令
find . -print | sed -e 's;[^/]*/;|____;g;s;____|; |;g' > structure.txt

find ebook -print | sed -e 's;[^/]*/;│── ;g;s;── │;   │;g' > structure.txt
```

##### time命令查看命令执行时间
http://www.runoob.com/linux/linux-comm-time.html
```
time  find . \! -type d -exec md5sum '{}' ';' | sort | uniq -D -w 33

time命令结果有三行组成：real、user和sys。CPU用时被划分为user和sys两块。

real值表示从程序开始到程序执行结束时所消耗的时间，包括CPU的用时。

user值表示程序本身，以及它所调用的库中的子例程使用的时间。

sys是由程序直接或间接调用的系统调用执行的时间。
```

##### crontab详解
http://linuxtools-rst.readthedocs.io/zh_CN/latest/tool/crontab.html
http://linux.vbird.org/linux_basic/0430cron.php
http://www.cnblogs.com/b028/archive/2011/01/07/1930243.html
```
crontab的文件格式

分 时 日 月 星期 要运行的命令

    第1列分钟0～59
    第2列小时0～23（0表示子夜）
    第3列日1～31
    第4列月1～12
    第5列星期0～7（0和7表示星期天）
    第6列要运行的命令

0,15,30,45 18-06 * * * /bin/echo 'date' > /dev/console

使用实例
实例1：每1分钟执行一次myCommand

* * * * * myCommand

实例2：每小时的第3和第15分钟执行

3,15 * * * * myCommand

实例3：在上午8点到11点的第3和第15分钟执行

3,15 8-11 * * * myCommand

实例4：每隔两天的上午8点到11点的第3和第15分钟执行

3,15 8-11 */2  *  * myCommand

实例5：每周一上午8点到11点的第3和第15分钟执行

3,15 8-11 * * 1 myCommand

实例6：每晚的21:30重启smb

30 21 * * * /etc/init.d/smb restart

实例7：每月1、10、22日的4 : 45重启smb

45 4 1,10,22 * * /etc/init.d/smb restart

实例8：每周六、周日的1 : 10重启smb

10 1 * * 6,0 /etc/init.d/smb restart

实例9：每天18 : 00至23 : 00之间每隔30分钟重启smb

0,30 18-23 * * * /etc/init.d/smb restart

实例10：每星期六的晚上11 : 00 pm重启smb

0 23 * * 6 /etc/init.d/smb restart

实例11：每一小时重启smb

* */1 * * * /etc/init.d/smb restart

实例12：晚上11点到早上7点之间，每隔一小时重启smb

0 23-7 * * * /etc/init.d/smb restart


預設情況下，任何使用者只要不被列入 /etc/cron.deny 當中，那麼他就可以直接下達『 crontab -e 』去編輯自己的例行性命令了！整個過程就如同上面提到的，會進入 vi 的編輯畫面， 然後以一個工作一行來編輯，編輯完畢之後輸入『 :wq 』儲存後離開 vi 就可以了！ 而每項工作 (每行) 的格式都是具有六個欄位，這六個欄位的意義為：
代表意義	分鐘	小時 	日期	月份	週	指令
數字範圍	0-59	0-23	1-31	1-12	0-7 	呀就指令啊

比較有趣的是那個『週』喔！週的數字為 0 或 7 時，都代表『星期天』的意思！另外，還有一些輔助的字符，大概有底下這些：
特殊字符	代表意義
*(星號)	代表任何時刻都接受的意思！舉例來說，範例一內那個日、月、週都是 * ， 就代表著『不論何月、何日的禮拜幾的 12:00 都執行後續指令』的意思！
,(逗號)	代表分隔時段的意思。舉例來說，如果要下達的工作是 3:00 與 6:00 時，就會是：

    0 3,6 * * * command

時間參數還是有五欄，不過第二欄是 3,6 ，代表 3 與 6 都適用！
-(減號)	代表一段時間範圍內，舉例來說， 8 點到 12 點之間的每小時的 20 分都進行一項工作：

    20 8-12 * * * command

仔細看到第二欄變成 8-12 喔！代表 8,9,10,11,12 都適用的意思！
/n(斜線)	那個 n 代表數字，亦即是『每隔 n 單位間隔』的意思，例如每五分鐘進行一次，則：

    */5 * * * * command

很簡單吧！用 * 與 /5 來搭配，也可以寫成 0-59/5 ，相同意思！


hogan@hogan:~$ crontab -l
# Edit this file to introduce tasks to be run by cron.
#
# Each task to run has to be defined through a single line
# indicating with different fields when the task will be run
# and what command to run for the task
#
# To define the time you can provide concrete values for
# minute (m), hour (h), day of month (dom), month (mon),
# and day of week (dow) or use '*' in these fields (for 'any').#
# Notice that tasks will be started based on the cron's system
# daemon's notion of time and timezones.
#
# Output of the crontab jobs (including errors) is sent through
# email to the user the crontab file belongs to (unless redirected).
#
# For example, you can run a backup of all your user accounts
# at 5 a.m every week with:
# 0 5 * * 1 tar -zcf /var/backups/home.tgz /home/
#
# For more information see the manual pages of crontab(5) and cron(8)
#
# m h  dom mon dow   command
0 23 * * 1-5 cd /home/hogan/Documents/Docs/practice/python/stcksql/; /home/hogan/anaconda3/bin/python update_hist_data.py > update.log 2>&1 &
0 0 * * 1-5 cd /home/hogan/Documents/Docs/practice/python/stcksql/; /home/hogan/anaconda3/bin/python stck3.py > stck3.log 2>&1 &
0 1 * * 1-5 cd /home/hogan/Documents/Docs/practice/python/stcksql/; /home/hogan/anaconda3/bin/python get_today_data3.py > get_today_data3.log 2>&1 &


```

##### watch周期性的方式执行给定的指令
```
watch -n 1 -d "netstat -nalt | grep 20000"

while :; do netstat -nal | grep 20000; echo -e "\n\n"; sleep 1; done
```

##### Tcpdump命令行格式
http://www.cnblogs.com/yc_sunniwell/archive/2010/07/05/1771563.html
http://linuxwiki.github.io/NetTools/tcpdump.html
http://blog.csdn.net/hzhsan/article/details/43445787
https://www.ibm.com/support/knowledgecenter/zh/ssw_aix_71/com.ibm.aix.cmds5/tcpdump.htm

http://www.what21.com/article/b_linux_1488875255218.html
https://linux.cn/article-3967-1.html
https://www.cnblogs.com/ggjucheng/archive/2012/01/14/2322659.html
http://blog.csdn.net/hzhsan/article/details/43445787
http://man.linuxde.net/tcpdump
http://cizixs.com/2015/03/12/tcpdump-introduction
http://weibo.com/ttarticle/p/show?id=2309351002704062303971614470
http://blog.csdn.net/lishuhuakai/article/details/73136636
http://pytool.com/2016/01/12/%E5%B8%B8%E7%94%A8%E5%91%BD%E4%BB%A4-2016-01-01-Linux%E5%91%BD%E4%BB%A4-Tcpdump/
```
sudo tcpdump -i lo -x -vv port 20000

sudo tcpdump -i lo tcp port 20000 -X
sudo tcpdump -i lo tcp port 20000 -XX
sudo tcpdump -i lo tcp port 20000 -nSA

只获取syn报文
https://linux.cn/article-3967-1.html

sudo tcpdump -i wlan0 'tcp[13] = 2' -nSA
sudo tcpdump -i wlan0 "tcp[tcpflags] & (tcp-syn) != 0"

tcpdump采用命令行方式，它的命令格式为：
    　　tcpdump [ -adeflnNOpqStvx ] [ -c 数量 ] [ -F 文件名 ]
　　　　　　　　　　[ -i 网络接口 ] [ -r 文件名] [ -s snaplen ]
　　　　　　　　　　[ -T 类型 ] [ -w 文件名 ] [表达式 ]

(1). tcpdump的选项介绍

     -a 　　　将网络地址和广播地址转变成名字；
　　　-d 　　　将匹配信息包的代码以人们能够理解的汇编格式给出；
　　　-dd 　　 将匹配信息包的代码以c语言程序段的格式给出；
　　　-ddd 　　将匹配信息包的代码以十进制的形式给出；
　　　-e 　　　在输出行打印出数据链路层的头部信息；
　　　-f 　　　将外部的Internet地址以数字的形式打印出来；
　　　-l 　　　使标准输出变为缓冲行形式；
　　　-n 　　　不把网络地址转换成名字；
　　　-t 　　　在输出的每一行不打印时间戳；
　　　-v 　　　输出一个稍微详细的信息，例如在ip包中可以包括ttl和服务类型的信息；
　　　-vv 　　 输出详细的报文信息；
　　　-c 　　　在收到指定的包的数目后，tcpdump就会停止；
　　　-F 　　　从指定的文件中读取表达式,忽略其它的表达式；
　　　-i 　　　指定监听的网络接口；
　　　-r 　　　从指定的文件中读取包(这些包一般通过-w选项产生)；
　　　-w 　　　直接将包写入文件中，并不分析和打印出来；
　　　-T 　　　将监听到的包直接解释为指定的类型的报文，常见的类型有rpc （远程过程调用）和snmp（简单网络管理协议；）


来自: http://man.linuxde.net/tcpdump
-a：尝试将网络和广播地址转换成名称；
-c<数据包数目>：收到指定的数据包数目后，就停止进行倾倒操作；
-d：把编译过的数据包编码转换成可阅读的格式，并倾倒到标准输出；
-dd：把编译过的数据包编码转换成C语言的格式，并倾倒到标准输出；
-ddd：把编译过的数据包编码转换成十进制数字的格式，并倾倒到标准输出；
-e：在每列倾倒资料上显示连接层级的文件头；
-f：用数字显示网际网络地址；
-F<表达文件>：指定内含表达方式的文件；
-i<网络界面>：使用指定的网络截面送出数据包；
-l：使用标准输出列的缓冲区；
-n：不把主机的网络地址转换成名字；
-nn：不要解析域名和端口
-N：不列出域名；
-O：不将数据包编码最佳化；
-p：不让网络界面进入混杂模式；
-q ：快速输出，仅列出少数的传输协议信息；
-r<数据包文件>：从指定的文件读取数据包数据；
-s<数据包大小>：设置每个数据包的大小；
-S：用绝对而非相对数值列出TCP关联数；
-t：在每列倾倒资料上不显示时间戳记；
-tt： 在每列倾倒资料上显示未经格式化的时间戳记；
-T<数据包类型>：强制将表达方式所指定的数据包转译成设置的数据包类型；
-v：详细显示指令执行过程；
-vv：更详细显示指令执行过程；
-vvv：更更详细显示指令执行过程；
-x：用十六进制字码列出数据包资料；
-w<数据包文件>：把数据包数据写入指定的文件。
-X：告诉tcpdump命令，需要把协议头和包内容都原原本本的显示出来（tcpdump会以16进制和ASCII的形式显示）;
-XX：同 -X，但同时显示以太网头部。
-A：只使用 ascii 打印报文的全部数据，不要和 -X 一起使用。截取 http 请求的时候可以用 sudo tcpdump -nSA port 80！


简单使用
1. tcpdump -nS
监听所有端口，直接显示 ip 地址。

2. tcpdump -nnvvS
显示更详细的数据报文，包括 tos, ttl, checksum 等。

3. tcpdump -nnvvXS
显示数据报的全部数据信息，用 hex 和 ascii 两列对比输出。


来自: http://blog.csdn.net/lishuhuakai/article/details/73136636
参数 	含义
-A 	以ASCII格式打印出所有分组，通常用来抓取www的网页数据包数据。
-c 	在收到指定的数量的分组后，tcpdump就会停止。
-C 	在将一个原始分组写入文件之前，检查文件当前的大小是否超过了参数file_size 中指定的大小。如果超过了指定大小，则关闭当前文件，然后在打开一个新的文件。参数 file_size 的单位是兆字节（是1,000,000字节，而不是1,048,576字节）。
-d 	将匹配信息包的代码以人们能够理解的汇编格式给出。
-dd 	将匹配信息包的代码以c语言程序段的格式给出。
-ddd 	将匹配信息包的代码以十进制的形式给出。
-D 	打印出系统中所有可以用tcpdump截包的网络接口。
-e 	在输出行打印出数据链路层的头部信息,也就是使用数据链路层的MAC数据包数据来显示.
-f 	将外部的Internet地址以数字的形式打印出来。
-F 	从指定的文件中读取表达式，忽略命令行中给出的表达式。
-i 	指定监听的网络接口。
-l 	使标准输出变为缓冲行形式，可以把数据导出到文件。
-L 	列出网络接口的已知数据链路。
-b 	在数据-链路层上选择协议，包括ip、arp、rarp、ipx都是这一层的。
-n 	不把网络地址转换成名字。
-nn 	不进行端口名称的转换。
-N 	不输出主机名中的域名部分。例如，‘nic.ddn.mil‘只输出’nic‘。
-t 	在输出的每一行不打印时间戳。
-O 	不运行分组分组匹配（packet-matching）代码优化程序。
-P 	不将网络接口设置成混杂模式。
-q 	快速输出。只输出较少的协议信息。
-r 	从指定的文件中读取包(这些包一般通过-w选项产生)。
-S 	将tcp的序列号以绝对值形式输出，而不是相对值。
-s 	从每个分组中读取最开始的snaplen个字节，而不是默认的68个字节。
-T 	将监听到的包直接解释为指定的类型的报文，常见的类型有rpc远程过程调用）和snmp（简单网络管理协议)。
-t 	不在每一行中输出时间戳。
-tt 	在每一行中输出非格式化的时间戳
-ttt 	输出本行和前面一行之间的时间差。
-tttt 	在每一行中输出由date处理的默认格式的时间戳。
-v 	输出一个稍微详细的信息，例如在ip包中可以包括ttl和服务类型的信息。
-vv 	输出详细的报文信息。
-w 	直接将分组写入文件中，而不是不分析并打印出来。
-X 	可以列出16进制以及ASCII的数据包内容,对于监听数据包内容很有用.


来自: http://cizixs.com/2015/03/12/tcpdump-introduction
此外， TCP协议的三次握手过程，第一条就是 SYN 报文，这个可以通过 Flags [S] 看出。下面是常见的 TCP 报文的 Flags:

    [S]： SYN（开始连接）
    [.]: 没有 Flag
    [P]: PSH（推送数据）
    [F]: FIN （结束连接）
    [R]: RST（重置连接）

而第二条数据的 [S.] 表示 SYN-ACK，就是 SYN 报文的应答报文。


来自: http://pytool.com/2016/01/12/%E5%B8%B8%E7%94%A8%E5%91%BD%E4%BB%A4-2016-01-01-Linux%E5%91%BD%E4%BB%A4-Tcpdump/
TCP协议要建立连接要经过3次“握手”，截取的数据包也是从3次握手开始，可以看到前三个包的状态（Flags）分别是：

[S]、[S.]、[.]

首先是客户端向服务端发送一个10位的序号给服务端；服务端收到后把它+1再返回回去；客户端检查返回来的序号是对的，就返回给服务端一个1。根据上面的描述，知道这三个包满足：第一个包的seq+1=第二个包的ack；第三个包的ack=1

连接建立了之后就是具体的数据交互了，tcpdump脚本加-X参数可以通过十六进制和ASCII方式显示出具体的数据内容，这里略过。

TCP协议要断开连接要经过4次“挥手”，上面数据包的最后3条就是挥手的过程。细心的朋友会发现前面说的4次挥手，却只有3个包，这不是笔误。

最后三个包的状态分别是：

[F.]、[F.]、[.]

首先是客户端发一个序号告诉服务器我要断开，服务器说行，服务器发回一个序号，说断开吧，客户端说：“断！”

四次挥手之所以只能看到3个数据包是因为：ACK延迟发送机制。为了提高性能，TCP在收到ACK之后会攒起来而不是立即发送的，在几种情况下才会发送：

1 超过MSS（可以理解为攒得太多了，放不下了）
2 有FIN
3 系统设置为禁用延迟（TCP_NODELAY）

倒数第二条的前面应该还有一个ACK，因为不符合上述3条，所以被延迟（一般是40ms或者200ms）了，等到倒数第二条发出时符合条件了（有FIN）就一块发出来了，所以4次挥手只能看到3个包。如果系统禁用了延迟发送，就会看到4个包了。

```