---
title: Git使用问题记录
date: 2018-06-11 10:12:58
tags: Git
---

<ol>

#### GIT是什么
https://github.com/pubyun/testing
Git(读音为/gɪt/。)是一个开源的分布式版本控制系统，可以有效、高速的处理从很小到非常大的项目版本管理。Git 是 Linus Torvalds 为了帮助管理 Linux 内核开发而开发的一个开放源码的版本控制软件。
Torvalds 开始着手开发 Git 是为了作为一种过渡方案来替代 BitKeeper，后者之前一直是 Linux 内核开发人员在全球使用的主要源代码工具。开放源码社区中的有些人觉得BitKeeper 的许可证并不适合开放源码社区的工作，因此 Torvalds 决定着手研究许可证更为灵活的版本控制系统。尽管最初 Git 的开发是为了辅助 Linux 内核开发的过程，但是我们已经发现在很多其他自由软件项目中也使用了 Git。例如 很多 Freedesktop 的项目迁移到了 Git 上。

<!-- more -->

##### 全局用户信息配置
```
git config --global user.email "hogan.chen@ymail.com"
git config --global user.name "hogan chen"

设置git记住密码，这样保存的密码是明文的，保存在用户目录~的.git-credentials文件中
git config credential.helper store

设置代理
git config --global http.proxy http://173.17.40.143:1080
git config --global https.proxy https://173.17.40.143:1080
```

##### 非全局用户信息配置
```
git config user.email "hogan.chen@ymail.com"
git config user.name "hogan chen"
```

##### 检查配置信息
https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%88%9D%E6%AC%A1%E8%BF%90%E8%A1%8C-Git-%E5%89%8D%E7%9A%84%E9%85%8D%E7%BD%AE
https://git-scm.com/book/zh/v2/%E8%87%AA%E5%AE%9A%E4%B9%89-Git-%E9%85%8D%E7%BD%AE-Git
```
git config --list

git config -l 查看config配置，用 git config --global -l 查看全局设置。
```

##### Git快捷方式添加
https://peter517.github.io/2015/08/10/Git%E4%B8%AA%E4%BA%BA%E9%85%8D%E7%BD%AE/
https://www.jianshu.com/p/e5ed3a29a3c4

1. 通过git命令添加
```
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.ci commit
git config --global alias.br branch
```

2. 直接修改~/.gitconfig
```
hogan@ubuntu:~$ cat .gitconfig
[alias]
        st = status
        co = checkout
        ci = commit
        br = branch
```

3. 添加.bashrc的alias
```
alias gitcommit="git commit -m"
alias gitlog="git log"
alias gitshow="git show" #查看修改内容
alias gitcat="git cat-file"
alias gitloggraph="git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset'" #以图形方式显示提交日志
alias gitinfo="git remote show origin" #查看仓库信息
alias gitshortlog="git shortlog --since=1.day.ago" #查看最近一天的提交日志
alias gitweekshortlog="git shortlog --since=1.week.ago --author='pengjun' | grep -v Merge | uniq" #查看最近一周pengjun的提交日志
alias gitfilelog="git log --follow -p" #查看文件的修改日志
```

##### Git ssh访问设置
```
$ ssh-keygen -t rsa -C "hogan.chen@ymail.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/hogan/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /c/Users/hogan/.ssh/id_rsa.
Your public key has been saved in /c/Users/hogan/.ssh/id_rsa.pub.
The key fingerprint is:
......
```

##### Github ssh和https访问切换
https://www.sheng00.com/2057.html
https://help.github.com/articles/connecting-to-github-with-ssh/
```
1. Generating a new SSH key
ssh-keygen -t rsa -b 4096 -C "hogan.chen@ymail.com"

2. Adding a new SSH key to your GitHub account
https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/

3. Testing your SSH connection
ssh -T git@github.com

4. change the https to ssh
4.1 change the config file directly
hogan@ubuntu:~/hoganchen.github.io/.git$ cat config
[core]
        repositoryformatversion = 0
        filemode = true
        bare = false
        logallrefupdates = true
[remote "origin"]
        # url = https://github.com/hoganchen/hoganchen.github.io.git
        url = git@github.com:hoganchen/hoganchen.github.io.git
        fetch = +refs/heads/*:refs/remotes/origin/*
[branch "hexo"]
        remote = origin
        merge = refs/heads/hexo
[user]
        email = hogan.chen@ymail.com
        name = hogan chen
[branch "master"]
        remote = origin
        merge = refs/heads/master

4.2 or use command to change the remote url
git remote set-url origin git@github.com:hoganchen/hoganchen.github.io.git
```

