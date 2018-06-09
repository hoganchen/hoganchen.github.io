---
title: 清除并重建windows 10图标缓存
date: 2018-06-09 14:36:39
tags: Windows
---

图标缓存，即Windows系统为桌面图标所建立的一个图标缓冲区。当桌面图标有所更改的时候系统会将新的图标自动写入缓冲区从而使下次重启电脑时图标不会恢复原样。

电脑系统用久了，随着时间的推移，自己的电脑桌面上会出现大堆图标，如果有时候桌面图标开始无原由的变化，或者桌面上图标都不显示了，都变成了白砖头（就是白色的文件图标），或者任务栏右下角的图标也不正常显示了，那可能就是图标缓存出现了问题，该如何修复这里图标缓存引起的问题呢？

<!-- more -->

#### 清除并重建windows 10图标缓存
##### 方法1
http://www.w10zj.com/Win10xy/Win10yh_971.html
http://www.xitonghe.com/jiaocheng/Windows10-7637.html
```
保存如下代码为icon.bat，并双击运行

cd /d %userprofile%\AppData\Local\Microsoft\Windows\Explorer
taskkill /f /im explorer.exe
attrib -h iconcache_*.db
del iconcache_*.db /a
start explorer
pause
```

##### 方法2
https://www.windows10.pro/ie4uinit-show/
https://www.ithome.com/html/win10/235140.htm
```
Win + R 快捷键调出“运行”对话框，输入如下命令：

ie4uinit -show
```

#### 清除并重建windows 7图标缓存
https://www.nenew.net/win7-iconcache.html
http://www.epinv.com/post/7428.html
```
保存如下代码为icon.bat，并双击运行

rem 关闭Windows外壳程序explorer
taskkill /f /im explorer.exe
rem 清理系统图标缓存数据库
attrib -h -s -r "%userprofile%\AppData\Local\IconCache.db"
del /f "%userprofile%\AppData\Local\IconCache.db"
attrib /s /d -h -s -r "%userprofile%\AppData\Local\Microsoft\Windows\Explorer\*"
del /f "%userprofile%\AppData\Local\Microsoft\Windows\Explorer\thumbcache_32.db"
del /f "%userprofile%\AppData\Local\Microsoft\Windows\Explorer\thumbcache_96.db"
del /f "%userprofile%\AppData\Local\Microsoft\Windows\Explorer\thumbcache_102.db"
del /f "%userprofile%\AppData\Local\Microsoft\Windows\Explorer\thumbcache_256.db"
del /f "%userprofile%\AppData\Local\Microsoft\Windows\Explorer\thumbcache_1024.db"
del /f "%userprofile%\AppData\Local\Microsoft\Windows\Explorer\thumbcache_idx.db"
del /f "%userprofile%\AppData\Local\Microsoft\Windows\Explorer\thumbcache_sr.db"
rem 清理 系统托盘记忆的图标
echo y reg delete "HKEY_CLASSES_ROOT\Local Settings\Software\Microsoft\Windows\CurrentVersion\TrayNotify" /v IconStreams
echo y reg delete "HKEY_CLASSES_ROOT\Local Settings\Software\Microsoft\Windows\CurrentVersion\TrayNotify" /v PastIconsStream
rem 重启Windows外壳程序explorer
start explorer
```
