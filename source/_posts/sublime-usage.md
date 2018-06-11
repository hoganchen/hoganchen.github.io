---
title: sublime使用问题记录
date: 2018-06-11 16:31:12
tags: Editor
---

<!-- more -->

<ol>

#### <li> reference links
```
http://feliving.github.io/Sublime-Text-3-Documentation/index.html
http://sublime-text.readthedocs.io/en/latest/index.html
http://lucida.me/blog/sublime-text-complete-guide/
http://zh.lucida.me/blog/sublime-text-complete-guide/
https://www.zhihu.com/question/22904994
https://laravel-china.org/topics/2825
```

#### <li> 安装插件管理器Package Control
进入 Package Control的[官网](https://packagecontrol.io/)，里面有详细的安装教程。

The simplest method of installation is through the Sublime Text console. The console is accessed via the ctrl+` shortcut or the View > Show Console menu. Once open, paste the appropriate Python code for your version of Sublime Text into the console.

```
import urllib.request,os,hashlib; h = 'df21e130d211cfc94d9b0905775a7c0f' + '1e3d39e33b79698005270310898eea76'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
```

等待 Package Control 安装完成。之后使用 Ctrl + Shift + P 打开命令板，输入 PC 应出现 Package Control

优雅使用Sublime Text，插件则是不可缺少的存在；而插件的备份就显得非常的重要（譬如：各平台同步；更换系统/电脑，迅速使用已安装的插件）。这事儿也很简单，只需将Packages（Preferences > Browse Packages）中内容拷贝一份，同步云端即可；至于存储何处，云盘，Github，皆无不可；譬如先前有存一份于sublime_packages，每有所需只要Down下来，替换掉原Packages下内容就好。

#### <li> Sublime Text快捷键
https://www.jianshu.com/p/6185dc5eb507
```
Sublime Text 常用快捷键（MAC 下）

符号说明
    ⌘：command
    ⌃：control
    ⌥：option
    ⇧：shift
    ↩：enter
    ⌫：delete
```

##### 打开/关闭/前往
快捷键		| 功能
--------- | --------------------
⌘⇧N       | 打开一个新的sublime窗口
⌘N        | 新建文件
⌘⇧W       | 关闭sublime，关闭所有文件
⌘W        | 关闭当前文件
⌘P        | 跳转、前往文件、前往项目、命令提示、前往method等等（Goto anything）
⌘⇧T       | 重新打开最近关闭的文件
⌘T        | 前往文件
⌘⌃P       | 前往项目
⌘R        | 前往method，函数切换
⌘⇧R       | 单个文件中进行函数之间的快速切换
⌘⇧P       | 命令提示
⌃G        | 前往行
⌘KB       | 开关侧栏
⌃`        | 打开控制台
⌃-        | 光标跳回上一个位置
⌃⇧-       | 光标恢复位置

##### 编辑
快捷键     | 功能
--------- | --------------------
⌘A        | 全选
⌘L        | 选择行（重复按下将下一行加入选择）
⌘D        | 选择词（重复按下时多重选择相同的词进行多重编辑）如选取过多，可使用⌘U撤消
⌃⌘G       | 选择整个文件中的匹配项
⌃⇧M       | 选择括号的内容
⌘⇧↩       | 在当前行前插入新行
⌘↩        | 在当前行后插入新行
⌃⇧K       | 删除行
⌘KK       | 从光标处删除至行尾
⌘K⌫       | 从光标处删除至行首
⌘⇧D       | 复制（多）行
⌘J        | 合并（多）行
⌘KU       | 改为大写
⌘KL       | 改为小写
⌘C        | 复制
⌘X        | 剪切
⌘V        | 粘贴
⌘/        | 注释
⌘⌥/       | 块注释
⌘Z        | 撤销
⌘Y        | 恢复撤销
⌘⇧V       | 粘贴并自动缩进
⌘⌥V       | 从历史中选择粘贴
⌃M        | 跳转至对应的括号
⌘U        | 软撤销（可撤销光标移动）
⌘⇧U       | 软重做（可重做光标移动）
⌘⇧S       | 保存所有文件
⌘]        | 向右缩进
⌘[        | 向左缩进
⌘⌥T       | 特殊符号集
⌘⇧L       | 将选区转换成多个单行选区

##### 移动

快捷键     | 功能
--------- | --------------------
⌃b        | 前移一个字符位置
⌃f        | 后移一个字符位置
⌃p        | 上移一行
⌃n        | 下移一行

##### 查找/替换
快捷键     | 功能
--------- | --------------------
⌘f        | 查找
⌘⌥f       | 查找并替换
⌘⌥g       | 查找下一个符合当前所选的内容
⌘⌃g       | 查找所有符合当前选择的内容进行多重编辑
⌘⇧F       | 在所有打开的文件中进行查找

##### 拆分窗口/标签页
快捷键       | 功能
---------   | --------------------
⌘⌥[1,2,3,4] | 单列、双列、三列、四列
⌘⌥5         | 网格（4组）
⌃[1,2,3,4]  | 焦点移动到相应的组（分屏编号）
⌃⇧[1,2,3,4] | 将当前文件移动到相应的组（分屏编号）
⌘[1,2,3,4]  | 选择相应的标签页

##### 快捷操作
快捷键       | 功能
---------   | --------------------
⌘⌃上下键     | 两行交换位置
⌘KB         | 显示/隐藏侧边栏
⌘B          | 运行脚本
⌘`          | 多个Sublime实例切换

#### <li> Sublime Text 3 快捷键精华版
https://segmentfault.com/a/1190000002570753
```
Ctrl+Shift+P：打开命令面板
Ctrl+P：搜索项目中的文件
Ctrl+G：跳转到第几行
Ctrl+W：关闭当前打开文件
Ctrl+Shift+W：关闭所有打开文件
Ctrl+Shift+V：粘贴并格式化
Ctrl+D：选择单词，重复可增加选择下一个相同的单词
Ctrl+L：选择行，重复可依次增加选择下一行
Ctrl+Shift+L：选择多行
Ctrl+Shift+Enter：在当前行前插入新行
Ctrl+X：删除当前行
Ctrl+M：跳转到对应括号
Ctrl+U：软撤销，撤销光标位置
Ctrl+J：选择标签内容
Ctrl+F：查找内容
Ctrl+Shift+F：查找并替换
Ctrl+H：替换
Ctrl+R：前往 method
Ctrl+N：新建窗口
Ctrl+K+B：开关侧栏
Ctrl+Shift+M：选中当前括号内容，重复可选着括号本身
Ctrl+F2：设置/删除标记
Ctrl+/：注释当前行
Ctrl+Shift+/：当前位置插入注释
Ctrl+Alt+/：块注释，并Focus到首行，写注释说明用的
Ctrl+Shift+A：选择当前标签前后，修改标签用的
F11：全屏
Shift+F11：全屏免打扰模式，只编辑当前文件
Alt+F3：选择所有相同的词
Alt+.：闭合标签
Alt+Shift+数字：分屏显示
Alt+数字：切换打开第N个文件
Shift+右键拖动：光标多不，用来更改或插入列内容
鼠标的前进后退键可切换Tab文件
按Ctrl，依次点击或选取，可需要编辑的多个位置
按Ctrl+Shift+上下键，可替换行
```

##### 选择类
```
Ctrl+D 选中光标所占的文本，继续操作则会选中下一个相同的文本。

Alt+F3 选中文本按下快捷键，即可一次性选择全部的相同文本进行同时编辑。举个栗子：快速选中并更改所有相同的变量名、函数名等。

Ctrl+L 选中整行，继续操作则继续选择下一行，效果和 Shift+↓ 效果一样。

Ctrl+Shift+L 先选中多行，再按下快捷键，会在每行行尾插入光标，即可同时编辑这些行。

Ctrl+Shift+M 选择括号内的内容（继续选择父括号）。举个栗子：快速选中删除函数中的代码，重写函数体代码或重写括号内里的内容。

Ctrl+M 光标移动至括号内结束或开始的位置。

Ctrl+Enter 在下一行插入新行。举个栗子：即使光标不在行尾，也能快速向下插入一行。

Ctrl+Shift+Enter 在上一行插入新行。举个栗子：即使光标不在行首，也能快速向上插入一行。

Ctrl+Shift+[ 选中代码，按下快捷键，折叠代码。

Ctrl+Shift+] 选中代码，按下快捷键，展开代码。

Ctrl+K+0 展开所有折叠代码。

Ctrl+← 向左单位性地移动光标，快速移动光标。

Ctrl+→ 向右单位性地移动光标，快速移动光标。

shift+↑ 向上选中多行。

shift+↓ 向下选中多行。

Shift+← 向左选中文本。

Shift+→ 向右选中文本。

Ctrl+Shift+← 向左单位性地选中文本。

Ctrl+Shift+→ 向右单位性地选中文本。

Ctrl+Shift+↑ 将光标所在行和上一行代码互换（将光标所在行插入到上一行之前）。

Ctrl+Shift+↓ 将光标所在行和下一行代码互换（将光标所在行插入到下一行之后）。

Ctrl+Alt+↑ 向上添加多行光标，可同时编辑多行。

Ctrl+Alt+↓ 向下添加多行光标，可同时编辑多行。
```

##### 编辑类
```
Ctrl+J 合并选中的多行代码为一行。举个栗子：将多行格式的CSS属性合并为一行。

Ctrl+Shift+D 复制光标所在整行，插入到下一行。

Tab 向右缩进。

Shift+Tab 向左缩进。

Ctrl+K+K 从光标处开始删除代码至行尾。

Ctrl+Shift+K 删除整行。

Ctrl+/ 注释单行。

Ctrl+Shift+/ 注释多行。

Ctrl+K+U 转换大写。

Ctrl+K+L 转换小写。

Ctrl+Z 撤销。

Ctrl+Y 恢复撤销。

Ctrl+U 软撤销，感觉和 Gtrl+Z 一样。

Ctrl+F2 设置书签

Ctrl+T 左右字母互换。

F6 单词检测拼写
```

##### 搜索类
```
Ctrl+F 打开底部搜索框，查找关键字。

Ctrl+shift+F 在文件夹内查找，与普通编辑器不同的地方是sublime允许添加多个文件夹进行查找，略高端，未研究。

Ctrl+P 打开搜索框。举个栗子：1、输入当前项目中的文件名，快速搜索文件，2、输入@和关键字，查找文件中函数名，3、输入：和数字，跳转到文件中该行代码，4、输入#和关键字，查找变量名。

Ctrl+G 打开搜索框，自动带：，输入数字跳转到该行代码。举个栗子：在页面代码比较长的文件中快速定位。

Ctrl+R 打开搜索框，自动带@，输入关键字，查找文件中的函数名。举个栗子：在函数较多的页面快速查找某个函数。

Ctrl+： 打开搜索框，自动带#，输入关键字，查找文件中的变量名、属性名等。

Ctrl+Shift+P 打开命令框。场景栗子：打开命名框，输入关键字，调用sublime text或插件的功能，例如使用package安装插件。

Esc 退出光标多行选择，退出搜索框，命令框等。
```

##### 显示类
```
Ctrl+Tab 按文件浏览过的顺序，切换当前窗口的标签页。

Ctrl+PageDown 向左切换当前窗口的标签页。

Ctrl+PageUp 向右切换当前窗口的标签页。

Alt+Shift+1 窗口分屏，恢复默认1屏（非小键盘的数字）

Alt+Shift+2 左右分屏-2列

Alt+Shift+3 左右分屏-3列

Alt+Shift+4 左右分屏-4列

Alt+Shift+5 等分4屏

Alt+Shift+8 垂直分屏-2屏

Alt+Shift+9 垂直分屏-3屏

Ctrl+K+B 开启/关闭侧边栏。

F11 全屏模式

Shift+F11 免打扰模式

update

Ctrl+k+2 折叠注释和方法

Ctrl+k+3 折叠if

Ctrl+k+4 折叠switch
```

#### <li> Sublime Text常用快捷键
https://gist.github.com/xingfuqiu/6171892
```
Ctrl+Shift+P：打开命令面板
Ctrl+P：搜索项目中的文件
Ctrl+G：跳转到第几行
Ctrl+W：关闭当前打开文件
Ctrl+Shift+W：关闭所有打开文件
Ctrl+Shift+V：粘贴并格式化
Ctrl+D：选择单词，重复可增加选择下一个相同的单词
Ctrl+L：选择行，重复可依次增加选择下一行
Ctrl+Shift+L：选择多行
Ctrl+Shift+Enter：在当前行前插入新行
Ctrl+X：删除当前行
Ctrl+M：跳转到对应括号
Ctrl+U：软撤销，撤销光标位置
Ctrl+J：选择标签内容
Ctrl+F：查找内容
Ctrl+Shift+F：查找并替换
Ctrl+H：替换
Ctrl+R：前往 method
Ctrl+N：新建窗口
Ctrl+K+B：开关侧栏
Ctrl+Shift+M：选中当前括号内容，重复可选着括号本身
Ctrl+F2：设置/删除标记
Ctrl+/：注释当前行
Ctrl+Shift+/：当前位置插入注释
Ctrl+Alt+/：块注释，并Focus到首行，写注释说明用的
Ctrl+Shift+A：选择当前标签前后，修改标签用的
F11：全屏
Shift+F11：全屏免打扰模式，只编辑当前文件
Alt+F3：选择所有相同的词
Alt+.：闭合标签
Alt+Shift+数字：分屏显示
Alt+数字：切换打开第N个文件
Shift+右键拖动：光标多不，用来更改或插入列内容
鼠标的前进后退键可切换Tab文件
按Ctrl，依次点击或选取，可需要编辑的多个位置
按Ctrl+Shift+上下键，可替换行
```

#### <li> Sublime Text 常用快捷键整理
http://kuanghy.github.io/2015/11/23/sublimetext-hotkey
```
插入

    Ctrl+Enter

在下一行插入新行。即使光标不在行尾，也能快速向下插入一行。

    Ctrl+Shift+Enter

在上一行插入新行。即使光标不在行首，也能快速向上插入一行。

    Ctrl+Shift+D

复制光标所在整行，插入到下一行。即先将光标所在行复制，然后再插入到光标所在的下一行。
编辑

    Ctrl+J

合并选中的多行代码为一行。例如：将多行格式的CSS属性合并为一行。

    Ctrl+Shift+V

粘贴并保持缩进。

    Alt+Shift+W

使用标签包裹一行，Web开发利器。

    Ctrl+Shift+;

移除与光标所在位置相关的父标签。对清除标记很有帮助。

    Ctrl + 左键点击

按Ctrl，依次点击或选取，可需要编辑的多个位置。

    Ctrl+T 左右字母互换。

Esc 退出光标多行选择，退出搜索框，命令框等。

    Ctrl+K+B

开启/关闭侧边栏。
选择

    Ctrl+D

选中光标所占的文本，继续操作则会选中下一个相同的文本。

    Alt+F3

选中文本按下快捷键，即可一次性选择全部的相同文本进行同时编辑。例如：快速选中并更改所有相同的变量名、函数名等。

    Ctrl+L

选中整行，继续操作则继续选择下一行，效果和 Shift+↓ 效果一样。

    Ctrl+Shift+L

先选中多行，再按下快捷键，会在每行行尾插入光标，即可同时编辑这些行。

    Ctrl+Shift+M

选择括号内的内容（继续选择父括号）。例如：快速选中删除函数中的代码，重写函数体代码或重写括号内里的内容。

    shift+↑

向上选中多行。

    shift+↓

向下选中多行。

    Shift+←

向左选中文本。

    Shift+→

向右选中文本。

    Ctrl+Shift+←

向左单位性地选中文本。

    Ctrl+Shift+→

向右单位性地选中文本。
移动

    Ctrl+M

光标移动至括号内结束或开始的位置。

    Ctrl+←

向左单位性地移动光标，快速移动光标。

    Ctrl+→

向右单位性地移动光标，快速移动光标。

    Ctrl+G

输入数字跳转到指定行。与 Ctrl + P 输人 ： 再输入数字一样的功能。
折叠

    Ctrl+Shift+[

选中代码，按下快捷键，折叠代码。

    Ctrl+Shift+]

选中代码，按下快捷键，展开代码。

    Ctrl+K+0

展开所有折叠代码。
缩进

    Tab

向右缩进。

    Shift+Tab

向左缩进。

    Ctrl+]

