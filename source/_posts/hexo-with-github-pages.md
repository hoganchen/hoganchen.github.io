---
title: Ubuntu下Hexo + Github博客搭建过程记录
date: 2018-06-09 18:16:55
tags:
---

### 选择Hexo还是Jekyll
https://www.jianshu.com/p/ce1619874d34

于是开始接触比较流行的一些静态博客框架，比较流行的有Jekyll，Hexo，Simple，Octopress，Pelican以及Lo·gecho等等。这些静态程序可以说都有各自的好处，但最后我选择了Hexo来搭建自己的博客，和Jekyll相比，选择Hexo主要原因是：
```
1. Jeky基于Ruby实现，安装Jeky需要搭建Ruby环境，在Windows搭建Ruby环境并不是被推荐的，而 Hexo基于NodeJs实现，在Windows上安装NodeJs开发环境简单。
2. 比较直接的另一个原因是在网上查找了很多博客的主题，发现Jekyll官网提供的主题都不怎么好看(可能是个人原因)，而Hexo的主题看的比较顺眼。
两者都支持Markdown语法，这点我非常喜欢。
```

<!-- more -->

### Hexo博客开发过程
https://hexo.io/zh-cn/docs/index.html

#### 安装nodejs和npm
https://www.howtoing.com/install-latest-nodejs-npm-on-ubuntu
https://github.com/nodesource/distributions

以下为ubuntu中添加NodeJS的PPA，并安装了8.*版本的nodejs，sudo apt-get install nodejs命令会同时安装nodejs和npm，所以不需要再次安装npm，同时也不要安装ubuntu包管理器自带的nodejs，ubuntu自带的nodejs版本过低(v0.10.25)，会导致hexo generate失败，如已按照旧版本的nodejs和npm，请使用命令sudo apt-get purge nodejs和sudo apt-get purge npm删除旧版本的nodejs和npm，然后根据如下步骤安装新版本的nodejs和npm。
如果系统中以前没有添加过nodejs的ppa，可以直接跳到第4步

1. Remove the old PPA if it exists
```
This step is only required if you previously used Chris Lea's Node.js PPA.

# add-apt-repository may not be present on some Ubuntu releases:
# sudo apt-get install python-software-properties
sudo add-apt-repository -y -r ppa:chris-lea/node.js
sudo rm -f /etc/apt/sources.list.d/chris-lea-node_js-*.list
sudo rm -f /etc/apt/sources.list.d/chris-lea-node_js-*.list.save
```

2. Add the NodeSource package signing key
```
curl -sSL https://deb.nodesource.com/gpgkey/nodesource.gpg.key | sudo apt-key add -
# wget can also be used:
# wget --quiet -O - https://deb.nodesource.com/gpgkey/nodesource.gpg.key | sudo apt-key add -
```

3. Add the desired NodeSource repository
```
# Replace with the branch of Node.js or io.js you want to install: node_6.x, node_8.x, etc...
VERSION=node_8.x
# The below command will set this correctly, but if lsb_release isn't available, you can set it manually:
# - For Debian distributions: jessie, sid, etc...
# - For Ubuntu distributions: xenial, bionic, etc...
# - For Debian or Ubuntu derived distributions your best option is to use the codename corresponding to the upstream release your distribution is based off. This is an advanced scenario and unsupported if your distribution is not listed as supported per earlier in this README.
DISTRO="$(lsb_release -s -c)"
echo "deb https://deb.nodesource.com/$VERSION $DISTRO main" | sudo tee /etc/apt/sources.list.d/nodesource.list
echo "deb-src https://deb.nodesource.com/$VERSION $DISTRO main" | sudo tee -a /etc/apt/sources.list.d/nodesource.list
```

4. 上述步骤可以省略，直接在/etc/apt/sources.list.d/目录下新建nodesource.list文件，并修改其内容如下
如需要按照别的版本的nodejs，直接根据https://github.com/nodesource/distributions网址的说明，直接修改nodesource.list文件的版本即可

```
hogan@ubuntu:/mnt/share/github/hoganchen.github.io$ cat /etc/apt/sources.list.d/nodesource.list
deb https://deb.nodesource.com/node_8.x trusty main
deb-src https://deb.nodesource.com/node_8.x trusty main
```

5. Update package lists and install Node.js
```
sudo apt-get update
sudo apt-get install nodejs
```

