---
title: Virtualbox中安装Ubuntu Server版本
date: 2018-11-25 23:53:06
tags: Ubuntu
---

<ol>

##### <li> 配置ssh访问
```
virtualbox设置
设置--网络--端口转发--端口转发规则
ssh tcp 127.0.0.1 22 10.0.2.15 22

如果是多台虚拟机，则修改端口转发规则为
ssh tcp 127.0.0.1 22 10.0.2.15 22
ssh tcp 127.0.0.1 2222 10.0.2.15 22
ssh tcp 127.0.0.1 2223 10.0.2.15 22
ssh tcp 127.0.0.1 2224 10.0.2.15 22
......

putty
hogan@127.0.0.1 22

ubuntu免输入密码
cd ~
mkdir .ssh
cd .ssh
vi authorized_keys
```

<!-- more -->

##### <li> 配置sudo免密码
https://askubuntu.com/questions/147241/execute-sudo-without-password
https://blog.csdn.net/wxqee/article/details/72718869
https://www.linuxidc.com/Linux/2016-12/139018.htm
https://blog.csdn.net/javensun/article/details/7582341
https://www.jb51.net/os/Ubuntu/63313.html
```
sudo visudo

# 在文件末尾添加如下语句，USER替换为不需要输入密码的用户名
USER ALL=(ALL) NOPASSWD: ALL

# 上面的命令其实是修改了/etc/sudoers文件，所以也可以直接编辑这个文件
sudo vi /etc/sudoers
添加如下语句
USER ALL=(ALL) NOPASSWD: ALL

hogan@ubuntu:/etc$ cat /etc/sudoers
cat: /etc/sudoers: Permission denied
hogan@ubuntu:/etc$ sudo cat /etc/sudoers
#
# This file MUST be edited with the 'visudo' command as root.
#
# Please consider adding local content in /etc/sudoers.d/ instead of
# directly modifying this file.
#
# See the man page for details on how to write a sudoers file.
#
Defaults        env_reset
Defaults        mail_badpass
Defaults        secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"

# Host alias specification

# User alias specification

# Cmnd alias specification

# User privilege specification
root    ALL=(ALL:ALL) ALL

# Members of the admin group may gain root privileges
%admin ALL=(ALL) ALL

# Allow members of group sudo to execute any command
%sudo   ALL=(ALL:ALL) ALL

# See sudoers(5) for more information on "#include" directives:

#includedir /etc/sudoers.d
hogan ALL=(ALL) NOPASSWD: ALL
```

##### <li> 备份并替换ubuntu源
```
cd /etc/apt/
sudo cp sources.list sources.list.orig
sudo vi sources.list
查找所有cn.archive.ubuntu.com，并替换为mirrors.163.com
:%s/cn.archive.ubuntu.com/mirrors.163.com/g
```

##### <li> 更新并安装build-essential
```
sudo apt-get update
sudo apt-get install build-essential
```

##### <li> 安装virtualbox增强工具
```
cd /mnt/
sudo mkdir cdrom
sudo mount /dev/cdrom /mnt/cdrom

cd cdrom
sudo bash VBoxLinuxAdditions.run
关机并设置共享目录
sudo halt -p
```

##### <li> 设置共享文件夹
https://www.cnblogs.com/lidabo/p/5317024.html
http://www.cnblogs.com/linjiqin/p/3615477.html
```
virtualbox设置
设置--共享文件夹--设置目录(固定分配勾选，注意把自动挂载选项去掉，Ubuntu不能勾选自动挂载，Windows可以勾选自动挂载)

ubuntu设置
cd /mnt
sudo mkdir shared
sudo mount -t vboxsf share /mnt/shared

其中"share"是之前创建的共享文件夹的名字。OK，现在Ubuntu和主机可以互传文件了。

要想自动挂载的话，可以在/etc/fstab中添加一项
share /mnt/shared vboxsf rw,gid=100,uid=1000,auto 0 0

卸载的话使用下面的命令：
sudo umount -f /mnt/shared

注意事项
共享文件夹的名称千万不要和挂载点的名称相同。比如，上面的挂载点是/mnt/shared，如果共享文件夹的名字也是shared的话，在挂载的时候就会出现如下的错误信息：/sbin/mount.vboxsf: mounting failed with the error: Protocol error

自用Ubuntu上的实际配置
cd /mnt
sudo mkdir share
sudo mount -t vboxsf Ubuntu /mnt/share

sudo vi /etc/fstab
/etc/fstab添加如下语句
Ubuntu /mnt/share vboxsf rw,gid=100,uid=1000,auto 0 0

*****20200621 update*****
在实际使用中，因为系统调用fstab的时候，Virtualbox的共享目录的模块还没有加载，所以每次加载都会失败
以下是ubuntu 16上实际使用方式
1. 设置--共享文件夹--设置目录(固定分配勾选，注意把自动挂载选项去掉，Ubuntu不能勾选自动挂载，Ubuntu不能勾选自动挂载，Ubuntu不能勾选自动挂载，重要的事说三遍。。。

2. 修改/etc/rc.local，把mount的语句加在rc.local中，rc.local是最后执行的开机启动任务，所以这时候virtualbox的相关模块已启动，不会导致加载失败的问题，值得注意的是，一定要把virtualbox设置中的自动挂载去掉
hogan@ubuntu:~$ cat /etc/rc.local
#!/bin/sh -e
#
# rc.local
#
# This script is executed at the end of each multiuser runlevel.
# Make sure that the script will "exit 0" on success or any other
# value on error.
#
# In order to enable or disable this script just change the execution
# bits.
#
# By default this script does nothing.

mount -t vboxsf ubuntu /mnt/share
mount -t vboxsf codes /mnt/repository
exit 0

```

