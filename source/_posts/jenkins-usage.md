---
title: Jenkins使用问题记录
date: 2018-06-08 15:31:51
tags: jenkins
---

<ol>

##### <li> Jenkins强制设置语言为中文 </li>
```
1. 先安装插件：Locale plugin

2. 配置：jienkins->【系统管理】->【系统设置】->【Locale】，输入：zh_CN，并勾上Ignore browser preference and force this language to all users. 这里还有很多语言，比如：en_US等都是国际化标志。
```

<!-- more -->

##### <li> Jenkins允许匿名访问 </li>
```
jienkins->【系统管理】->Configure Global Security, 勾上Allow anonymous read access
```

##### <li> Jenkins权限管理
http://www.cnblogs.com/zz0412/p/jenkins_jj_14.html
```
配置用户权限

点击左侧的系统管理—>Configure Global Security

选择授权策略中的安全矩阵或者项目矩阵授权策略

说明：安全矩阵和项目矩阵授权策略的配置是一模一样的，唯一的区别是项目矩阵授权策略支持在Job的配置页面再次配置授权策略。
```

##### <li> Jenkins的Admin账号权限恢复
http://blog.sina.com.cn/s/blog_56d8ea90010147z3.html
https://www.jianshu.com/p/3dd94ed4cde3
http://www.cnblogs.com/comeonbaby/p/5016021.html
```
找到.jenkins/config.xml文件：
替换为：
1、<authorizationStrategy class="hudson.security.AuthorizationStrategy$Unsecured"/>
这个权限对应“任何用户可以做任何事(没有任何限制)”

2、<authorizationStrategy class="hudson.security.FullControlOnceLoggedInAuthorizationStrategy"/>
这个权限对应“登录用户可以做任何事”

3、<authorizationStrategy class="hudson.security.GlobalMatrixAuthorizationStrategy">
    <permission>hudson.model.Hudson.Administer:test</permission>
    <permission>hudson.scm.SCM.Tag:test</permission>
  </authorizationStrategy>
这个权限对应 test用户可以是管理员、打标签权限。
```


##### <li> 启动 </li>
```
cd ~/Downloads/jenkins/ && java -jar jenkins.war
cd ~/Downloads/jenkins/ && java -Dhudson.model.DirectoryBrowserSupport.CSP= -jar jenkins.war
```

##### <li> 服务管理 </li>
```
关闭jenkins服务
http://localhost:8080/exit

重新启动jenkins服务
http://localhost:8080/restart

重新加载配置信息
http://localhost:8080/reload
```

##### <li> Jenkins插件选择 </li>
```
Email Extension Template Plugin
HTML Publisher plugin
Test Results Analyzer Plugin
xUnit plugin
Locale plugin
Hudson Post build task /构建结束后执行shell命令
Lockable Resources Plugin
```

##### <li> Jenkins Email Extension Template Plugin配置 </li>
jenkins->system management

![extended_email_notification.png](/upload_image/jenkins-usage/extended_email_notification.png)

##### <li> 删除构建历史 </li>
###### 最佳解决方案
如果您单击Manage Hudson /Reload Configuration From Disk，Hudson将重新加载所有构建历史数据。

如果磁盘上的数据被搞砸了，你需要去你的％HUDSON_HOME％\ jobs \< projectname>目录，并按原来的方式恢复构建目录。然后重新加载配置数据。

如果您只是要求如何删除所有的构建历史记录，那么只需少数几个，您可以通过UI逐个删除构建，或者转到％HUDSON_HOME％\ jobs \< projectname>目录并删除所有子目录，它们对应于构建。然后重新启动服务，使更改生效。


###### 次佳解决方案
使用脚本控制台(管理Jenkins>脚本控制台)和类似此脚本的大量删除作业的构建历史记录https://github.com/jenkinsci/jenkins-scripts/blob/master/scriptler/bulkDeleteBuilds.groovy

该脚本假定您只想删除一系列的构建。要删除给定作业的所有构建，请使用(测试)：

// change this variable to match the name of the job whose builds you want to delete
def jobName = "Your Job Name"
def job = Jenkins.instance.getItem(jobName)

job.getBuilds().each { it.delete() }
// uncomment these lines to reset the build number to 1:
//job.nextBuildNumber = 1
//job.save()


