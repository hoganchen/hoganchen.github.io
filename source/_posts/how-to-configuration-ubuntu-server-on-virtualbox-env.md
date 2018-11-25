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
sudo reboot
```

##### <li> 设置共享文件夹
https://www.cnblogs.com/lidabo/p/5317024.html
http://www.cnblogs.com/linjiqin/p/3615477.html
```
virtualbox设置
设置--共享文件夹--设置目录(固定分配勾选，注意把自动挂载选项去掉)

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

实际配置
cd /mnt
sudo mkdir share
sudo mount -t vboxsf Ubuntu /mnt/share
/etc/fstab添加如下语句
Ubuntu /mnt/share vboxsf rw,gid=100,uid=1000,auto 0 0
```

##### <li> 安装mysql server
```
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
```

##### <li> apt命令参考
```
apt-cache search package 搜索包
apt-cache show package 获取包的相关信息，如说明、大小、版本等
sudo apt-get install package 安装包
sudo apt-get install package - - reinstall 重新安装包
sudo apt-get -f install 修复安装"-f = ——fix-missing"
sudo apt-get remove package 删除包
sudo apt-get remove package - - purge 删除包，包括删除配置文件等
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