##### Git for Windows错误解决
http://blog.csdn.net/leedaning/article/details/49887015
http://blog.csdn.net/junheart/article/details/51324848
```
解决：修改~/.ssh/config，加入

Host *
    KexAlgorithms +diffie-hellman-group1-sha1


$ git clone ssh://hogan@173.17.40.143:29418/git_project
Cloning into 'git_project'...
Unable to negotiate with 173.17.40.143 port 29418: no matching key exchange method found. Their offer: diffie-hellman-group1-sha1
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.

在~/.ssh目录下新建config文件，并添加文件内容如下：
$ cat ~/.ssh/config
Host 173.17.40.143
    KexAlgorithms +diffie-hellman-group1-sha1

Host 173.17.40.143
    FingerprintHash md5
$

错误解决
no matching key exchange method found. Their offer: diffie-hellman-group1-sha1

解决方法：创建.ssh/config文件，并添加
Host 173.17.40.143
    KexAlgorithms +diffie-hellman-group1-sha1

RSA key fingerprint is SHA256

解决方法：在config文件中添加
Host 173.17.40.143
    FingerprintHash md5

```

##### 获取帮助
```
$ git help \<verb>
$ git \<verb> --help
$ man git-\<verb>
```

##### Git多平台换行符问题
http://kuanghy.github.io/2017/03/19/git-lf-or-crlf
```
跨平台协作开发是常有的，不统一的换行符确实对跨平台的文件交换带来了麻烦。最大的问题是，在不同平台上，换行符发生改变时，Git 会认为整个文件被修改，这就造成我们没法 diff，不能正确反映本次的修改。还好 Git 在设计时就考虑了这一点，其提供了一个 autocrlf 的配置项，用于在提交和检出时自动转换换行符，该配置有三个可选项：

    true: 提交时转换为 LF，检出时转换为 CRLF
    false: 提交检出均不转换
    input: 提交时转换为LF，检出时不转换

用如下命令即可完成配置：

#提交时转换为LF，检出时转换为CRLF
git config --global core.autocrlf true

#提交时转换为LF，检出时不转换
git config --global core.autocrlf input

#提交检出均不转换
git config --global core.autocrlf false
```

##### Git diff生成patch
http://blog.csdn.net/liuhaomatou/article/details/54410361
https://www.cnblogs.com/y041039/articles/2411600.html
https://www.cnblogs.com/chenfulin5/p/6210581.html

https://codeday.me/bug/20170308/5498.html
http://stackoverflow.com/questions/4350678/git-diff-w-ignore-whitespace-only-at-start-end-of-lines
```
1. 查看两个版本之间文件的修改列表
git diff -w 1b636c811df6862f309e0d0515166eb454a02e23..7a0cece26a1aa9a32795cf3623df342bea7a843b --stat wvt/

--stat参数的作用是只显示修改的文件列表，不显示详细修改记录

2. 生成patch
git diff -w 1b636c811df6862f309e0d0515166eb454a02e23..7a0cece26a1aa9a32795cf3623df342bea7a843b wvt/ > ~/wvt_bug_fix_patch_20180212.patch

以上命令是比较1b636c811df6862f309e0d0515166eb454a02e23与7a0cece26a1aa9a32795cf3623df342bea7a843b两个版本中，wvt目录的差异，-w选项的意思是忽略空白变化，然后将差异重定向生成标准的patch文件(注意：当生成patch时，前面提交的版本的commit id在前，后面提交的版本的commit id在后，不然patch就变成为当前版本回退需要删除那些内容了)

对于行尾使用：
git diff --ignore-space-at-eol

而不是你目前使用的是什么：
git diff -w (--ignore-all-space)

对于开始行…如果你想要一个内置的解决方案，你是运气不好。

3. 应用patch
git apply ~/wvt_bug_fix_patch_20180205.patch

4. 检查patch是否成功应用
git apply --check ~/wvt_bug_fix_patch_20180205.patch
```