6. 通过添加ppa源，然后通过sudo apt-get install nodejs方式安装nodejs的同时，npm同时也会被安装，但这时输入sudo apt-get install npm试图安装npm，会出现如下错误，但是随后查看nodejs和npm版本的命令能成功执行，可以忽略该错误。
https://github.com/nodesource/distributions/issues/182
```
apt-get install npm
Reading package lists... Done
Building dependency tree
Reading state information... Done
Some packages could not be installed. This may mean that you have
requested an impossible situation or if you are using the unstable
distribution that some required packages have not yet been created
or been moved out of Incoming.
The following information may help to resolve the situation:

The following packages have unmet dependencies:
 npm : Depends: nodejs but it is not going to be installed
       Depends: node-abbrev (>= 1.0.4) but it is not going to be installed
       Depends: node-ansi (>= 0.3.0-2) but it is not going to be installed
...

如以下两条命令被成功执行，并返回了版本号，则以上错误忽略。
hogan@ubuntu:/mnt/share/github/hoganchen.github.io$ nodejs -v
v8.11.2
hogan@ubuntu:/mnt/share/github/hoganchen.github.io$ npm -v
5.6.0
```

#### 安装git
```
sudo apt-get update
sudo apt-get install git
```

#### github添加username.github.io的库
我添加的库为hoganchen.github.io，以下都以我添加的库来说明，可自行修改为对应的库名称

#### 安装hexo博客
https://hexo.io/zh-cn/docs/index.html

##### 安装hexo
https://github.com/hexojs/hexo/issues/1836
https://docs.npmjs.com/getting-started/fixing-npm-permissions

以上两个网址建议不要用sudo的方式安装hexo，并给出了解决方案，但是sudo方式安装是OK的，所以就没有去care权限问题了，有兴趣可以看看。
```
sudo npm install -g hexo-cli
```

##### 建站
https://hexo.io/zh-cn/docs/setup.html

安装 Hexo 完成后，请执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件。
```
hexo init hoganchen.github.io
cd hoganchen.github.io
npm install
```

##### 安装 hexo-deployer-git
https://hexo.io/zh-cn/docs/deployment.html

Hexo 提供了快速方便的一键部署功能，让您只需一条命令就能将网站部署到服务器上。
```
$ npm install hexo-deployer-git --save

修改配置。

deploy:
  type: git
  repo: <repository url>
  branch: [branch]
  message: [message]

示例如下:
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: https://github.com/hoganchen/hoganchen.github.io.git
  branch: master
```

##### 修改_config.yml中site section和Deployment section相关信息，全部内容如下
https://hexo.io/zh-cn/docs/configuration.html
```
# Hexo Configuration
## Docs: https://hexo.io/docs/configuration.html
## Source: https://github.com/hexojs/hexo/

# Site
title: Hogan's Blog
subtitle:
description:
keywords:
author: Hogan Chen
language:
timezone:

# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: http://yoursite.com
root: /
permalink: :year/:month/:day/:title/
permalink_defaults:

# Directory
source_dir: source
public_dir: public
tag_dir: tags
archive_dir: archives
category_dir: categories
code_dir: downloads/code
i18n_dir: :lang
skip_render:

# Writing
new_post_name: :title.md # File name of new posts
default_layout: post
titlecase: false # Transform title into titlecase
external_link: true # Open external links in new tab
filename_case: 0
render_drafts: false
post_asset_folder: false
relative_link: false
future: true
highlight:
  enable: true
  line_number: true
  auto_detect: false
  tab_replace:

# Home page setting
# path: Root path for your blogs index page. (default = '')
# per_page: Posts displayed per page. (0 = disable pagination)
# order_by: Posts order. (Order by date descending by default)
index_generator:
  path: ''
  per_page: 10
  order_by: -date

# Category & Tag
default_category: uncategorized
category_map:
tag_map:

# Date / Time format
## Hexo uses Moment.js to parse and display date
## You can customize the date format as defined in
## http://momentjs.com/docs/#/displaying/format/
date_format: YYYY-MM-DD
time_format: HH:mm:ss

# Pagination
## Set per_page to 0 to disable pagination
per_page: 10
pagination_dir: page

# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
# theme: landscape
theme: next

# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: https://github.com/hoganchen/hoganchen.github.io.git
  branch: master
```

##### 相关命令
https://hexo.io/zh-cn/docs/commands.html
https://segmentfault.com/a/1190000002632530