###### 第三种解决方案
https://stackoverflow.com/questions/3410141/how-do-i-clear-my-jenkins-hudson-build-history
转到您的Jenkins主页→管理Jenkins→脚本控制台
![manage_jenkins.jpg](/upload_image/jenkins-usage/manage_jenkins.jpg)

在那里运行以下脚本。将copy_folder更改为your project name

码：

def jobName = "copy_folder"
def job = Jenkins.instance.getItem(jobName)
job.getBuilds().each { it.delete() }
job.nextBuildNumber = 1
job.save()


###### 第四种方案
这是另一种选择：使用cURL删除构建。

$ curl -X POST http://jenkins-host.tld:8080/jenkins/job/myJob/[1-56]/doDeleteAll

上面的工作删除了＃1到＃56作业myJob。

如果在Jenkins实例上启用了身份验证，则必须提供用户名和API令牌：

$ curl -u userName:apiToken -X POST http://jenkins-host.tld:8080/jenkins/job/myJob/[1-56]/doDeleteAll

必须从Jenkins的/me /configure页面中提取API令牌。只需点击“显示API令牌…”按钮即可显示用户名和API令牌。

编辑：可能必须在上面的URL中替换doDelete的doDeleteAll，以使其工作，这取决于所使用的Jenkins的配置或版本。


###### 第五种方案
您可以暂时修改项目配置以仅保存最后一个构建，重新加载配置(应该将旧版本删除)，然后将配置设置再次更改为所需的值。


###### 第六种方案
这里是如何删除所有工作的所有工作……使用Jenkins脚本。

def jobs = Jenkins.instance.projects.collect { it }
jobs.each { job -> job.getBuilds().each { it.delete() }}


##### <li> Jenkins Configuration </li>
![conf1.png](/upload_image/jenkins-usage/conf1.png)
![conf2.png](/upload_image/jenkins-usage/conf2.png)
![conf3.png](/upload_image/jenkins-usage/conf3.png)
![conf4.png](/upload_image/jenkins-usage/conf4.png)
![conf5.png](/upload_image/jenkins-usage/conf5.png)
![conf6.png](/upload_image/jenkins-usage/conf6.png)
![conf7.png](/upload_image/jenkins-usage/conf7.png)
![conf8.png](/upload_image/jenkins-usage/conf8.png)
![conf9.png](/upload_image/jenkins-usage/conf9.png)


##### <li> Jenkins调用第三方脚本的console output没有实时打印 </li>
https://gxnotes.com/article/206166.html
https://stackoverflow.com/questions/11631951/jenkins-console-output-not-in-realtime?answertab=votes
http://debugtalk.com/post/make-Jenkins-Console-Output-Colorful/
```
python -u script.py
```

##### <li> 配置备份
https://wiki.jenkins.io/display/JENKINS/Administering+Jenkins#AdministeringJenkins-Moving%2Fcopying%2Frenamingjobs
https://stackoverflow.com/questions/8424228/export-import-jobs-in-jenkins
http://blog.csdn.net/tengdazhang770960436/article/details/62043154
http://www.jianshu.com/p/8762e251c41c