##### Git head图解
https://codeday.me/bug/20170224/4134.html
```
G   H   I   J
 \ /     \ /
  D   E   F
   \  |  / \
    \ | /   |
     \|/    |
      B     C
       \   /
        \ /
         A

A =      = A^0
B = A^   = A^1     = A~1
C = A^2  = A^2
D = A^^  = A^1^1   = A~2
E = B^2  = A^^2
F = B^3  = A^^3
G = A^^^ = A^1^1^1 = A~3
H = D^2  = B^^2    = A^^^2  = A~2^2
I = F^   = B^3^    = A^^3^
J = F^2  = B^3^2   = A^^3^2
```

##### Git reset hard后恢复
https://tonydeng.github.io/2015/07/08/how-to-undo-almost-anything-with-git/
https://segmentfault.com/q/1010000000167491
```
git reflog查看操作历史，找到之前HEAD的hash值，然后git reset --hard到那个hash即可。
```

##### Stash操作
https://git-scm.com/book/zh/v1/Git-%E5%B7%A5%E5%85%B7-%E5%82%A8%E8%97%8F%EF%BC%88Stashing%EF%BC%89
https://jasonhzy.github.io/2016/06/15/git-stash/
https://kingofamani.gitbooks.io/git-teach/content/chapter_3_branch/stash.html
https://segmentfault.com/a/1190000002554160
https://zhuanlan.zhihu.com/p/28608106
```
保存

使用git stash保存当前的操作，如果不这么做，你在切换到别的分支之前就一定要提交已经有的改动。但你当前的操作尚未完成，所以要暂时保存起来。
查看

直接使用git stash list就可以了。

MyPC:project limi$ git stash list
stash@{0}: WIP on master: 3d72f0b clear file
stash@{1}: WIP on start-test: fabaa87 fix bug

git stash save some_msg 这样就比较容易区分了。另外 git stash 是个一堆合并提交的分支，可以在 tig 里慢慢看。其实 git-stash 就一 shell 脚本

恢复
用git stash pop stash@{num}，num 是你要恢复的操作的序号，所以你最好在回复前用git stash list查看一下。
git stash apply 不会删除掉这条 stash 的记录。 而 git stash pop stash@{num} 则会从 stash 列表中删除掉这条记录。
git stash pop命令是恢复stash队列中的stash@{0}，然后从记录就删除，就是常规的pop操作。

删除
stash存的不要过多，不然你也不知道哪个是哪个，最好随时清一清。
把所有的记录都清空掉用git stash clear。

暫時儲存現狀的操作
$ git stash save
可以省略 save。也可以在 save 之後加入欲顯示的訊息。

顯示暫存清單
$ git stash list

恢復暫存的操作
$ git stash pop
僅使用"git stash pop" 將可復原到最新的操作。指定stash ID （如：stash@{1} ），則可以復原特定的操作。

刪除暫存的操作
$ git stash drop
如果使用 "git stash drop"，會刪除最新的操作。指定stash ID （如：stash@{1} ），則可以刪除特定的操作。

刪除所有暫存的操作
$ git stash clear
```

##### 克隆现有仓库
```
ssh:
git clone git@github.com:hoganchen/hoganchen.github.io.git

https:
git clone https://github.com/hoganchen/hoganchen.github.io.git
```