向右缩进。

    Ctrl+[

向左不缩进。
注释

    Ctrl+/

注释单行。

    Ctrl+Shift+/

注释多行。
删除

    Ctrl+K+K

从光标处开始删除代码至行尾。

    Ctrl+Shift+K

删除整行。
撤消

    Ctrl+Z

撤销。

    Ctrl+Y

恢复撤销。

    Ctrl+U

软撤销，撤销光标位置。
大小写转换

    Ctrl+K+U

转换大写。

    Ctrl+K+L

转换小写。
查找

    Ctrl+F

打开底部搜索框，查找关键字。如果先选中文本再按快捷键，则自动开始查找。

    Ctrl+H

查找并替换。

    Ctrl+shift+F

在文件夹内查找，允许添加多个文件夹进行查找，同时支持替换。

    Ctrl+P

打开搜索框。该搜索框有强大的搜索功能：

1、输入当前项目中的文件名，快速搜索文件，
2、输入@和关键字，查找文件中函数名，
3、输入：和数字，跳转到文件中该行代码，
4、输入#和关键字，查找变量名。

    Ctrl+R

打开搜索框，自动带@，输入关键字，查找文件中的函数名。举个栗子：在函数较多的页面快速查找某个函数。

    Ctrl+：

打开搜索框，自动带#，输入关键字，查找文件中的变量名、属性名等。

    Ctrl+Shift+P

打开命令框。场景栗子：打开命名框，输入关键字，调用sublime text或插件的功能，例如使用package安装插件。
分屏

    Alt+Shift+1

窗口分屏，恢复默认1屏（非小键盘的数字）。

    Alt+Shift+2

左右分屏-2列。

    Alt+Shift+3

左右分屏-3列。

    Alt+Shift+4

左右分屏-4列。

    Alt+Shift+5

等分4屏。

    Alt+Shift+8

垂直分屏-2屏。

    Alt+Shift+9

垂直分屏-3屏。
```

#### <li> sublime text修改换行符为linux风格
```
文件的格式控制可以Perference->Setting-*中找到。设置对象是default_line_ending，这个参数有三 个可用选
项：system,windows,unix，system是根据当前系统情况设置，windows使用的CRLF，unix使用的是 LF。按你的情况，应该在Setting-User中设置"default_line_ending":"unix"就可以解决这个问题。
```

#### <li> Perferences.sublime-settings -- User备份
```
{
    "file_exclude_patterns":
    [
        "*.pyc",
        "*.pyo",
        "*.exe",
        "*.dll",
        "*.obj",
        "*.o",
        "*.a",
        "*.lib",
        "*.so",
        "*.dylib",
        "*.ncb",
        "*.sdf",
        "*.suo",
        "*.pdb",
        "*.idb",
        ".DS_Store",
        "*.class",
        "*.psd",
        "*.db",
        "*.sublime-workspace"
    ],
    "font_face": "Courier New",
    "font_size": 18,
    "highlight_line": true,
    "ignored_packages":
    [
        "Vintage"
    ],
    "translate_tabs_to_spaces": true,
    "trim_trailing_white_space_on_save": true
}


{
	"font_size": 14,
	"highlight_line": true,
	"ignored_packages":
	[
		"Vintage"
	],
	"translate_tabs_to_spaces": true,
	"trim_trailing_white_space_on_save": true
}
```

#### <li> Sublime ShortCut

http://www.techug.com/post/sublime-text-complete-guide.html
http://www.cocoachina.com/programmer/20150715/12550.html
http://sublime-undocs-zh.readthedocs.io/en/latest/
http://feliving.github.io/Sublime-Text-3-Documentation/index.html
https://www.w3cschool.cn/sublimetext3/

http://blog.jobbole.com/82527/
https://segmentfault.com/a/1190000002570753
http://jinfang.life/posts/e4aa08c5/
https://github.com/liveNo/Sublime-Tutorial
https://www.zhihu.com/question/24896283?rf=19976788
https://shunnien.github.io/2016/02/23/sublimetext-shortcuts/
http://www.daqianduan.com/4820.html
http://www.cnblogs.com/lanxuezaipiao/p/4151095.html
http://luopuya.github.io/2014/03/26/Sublime%20Text%203%20%E5%B8%B8%E7%94%A8%E5%BF%AB%E6%8D%B7%E9%94%AE/
http://blog.csdn.net/cywosp/article/details/31791881
http://blog.csdn.net/txz_gray/article/details/70516912

##### <li> 多行快速选择文本

    Ctrl+D：选中光标所占的文本，继续操作则会选中下一个相同的文本。（非常实用）
    Ctrl-K, Ctrl-D：把当前选中所占文本的光标，跳转到下一个相同文本。（配合Ctrl+D很实用）
    Ctrl+D选择当前光标所在的词并高亮该词所有出现的位置，再次Ctrl+D选择该词出现的下一个位置，在多重选词的过程中，使用Ctrl+K进行跳过，使用Ctrl+U进行回退，使用Esc退出多重编辑。
    Alt-F3：一次性选中(当前选中的文本）相同的文本。等于多次实用Ctrl+D。（部分修改情况下慎用，Mac下:Ctrl-Cmd-G）

##### <li> 行操作
###### <li> 选择类

    Ctrl+L：选择光标当前行，重复可依次增加选择下一行，若多有行光标，则第一次选择多行。
    Ctrl+J ：将光标的下一行，合并到光标当前行。若选择多行，则合并选择的多行为一行，同时再合并当前行的下一行。

###### <li> 操作类
	Shift+鼠标右键： 列模式
    Ctrl+G：跳转到第几行。
    Ctrl+Shift+L：（前提先选中多行）会在每行行尾插入光标，即可同时编辑这些行。有时我们需要对一片区域的所有行进行同时编辑，Ctrl + Shift + L可以将当前选中区域打散，然后进行同时编辑
    Ctrl + J： 把当前选中区域合并为一行
    Ctrl+Shift+↑ ↓： 当前行或当前选中行与上下行互换位置。
    Ctrl+Enter： 在当前光标的下一行插入新行并跳转光标。
    Ctrl+Shift+Enter：在当前光标的在上一行插入新行并跳转光标。
    Ctrl+Shift+D： 复制光标或所选区所在的整行，插入到下一行。
    Ctrl+Shift+T： 快速恢复关闭的标签页

###### <li> 删除类

    Ctrl+Shift+K：删除整行，没有空白符。
    Ctrl+k+k： 从光标处至行尾删除。
    Ctrl+K+Backspace：从光标处至行首删除。

###### <li> 注释

    Ctrl+Shift+/：根据选择进行多行注释。
    Ctrl+/：单行注释。

###### <li> 缩进

    Ctrl+[ ]：左右缩进当光标或光标所在的行。
    Tab： 向右缩进。
    Shift+Tab：向左缩进。

###### <li> 代码块

    Ctrl+Shift+[：选中代码，按下快捷键，折叠代码。
    Ctrl+Shift+]：选中代码，按下快捷键，展开代码。
    Ctrl+K+0： 展开所有折叠代码。
    Ctrl+K+T：折叠所有html的属性。（非常好用，看html结构的时候）
    Ctrl+M：跳转到对应括号。
    Ctrl+Shift+J：快速选择同级的内容，同级内容=兄弟内容。

###### <li> 编辑

    Ctrl+Y：恢复撤销。
    Ctrl+Z： 撤销。
    Ctrl+K+U：转换光标最近单词，或所选区域大写。
    Ctrl+K+L：转换光标最近单词，或所选区域小写。

###### <li> 查找

    Ctrl+F:在当前页面中查找
    Ctrl+shift+F：高级查找，在文件夹内查找。
    Ctrl+P：打开多功能搜索框。
    　　1.输入当前项目中的文件名，快速搜索文件。
    　　2.输入@和关键字，查找文件中函数名。（Ctrl+R）
    　　3.输入：和数字，跳转到文件中该行代码。（Ctrl+G）
    　　4.输入#和关键字，查找变量名。 （Ctrl+：）
    Ctrl+G：打开搜索框，自动带：，输入数字跳转到该行代码。
    Ctrl+R：打开搜索框，自动带@，输入关键字，查找文件中的函数名。
    Ctrl+; ：打开搜索框，自动带#，输入关键字，查找文件中的变量名、属性名等。

###### <li> 窗口

    Alt+Shift+1：窗口分屏，恢复默认1屏（非小键盘的数字）
    Alt+Shift+2：左右分屏-2列。
    Alt+Shift+3：左右分屏-3列。
    Alt+Shift+4：左右分屏-4列。
    Alt+Shift+5：等分4屏。
    Alt+Shift+8：垂直分屏-2屏。
    Alt+Shift+9：垂直分屏-3屏。
    Ctrl+K,Ctirl+B：开启/关闭侧边栏。
    Ctrl+N：新建空面板。
    Ctrl+Shift+N：在新建窗口中，创建空面板。
    Ctrl+Tab：从左往右，切换当前窗口的标签页。
    Ctrl+Shift+Tab：从右往左，切换当前窗口的标签页。
    Ctrl+W：关闭当前标签，当窗口内没有标签时会关闭该窗口
    Ctrl+Shift+T：恢复刚刚关闭的标签

###### <li> 高级

    Ctrl+Shift+Space：选择当前光标最小块的代码。（非常好用）
    Ctrl+Shift+'：emmet插件下，这个可以在html中，选择光标最近的一组闭合标签。修改标签非常方便。
    Ctrl+U： 软撤销，撤销快捷键的一些动作，比如撤销选中。（若快捷键冲突不起效果，请自定义快捷键）