```
hexo n "我的博客" == hexo new "我的博客" #新建文章
hexo p == hexo publish #发布草稿
hexo g == hexo generate #生成静态网页
hexo s == hexo server #启动服务预览
hexo d == hexo deploy #部署

hexo clean ##清除缓存 网页正常情况下可以忽略此条命令
```

##### github相关操作
https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013752340242354807e192f02a44359908df8a5643103a000
http://www.ruanyifeng.com/blog/2014/06/git_remote.html
https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93%E7%9A%84%E4%BD%BF%E7%94%A8
https://blog.csdn.net/u013372487/article/details/52925960

在上述操作中，deploy的分支为master，然而也需要把原始的md, 图片等文件git管理起来，这时在github上hoganchen.github.io库上再创建一个分支为hexo，并在setting中把hexo设置为默认分支
![github-hexo-branch.PNG](/upload_image/hexo-with-github-pages/github-hexo-branch.PNG)
![github-hexo-branch-as-default-branch.PNG](/upload_image/hexo-with-github-pages/github-hexo-branch-as-default-branch.PNG)

```
由于hexo建站时已主动生成.gitignore文件，内容如下：
hogan@ubuntu:/mnt/share/github/hoganchen.github.io$ cat .gitignore
.DS_Store
Thumbs.db
db.json
*.log
node_modules/
public/

所以可以直接git操作，并与远程库关联
cd hoganchen.github.io/
git init

git config user.email "hogan.chen@ymail.com"
git config user.name "hogan chen"

git checkout -b hexo
git add .
git commit -m "init hexo repository"
git remote add hexo https://github.com/hoganchen/hoganchen.github.io.git
git push origin hexo

以上操作会把原始数据上传到hexo分支，而hexo d也会把生产的静态网站上传到master分支，这时就可以用一个仓库的2个分支完美管理博客内容，并可以在不同的电脑之间进行写作。

在新的电脑上，除了不需要hexo init hoganchen.github.io命令外，别的命令都需要，归纳如下:
sudo apt-get update
sudo apt-get install git
sudo apt-get install nodejs
sudo npm install -g hexo-cli

git clone https://github.com/hoganchen/hoganchen.github.io.git
cd hoganchen.github.io.git
npm install
npm install hexo-deployer-git --save

# hexo为默认的branch
git branch -r
git branch -a
git checkout -b master origin/master
git checkout hexo

git config user.email "hogan.chen@ymail.com"
git config user.name "hogan chen"

# 提交原始数据到hexo分支
git add .
git commit -m "commit message"
git push origin hexo

# 静态网站数据提交master分支
hexo clean
hexo g
hexo s
hexo d

cd .deploy_git/
git config user.email "hogan.chen@ymail.com"
git config user.name "hogan chen"

hexo d
```

##### VirtualBox相关操作
由于是在虚拟机环境上执行以上操作，所以为了预览文章，需要在虚拟机上作端口转发，设置如下，这样就可以在windows浏览器中输入http://localhost:4000/来进行预览。
![hexo-server-port-forward.PNG](/upload_image/hexo-with-github-pages/hexo-server-port-forward.PNG)

##### hexo博客如何设置「阅读全文」
http://theme-next.iissnan.com/faqs.html#%E9%A6%96%E9%A1%B5%E6%98%BE%E7%A4%BA%E6%96%87%E7%AB%A0%E6%91%98%E5%BD%95

```
在首页显示一篇文章的部分内容，并提供一个链接跳转到全文页面是一个常见的需求。 NexT 提供三种方式来控制文章在首页的显示方式。 也就是说，在首页显示文章的摘录并显示 阅读全文 按钮，可以通过以下方法：

1. 在文章中使用 <!-- more --> 手动进行截断，Hexo 提供的方式 推荐
2. 在文章的 front-matter 中添加 description，并提供文章摘录

3. 自动形成摘要，在 主题配置文件 中添加：

auto_excerpt:
  enable: true
  length: 150

默认截取的长度为 150 字符，可以根据需要自行设定

建议使用 <!-- more -->（即第一种方式），除了可以精确控制需要显示的摘录内容以外， 这种方式也可以让 Hexo 中的插件更好的识别。
```

##### 更换主题
```
cd hoganchen.github.io/
git clone https://github.com/iissnan/hexo-theme-next themes/next
cp -af themes/landscape/source/upload_image/ themes/next/source/

修改_config.yml，修改Extensions section中themes为next，如下
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
# theme: landscape
theme: next
```