##### 合并提交
http://wuaner.iteye.com/blog/1683282
https://gxnotes.com/article/203186.html
http://feisky.xyz/2015/06/04/git-commit/
https://zlargon.gitbooks.io/git-tutorial/content/patch/amend.html
```
git commit --amend -m "comments"
使用commit --amend时如果加了 -m 参数，commit-msg hook会为该commit生成一个新的Change-Id；所以，gerrit下做提交不要git commit --amend -m，因为这样新的commit对象会有不同的change-Id，而gerrit服务器是通过change-Id区别commit对象的；请使用git commit --amend（没有-m参数），并不要改变编辑窗口中的change-Id。
如果amend后加入-m选项，会生成新的change ID，如果不想要生成新的change ID，使用如下命令
git commit --amend
```

##### 添加文件到暂存区，可使用通配符*
```
git add \<filename>
```

##### 提交修改
```
git commit -m "comments"
```

##### 推送修改到远程仓库
```
git push origin master

girret master分支
git push origin HEAD:refs/for/master

girret git_project分支
git push origin HEAD:refs/for/git_project
```

##### 查看当前文档状态
```
git status
git status –s
```

##### 删除文件
http://blog.csdn.net/p106786860/article/details/52023885
http://hbiao68.iteye.com/blog/2213238
https://tonydeng.github.io/2015/07/08/how-to-undo-almost-anything-with-git/
```
# 删除暂存区文件
git rm \<filename>

# 删除暂存区文件，而不擅长本地文件，可使用通配符*
git rm --cached <filename>

撤销删除操作
git reset HEAD

(1) 回退所有内容到上一个版本
$git reset HEAD^
(2) 回退a.py这个文件的版本到上一个版本
$git reset HEAD^ a.py
(3) 向前回退到第3个版本
$git reset --soft HEAD~3
(4) 将本地的状态回退到和远程的一样
$git reset --hard origin/master
(5) 回退到某个版本
$git  reset  057d
(6) 回退到上一次提交的状态，按照某一次的commit完全反向的进行一次commit
$git revert HEAD

https://git-scm.com/book/zh/v2/Git-%E5%B7%A5%E5%85%B7-%E9%80%89%E6%8B%A9%E4%BF%AE%E8%AE%A2%E7%89%88%E6%9C%AC
祖先引用

祖先引用是另一种指明一个提交的方式。 如果你在引用的尾部加上一个 ^， Git 会将其解析为该引用的上一个提交。 假设你的提交历史是：

$ git log --pretty=format:'%h %s' --graph
* 734713b fixed refs handling, added gc auto, updated tests
*   d921970 Merge commit 'phedders/rdocs'
|\
| * 35cfb2b Some rdoc changes
* | 1c002dd added some blame and merge stuff
|/
* 1c36188 ignore *.gem
* 9b29157 add open3_detach to gemspec file list

你可以使用 HEAD^ 来查看上一个提交，也就是 “HEAD 的父提交”：

$ git show HEAD^
commit d921970aadf03b3cf0e71becdaab3147ba71cdef
Merge: 1c002dd... 35cfb2b...
Author: Scott Chacon <schacon@gmail.com>
Date:   Thu Dec 11 15:08:43 2008 -0800

    Merge commit 'phedders/rdocs'

你也可以在 ^ 后面添加一个数字——例如 d921970^2 代表 “d921970 的第二父提交” 这个语法只适用于合并(merge)的提交，因为合并提交会有多个父提交。 第一父提交是你合并时所在分支，而第二父提交是你所合并的分支：

$ git show d921970^
commit 1c002dd4b536e7479fe34593e72e6c6c1819e53b
Author: Scott Chacon <schacon@gmail.com>
Date:   Thu Dec 11 14:58:32 2008 -0800

    added some blame and merge stuff

$ git show d921970^2
commit 35cfb2b795a55793d7cc56a6cc2060b4bb732548
Author: Paul Hedderly <paul+git@mjr.org>
Date:   Wed Dec 10 22:22:03 2008 +0000

    Some rdoc changes

另一种指明祖先提交的方法是 ~。 同样是指向第一父提交，因此 HEAD~ 和 HEAD^ 是等价的。 而区别在于你在后面加数字的时候。 HEAD~2 代表 “第一父提交的第一父提交”，也就是 “祖父提交” —— Git 会根据你指定的次数获取对应的第一父提交。 例如，在之前的列出的提交历史中，HEAD~3 就是

$ git show HEAD~3
commit 1c3618887afb5fbcbea25b7c013f4e2114448b8d
Author: Tom Preston-Werner <tom@mojombo.com>
Date:   Fri Nov 7 13:47:59 2008 -0500

    ignore *.gem

也可以写成 HEAD^^^，也是第一父提交的第一父提交的第一父提交：

$ git show HEAD^^^
commit 1c3618887afb5fbcbea25b7c013f4e2114448b8d
Author: Tom Preston-Werner <tom@mojombo.com>
Date:   Fri Nov 7 13:47:59 2008 -0500

    ignore *.gem

你也可以组合使用这两个语法 —— 你可以通过 HEAD~3^2 来取得之前引用的第二父提交（假设它是一个合并提交）。

```