##### <li> 安装mysql server
```
由于系统源中的mysql版本过低，所以需要先去mysql官网下载apt源的deb包

1. 下载mysql的Ubuntu版本的deb包
https://dev.mysql.com/downloads/mysql/

2. 安装deb包，并根据需求选择mysql的版本和附加包，
sudo dpkg -i mysql-apt-config_0.8.11-1_all.deb

3. 在ubuntu 14.04.5安装mysql apt源的deb包出错的解决方法
hogan@ubuntu:/mnt/share/tools$ sudo dpkg -i mysql-apt-config_0.8.11-1_all.deb
dpkg-deb: error: archive 'mysql-apt-config_0.8.11-1_all.deb' has premature member 'control.tar.xz' before 'control.tar.gz', giving up
dpkg: error processing archive mysql-apt-config_0.8.11-1_all.deb (--install):
 subprocess dpkg-deb --control returned error exit status 2
Errors were encountered while processing:
 mysql-apt-config_0.8.11-1_all.deb

解决方法:
https://askubuntu.com/questions/982748/dpkg-error-when-installing-nmap
Removing APT cache
hogan@ubuntu:/mnt/share/tools$ sudo apt-get clean && sudo apt-get autoclean
Updating APT
hogan@ubuntu:/mnt/share/tools$ sudo apt-get update
If there's available software to upgrade then run
hogan@ubuntu:/mnt/share/tools$ sudo apt-get upgrade
再次安装deb包
sudo dpkg -i mysql-apt-config_0.8.11-1_all.deb

4. 更新源并安装mysql
sudo apt-get update
sudo apt-cache search mysql | grep server
sudo apt-cache search mysql-server
sudo apt-get install mysql-server
```

##### <li> .bashrc设置
```
alias condapython='~/anaconda3/bin/python'
alias condapip='~/anaconda3/bin/pip'
alias conda='~/anaconda3/bin/conda'

alias toshare='cd /mnt/share'
alias updatemysql='cd /mnt/share/codes/python/stcksql; condapython update_mysql_data.py'

*****20200621 update*****
# go env
export GOROOT=~/go
export GOPATH=$HOME/gopath
export PATH=$PATH:$GOROOT/bin:$GOPATH/bin

# user alias
alias torepo='cd /mnt/repository'
alias tocode='cd /mnt/repository/github/codes'
alias tostck='cd /mnt/repository/github/codes/python/stcksql'
alias updata='cd ~/bin; nohup bash mysql_update > /dev/null 2>&1 &'

# added by Anaconda3 installer
export PATH="/home/hogan/anaconda3/bin:$PATH"

```

##### <li> mysql_update
```
hogan@ubuntu:~$ cat bin/mysql_update
#!/bin/bash

cd /mnt/repository/github/codes/python/stcksql

# ~/anaconda3/bin/python update_hist_data.py > update_hist_data_`date "+%Y%m%d%H%M%S"`.log 2>&1
~/anaconda3/bin/python update_hist_data.py > update_hist_data.log 2>&1
sleep 10

# ~/anaconda3/bin/python update_extend_hist_data.py > update_extend_hist_data_`date "+%Y%m%d%H%M%S"`.log 2>&1
~/anaconda3/bin/python update_extend_hist_data.py > update_extend_hist_data.log 2>&1

```

##### <li> 桥接网络设置
```
不知道是否路由器的原因，桥接网络有时候不能获取IP地址，但是这时候重启Host电脑，然后再打开虚拟机启动guest，就能够获取IP了，如果还不行，可以在桥接网络设置，混杂模式切换试试
```

##### <li> Ubuntu Server只安装安全更新(未验证)
https://linux.cn/article-8060-1.html
https://yq.aliyun.com/articles/113684
https://blog.ghostry.cn/server/753.html
https://ox0spy.github.io/post/configuration/debian-ubuntu-automatic-security-updates/
http://blog.topspeedsnail.com/archives/10299
https://www.howtoing.com/install-security-updates-ubuntu-debian/
https://www.cplusplus.me/2443.html

##### <li> apt命令参考
```
apt-cache search package 搜索包
apt-cache show package 获取包的相关信息，如说明、大小、版本等
sudo apt-get install package 安装包
sudo apt-get install package - - reinstall 重新安装包
sudo apt-get -f install 修复安装"-f = ——fix-missing"
sudo apt-get remove package 删除包
sudo apt-get remove package - - purge 删除包，包括删除配置文件等
sudo apt-get purge package 删除包，包括删除配置文件等，与上条命令等价
sudo apt-get autoremove 卸载所有自动安装且不再使用的软件包
sudo apt-get update 更新源
sudo apt-get upgrade 更新已安装的包
sudo apt-get dist-upgrade 升级系统
sudo apt-get dselect-upgrade 使用 dselect 升级
apt-cache depends package 了解使用依赖
apt-cache rdepends package 是查看该包被哪些包依赖
sudo apt-get build-dep package 安装相关的编译环境
apt-get source package 下载该包的源代码
sudo apt-get clean && sudo apt-get autoclean 清理无用的包
sudo apt-get check 检查是否有损坏的依赖 
```

