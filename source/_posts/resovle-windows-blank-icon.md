---
title: 解决Windows 10任务栏某些程序图标空白问题
date: 2018-06-09 10:20:20
tags: Windows
---

#### 问题：电脑任务栏锁定的某程序图标显示为白色，而其它图标显示正常。
![black-icon-01.png](/upload_image/windows-black-icon/black-icon-01.png)

<!-- more -->

#### 解决：
https://blog.csdn.net/DearMorning/article/details/79472245
##### Step 1:
Win + R快捷键弹出运行窗口，输入%APPDATA%\Microsoft\Internet Explorer\Quick Launch\User Pinned\TaskBar
![black-icon-02.png](/upload_image/windows-black-icon/black-icon-02.png)

##### step 2:
在弹出的TaskBar文件夹中，发现没有图标显示异常的快捷方式。将该程序的快捷方式放入到TaskBar文件夹
![black-icon-03.png](/upload_image/windows-black-icon/black-icon-03.png)

##### step 3:
重新运行该程序，若未恢复图标，在任务栏上右键点击【固定到任务栏】再取消固定，可以发现图标显示正常。

##### step 4:
如上述操作未能解决问题，备份并删除ImplicitAppShortcuts目录，然后重新启动。
![black-icon-04.png](/upload_image/windows-black-icon/black-icon-04.png)