##### git rebase --skip误操作的恢复
http://blog.csdn.net/w_xue/article/details/10975719
http://blog.screensteps.com/recovering-from-a-disastrous-git-rebase-mistake
https://codeday.me/bug/20170821/57813.html
http://www.cauchy.me/2015/09/27/recovery-from-a-disastrous-git-rebase-mistake/

https://nieyong.github.io/git%E4%BD%BF%E7%94%A8%E7%AC%94%E8%AE%B0.html
http://www.itguai.com/git/a5954029.html
https://codeday.me/bug/20170216/350.html
http://www.cnblogs.com/sumsung753/p/3821511.html
```
hogan@ubuntu:~$git commit -a -m "add new chapter for automation system testing"
[master a7f5046] add new chapter for automation system testing
 1 file changed, 0 insertions(+), 0 deletions(-)
 rewrite doc/XXX_Test_Plan.docx (78%)

hogan@ubuntu:~$git pull --rebase
remote: Counting objects: 42, done
remote: Finding sources: 100% (26/26)
remote: Total 26 (delta 12), reused 21 (delta 12)
Unpacking objects: 100% (26/26), done.
From ssh://172.0.0.1:29418/GIt_Project
   30b05d8..6d8c8d0  master     -> origin/master
First, rewinding head to replay your work on top of it...
Applying: add new chapter for automation system testing
Using index info to reconstruct a base tree...
M	doc/XXX_Test_Plan.docx
Falling back to patching base and 3-way merge...
warning: Cannot merge binary files: doc/XXX_Test_Plan.docx (HEAD vs. add new chapter for automation system testing)
Auto-merging doc/XXX_Test_Plan.docx
CONFLICT (content): Merge conflict in doc/XXX_Test_Plan.docx
Failed to merge in the changes.
Patch failed at 0001 add new chapter for automation system testing
The copy of the patch that failed is found in:
   /home/hogan/GIt_Project/.git/rebase-apply/patch

When you have resolved this problem, run "git rebase --continue".
If you prefer to skip this patch, run "git rebase --skip" instead.
To check out the original branch and stop rebasing, run "git rebase --abort".

hogan@ubuntu:~$git st
rebase in progress; onto 6d8c8d0
You are currently rebasing branch 'master' on '6d8c8d0'.
  (fix conflicts and then run "git rebase --continue")
  (use "git rebase --skip" to skip this patch)
  (use "git rebase --abort" to check out the original branch)

Unmerged paths:
  (use "git reset HEAD <file>..." to unstage)
  (use "git add <file>..." to mark resolution)

	both modified:      doc/XXX_Test_Plan.docx

hogan@ubuntu:~$git rebase --skip

hogan@ubuntu:~$git st
On branch master
Your branch is up-to-date with 'origin/master'.

hogan@ubuntu:~$git log

hogan@ubuntu:~$git reflog
6d8c8d0 HEAD@{0}: rebase finished: returning to refs/heads/master
6d8c8d0 HEAD@{1}: pull --rebase: checkout 6d8c8d06708e57def4fd2222616daa72a58d7181
a7f5046 HEAD@{2}: commit: add new chapter for automation system testing
30b05d8 HEAD@{3}: pull: Fast-forward
3f2d3e9 HEAD@{4}: commit: update the shell command line to get the usb device name
7461406 HEAD@{5}: reset: moving to 746140620b686c91a81019f0f2df8dea3d8d0a79
5752e93 HEAD@{6}: commit (amend): update the shell command line to get the usb device name
54fa1df HEAD@{7}: commit: update the command line to get the usb device name
7461406 HEAD@{8}: rebase finished: returning to refs/heads/master
7461406 HEAD@{9}: pull --rebase: checkout 746140620b686c91a81019f0f2df8dea3d8d0a79
d33dd57 HEAD@{10}: rebase finished: returning to refs/heads/master

hogan@ubuntu:~$git checkout -b doc_recovery a7f5046
Switched to a new branch 'doc_recovery'

```