##### <li> Jenkins升级、迁移和备份
http://www.cnblogs.com/zz0412/tag/jenkins/
http://www.cnblogs.com/zz0412/p/jenkins_jj_17.html
http://www.cnblogs.com/LegendOfBFS/p/3487259.html
```
升级Jenkins

Jenkins的开发迭代非常快，每周发布一个开发版本，长期支持版每半年更新一次(ps:大版本更新)。如此频繁的更新，怎么升级呢？

war：下载新版的war文件，替换旧版本war文件。重启即可。

二进制：卸载旧版本，安装新版本即可。

Jenkins程序下载地址：http://mirrors.jenkins-ci.org/

note：升级前，请测试该版本和你本地数据的兼容性。如何测试：将JENKINS_HOME拷贝一份到新的机器，用新版的程序启动。测试对应的插件和配置。
迁移和备份

首先找到JENKINS_HOME(见Jenkins入门系列之——00答疑解惑)，因为Jenkins的所有的数据都是以文件的形式存放在JENKINS_HOME目录中。所以不管是迁移还是备份，只需要操作JENKINS_HOME就行了。

迁移：建议将JENKINS_HOME打包后在拷贝，windows上可以用zip，rar等，Linux上有zip，tar等。然后将打包的文件解压到新的JENKINS_HOME目录就行了。

备份：参考Jenkins进阶系列之——08Jenkins纳入版本控制。如果是临时备份，整个压缩文件就行了。


Jenkins的目录结构

JENKINS_HOME，即为Jenkins的安装目录,可以在Jenkins页面中得到，Jenkins->系统管理-> 系统设置。

JENKINS_HOME
 +- config.xml     (jenkins root configuration)
 +- *.xml          (other site-wide configuration files)
 +- userContent    (files in this directory will be served under your http://server/userContent/)
 +- fingerprints   (stores fingerprint records)
 +- plugins        (stores plugins)
 +- jobs
     +- [JOBNAME]      (sub directory for each job)
         +- config.xml     (job configuration file)
         +- workspace      (working directory for the version control system)
         +- latest         (symbolic link to the last successful build)
         +- builds
             +- [BUILD_ID]     (for each build)
                 +- build.xml      (build result summary)
                 +- log            (log file)
                 +- changelog.xml  (change log)

如果有权限管理，则在HOME目录下还会有users目录。

其中config.xml是Jenkins重要的配置文件。我们都知道Jenkins用于monitor多个build，而jobs这个目录无疑就是存储每个build相关信息的地方。

总的来说，Jenkins目录结构非常直白，简洁。


备份和恢复

备份和恢复非常简单，就是简单的copy Jenkins的目录就好了：

All the settings, build logs, artifact archives are stored under the JENKINS_HOME directory. Simply archive this directory to make a back up. Similarly, restoring the data is just replacing the contents of the JENKINS_HOME directory from a back up.
```
http://www.tinygroup.org/docs/1862982733741657197

首先找到JENKINS_HOME，只要备份了JENKINS_HOME的目录，就可以全部迁移备份了。jenkins不需要连接数据库，没有数据库概念。

1、JENKINS_HOME确认方式：

点击jenkins中的系统设置，然后有一个主目录路径，这个就是JENKINS_HOME。如图：
![jenkins_backup.jpeg](./pictures/jenkins/jenkins_backup.jpeg)

2、迁移：

建议将JENKINS_HOME打包后在拷贝，windows上可以用zip，rar等，Linux上有zip，tar等。然后将打包的文件解压到新的JENKINS_HOME目录就行了。

3、备份：

参考Jenkins进阶系列之——08Jenkins纳入版本控制。如果是临时备份，整个压缩文件就行了。

4、其它：

1）如果jobs 和fingerprints文件太大，可以不需要备份下来，但是里面所有的项目构件就会都没有。只要迁移好以后，直接建两个这个名称的空文件即可。

2）在项目配置中，如果 源码管理--Git中输入账号就报错，可能是git版本过低。如果jenkins是2.12的，那么git需要1.8及以上版本。


##### <li> Email Notification </li>
```
FAQ:
Q. 邮件发送的html报告中，css样式丢失
A: 将html的依赖文件作为附件发送
```

##### <li> .bashrc backup </li>
```
# bash每执行完一条命令，都要显示一个新的提示符，而在显示提示符的同时，会执行保存在环境变量PROMPT_COMMAND里面的命令
PROMPT_COMMAND="history -a; $PROMPT_COMMAND"

# added by Anaconda3 4.4.0 installer
# export PATH="/home/hogan/anaconda3/bin:$PATH"
alias condapython='/home/hogan/anaconda3/bin/python'
alias condapip='/home/hogan/anaconda3/bin/pip'

# user define alias
alias pyshare='python -m SimpleHTTPServer'

# start up jenkins
if [[ ! $(ps -ewwf | grep "java -jar jenkins.war" | grep -v grep) ]]; then
    cd ~/tools/jenkins/
    nohup java -jar jenkins.war > /tmp/jenkins.log 2>&1 &
    cd ~
fi


# Add new path variable for coverage tools
PATH=$PATH:/home/hogan/.jenkins/workspace/XXX_Unit_Test/tools/cov_tools
```