##### 删除分支
https://backlogtool.com/git-tutorial/cn/stepup/stepup2_5.html
https://git-scm.com/book/zh/v1/Git-%E5%88%86%E6%94%AF-%E5%88%86%E6%94%AF%E7%9A%84%E7%AE%A1%E7%90%86
https://zlargon.gitbooks.io/git-tutorial/content/branch/create_delete.html
https://qiita.com/hudichao/items/d665cd769ed1d2ce832a
```
hogan@ubuntu:~$git branch
  doc_recovery
* master
hogan@ubuntu:~$git branch -D doc_recovery
Deleted branch doc_recovery (was a7f5046).
hogan@ubuntu:~$git st
On branch master
Your branch is up-to-date with 'origin/master'.
hogan@ubuntu:~$git branch
* master

```

##### git远程操作
http://www.ruanyifeng.com/blog/2014/06/git_remote.html
https://git-scm.com/book/zh/v2/Git-%E5%88%86%E6%94%AF-%E8%BF%9C%E7%A8%8B%E5%88%86%E6%94%AF
http://www.cnblogs.com/wangkangluo1/archive/2011/09/02/2164313.html
https://blog.csdn.net/whlclw/article/details/8633328

##### git branch操作
https://git-scm.com/book/zh/v2/Git-%E5%88%86%E6%94%AF-%E5%88%86%E6%94%AF%E7%9A%84%E6%96%B0%E5%BB%BA%E4%B8%8E%E5%90%88%E5%B9%B6
https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/001375840038939c291467cc7c747b1810aab2fb8863508000
https://zlargon.gitbooks.io/git-tutorial/content/branch/create_delete.html

http://blog.csdn.net/isaisai/article/details/44935653
```
查看本地分支
git branch

查看远程分支
git branch -r

查看所有分支
git branch -a

创建分支
git branch <branch_name>

创建+切换分支
git checkout -b <branch_name>

合并某分支到当前分支
git merge <branch_name>

切换分支(如果branch_name分支不存在，则会checkout remote的同名分支作为本地分支)
git checkout <branch_name>

删除分支，要删除的分支不能是当前使用的分支，如果是，需要先切换到其它分支，再做删除操作
如果分支已修改，小写d删除会失败，会提示没有merge，大写D是强制删除
git branch -d <branch_name>
git branch -D <branch_name>

checkout远程分支到本地
git checkout -b git_project remotes/origin/git_project
git checkout git_project


hogan@ubuntu:~/git_project/doc/Test$ git checkout -b git_project remotes/origin/git_project
Checking out files: 100% (6131/6131), done.
Branch git_project set up to track remote branch git_project from origin.
Switched to a new branch 'git_project'

hogan@ubuntu:~/git_project/doc/Test$ git checkout git_project
Checking out files: 100% (6131/6131), done.
Branch git_project set up to track remote branch git_project from origin.
Switched to a new branch 'git_project'
```

##### Git clone非master分支
https://gaohaoyang.github.io/2016/07/07/git-clone-not-master-branch/
```
直接使用命令

git branch -r #查看远程分支

或

git branch -a #查看所有分支

会显示

origin/HEAD -> origin/master
origin/daily/1.2.2
origin/daily/1.3.0
origin/daily/1.4.1
origin/develop
origin/feature/daily-1.0.0
origin/master

然后直接

git checkout origin/daily/1.4.1
git checkout -b local-branchname origin/remote_branchname
```

##### cherry-pick命令
https://marklodato.github.io/visual-git-guide/index-zh-cn.html
```
Cherry Pick

cherry-pick命令"复制"一个提交节点并在当前分支做一次完全一样的新提交。
```

##### Git fetch 和 git pull的区别
http://www.jianshu.com/p/4060731613c1
https://ruby-china.org/topics/15729
```
Git中从远程的分支获取最新的版本到本地有这样2个命令：

    git fetch：相当于是从远程获取最新版本到本地，不会自动merge

    git fetch origin master
    git log -p master..origin/master
    git merge origin/master

    以上命令的含义：
        首先从远程的origin的master主分支下载最新的版本到origin/master分支上
        然后比较本地的master分支和origin/master分支的差别
        最后进行合并

上述过程其实可以用以下更清晰的方式来进行：

git fetch origin master:test
git diff test
git merge test

从远程获取最新的版本到本地的test分支上,之后再进行比较合并.

    git pull：相当于是从远程获取最新版本并merge到本地

    git pull origin master

上述命令其实相当于git fetch 和 git merge
在实际使用中，git fetch更安全一些, 因为在merge前，我们可以查看更新情况，然后再决定是否合并.
```

##### Git远程操作详解
http://www.ruanyifeng.com/blog/2014/06/git_remote.html
http://liwei5917.logdown.com/posts/1417079-git-remote-collaboration

![git_remote.jpg](/upload_image/git-usage/git_remote.jpg)
```
git clone
git remote
git fetch
git pull
git push
```

##### 查看修改
```
git diff				#只显示尚未暂存的修改
git diff --cached		#查看已暂存的修改
git diff --staged		#查看已暂存的修改
```

##### 跳过添加文件到暂存区，Git就会自动把所有已经跟踪过的文件暂存起来一并提交
```
git commit -a -m 'added new benchmarks'
```

##### 重命名文件
```
git mv file_from file_to
```

##### 查看提交历史
```
git log
git log –p			#显示每次的提交的内容差异
git log –p -2		#最近两次的内容差异
git log --stat		#显示文件修改的简略统计信息
```

##### 撤消操作
https://tonydeng.github.io/2015/07/08/how-to-undo-almost-anything-with-git/ (**必读**)
https://github.com/geeeeeeeeek/git-recipes/wiki/5.2-%E4%BB%A3%E7%A0%81%E5%9B%9E%E6%BB%9A%EF%BC%9AReset%E3%80%81Checkout%E3%80%81Revert-%E7%9A%84%E9%80%89%E6%8B%A9

https://zhuanlan.zhihu.com/p/28130254
https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-%E6%92%A4%E6%B6%88%E6%93%8D%E4%BD%9C
https://www.git-tower.com/learn/git/ebook/cn/command-line/advanced-topics/undoing-things
http://blog.jobbole.com/87700/
http://blog.sina.com.cn/s/blog_4a2defca0102wcr7.html
```
#重新提交
git commit --amend

$ git commit -m 'initial commit'
$ git add forgotten_file
$ git commit --amend
```

##### 取消暂存的文件，可使用通配符*
```
git reset HEAD <filename>
```

##### 撤消对文件的修改，可使用通配符*
```
git checkout -- <filename>
```

##### 查看远程仓库
```
git remote
git remote -v
git remote show
git remote show origin
```

##### 添加远程仓库
```
git remote add <shortname> <url>
```

##### 远程仓库抓取
```
git fetch [remote-name]
```

##### 远程仓库拉取，如果你有一个分支设置为跟踪一个远程分支，可以使用git pull命令来自动的抓取然后合并远程分支到当前分支
```
git pull
```

##### 远程仓库移除
```
git remote rm <remote-name>
```

##### 远程仓库重命名
```
git remote rename <orig-name> <new-name>
```