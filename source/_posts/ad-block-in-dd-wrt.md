---
title: DD-WRT设置广告过滤
date: 2018-06-11 13:49:54
tags: Misc
---

<!-- more -->

<ol>

##### DD-WRT, Tomato 和 OpenWRT 有什么区别和联系
https://www.zhihu.com/question/21271677
https://zh.wikipedia.org/zh-cn/OpenWrt
https://zh.wikipedia.org/zh-cn/DD-WRT

##### xiaomi广告
https://www.zhihu.com/question/54992021
https://www.zhihu.com/question/20162501
https://www.zhihu.com/question/27707202

dd-wrt/openwrt + adbyby插件
```
作者：Repobor
链接：https://www.zhihu.com/question/54992021/answer/150990399
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

抓了一堆网址 加到hosts里127.0.0.1 de.pandora.xiaomi.com
127.0.0.1 mishop.pandora.xiaomi.com
127.0.0.1 auth.api.gitv.tv
127.0.0.1 misc.pandora.xiaomi.com
127.0.0.1 tvapi.kuyun.com
127.0.0.1 data.mistat.xiaomi.com
127.0.0.1 tv.aiseet.atianqi.com
127.0.0.1 vv.play.aiseet.atianqi.com
127.0.0.1 gallery.pandora.xiaomi.com
127.0.0.1 config.kuyun.com
127.0.0.1 bss.pandora.xiaomi.com
127.0.0.1 o2o.api.xiaomi.com
127.0.0.1 dvb.pandora.xiaomi.com
127.0.0.1 alog.umeng.com
127.0.0.1 pandora.mi.com
127.0.0.1 api.ad.xiaomi.com
127.0.0.1 tvapi.kuyun.com
127.0.0.1 sdkconfig.ad.xiaomi.com
127.0.0.1 assistant.pandora.xiaomi.com
127.0.0.1 tracking.miui.com
127.0.0.1 misc.pandora.xiaomi.com
127.0.0.1 gvod.aiseejapp.atianqi.com
127.0.0.1 omgmta.play.aiseet.atianqi.com
127.0.0.1 jellyfish.pandora.xiaomi.com
127.0.0.1 starfish.pandora.xiaomi.com
127.0.0.1 misc.in.duokanbox.com


顺便连接电脑禁用
com.xiaomi.tv.appupgrade
com.miui.systemAdSolution
com.xiaomi.tv.upgrade
com.xiaomi.tv.advertise
com.miui.cloudservice
com.xiaomi.mitv.tvpush.tvpushservice
com.xiaomi.smarthome
这些并没有什么用的程序厚颜无耻的发个教程地址：解决小米电视/盒子 广告 - 后花园
```

##### 优酷视频广告
https://www.zhihu.com/question/20610513
```
作者：隔岸观火
链接：https://www.zhihu.com/question/20610513/answer/33071655
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

PC端
1、打开我的电脑，在地址栏输入：C:\Windows\System32\drivers\etc 按enter 键，找到hosts 文件
2、用记事本方式 打开它hosts文件
3、在里面加入 以下代码，保存，退出即可，破解完成！！

#优酷
127.0.0.1 atm.youku.com
127.0.0.1 fvid.atm.youku.com
127.0.0.1 html.atm.youku.com
127.0.0.1 valb.atm.youku.com
127.0.0.1 valf.atm.youku.com
127.0.0.1 valo.atm.youku.com
127.0.0.1 valp.atm.youku.com
127.0.0.1 Lstat.youku.com
127.0.0.1 speed.lstat.youku.com
127.0.0.1 urchin.lstat.youku.com
127.0.0.1 stat.youku.com
127.0.0.1 static.lstat.youku.com
127.0.0.1 valc.atm.youku.com
127.0.0.1 vid.atm.youku.com
127.0.0.1 walp.atm.youku.com#CNTV
127.0.0.1 a.cctv.com
127.0.0.1 a.cntv.cn
127.0.0.1 ad.cctv.com
127.0.0.1 d.cNtv.cn
127.0.0.1 adguanggao.eee114.com
127.0.0.1 cctv.adsunion.com

#新浪视频
127.0.0.1 dcads.sina.com.cn

#pptv
127.0.0.1 pp2.pptv.com

#乐视
127.0.0.1 pro.letv.com

#搜狐高清
127.0.0.1 imagEs.sohu.com

#From LoneBlog.com
#我乐网
127.0.0.1 acs.56.com
127.0.0.1 acs.agent.56.com
127.0.0.1 acs.agent.v-56.com
127.0.0.1 Bill.agent.56.com
127.0.0.1 bill.agent.v-56.com
127.0.0.1 stat.56.com
127.0.0.1 stat2.corp.56.com
127.0.0.1 union.56.com
127.0.0.1 uvimage.56.com
127.0.0.1 v16.56.com

#6间房
127.0.0.1 pole.6rooms.com
127.0.0.1 shrek.6.cn
127.0.0.1 simba.6.cn
127.0.0.1 union.6.cn

#土豆网
127.0.0.1 adextensioncontrol.tudou.com
127.0.0.1 iwstat.tudou.com
127.0.0.1 nstat.tudou.com
127.0.0.1 stats.tudou.com
127.0.0.1 *.p2v.tudou.com*
127.0.0.1 at-img1.tdimg.com
127.0.0.1 at-img2.tdimg.com
127.0.0.1 at-img3.tdimg.com
127.0.0.1 adplay.tudou.com
127.0.0.1 adcontroL.tudou.com
127.0.0.1 stat.tudou.com

#酷6网
127.0.0.1 1.allyes.cOm.cn
127.0.0.1 analytics.ku6.com
127.0.0.1 gug.ku6cdn.com
127.0.0.1 ku6.allyes.com
127.0.0.1 ku6afp.allyes.com
127.0.0.1 pq.stat.ku6.com
127.0.0.1 st.vq.ku6.cn
127.0.0.1 stat0.888.ku6.com
127.0.0.1 stat1.888.ku6.com
127.0.0.1 stat2.888.ku6.com
127.0.0.1 stat3.888.ku6.com
127.0.0.1 static.ku6.com
127.0.0.1 v0.stat.ku6.com
127.0.0.1 v1.stat.ku6.com
127.0.0.1 v2.stat.ku6.com
127.0.0.1 v3.stat.ku6.com

#激动网
127.0.0.1 86file.megajoy.com
127.0.0.1 86Get.joy.cn
127.0.0.1 86log.joy.cn

#天线视频
127.0.0.1 casting.openv.com
127.0.0.1 m.openv.tv
127.0.0.1 uniclick.openv.com

手机端Android系统操作方法：
1、 首先你的手机需要有ROOT权限。
2、 在R.E浏览器进入/etc/hosts目录下，找到hosts文件，复制提取出来，用记事本打开。
3、 然后将以上的网址加进去，替换存为原来的hosts文件，并记得更改权限为rw-r--r--。
```

##### 自动切换代理
https://eliyar.biz/AutoProxy-By-Shadowsocks-and-SwitchyOmega/
https://github.com/gfwlist/gfwlist
https://github.com/FelisCatus/SwitchyOmega/wiki/GFWList
```
设置自动切换
    打开SwitchyOmega 设置，新建情景模式， 选择自动切换模式
    导入在线规则列表，类型选择AutoProxy，可以选择导入gfwlist - https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt 或者自己自定义的AutoProxy文件。
    保存设置并更新情景模式，若更新失败则开启全局代理后更新。
    设置规则匹配则使用代理模式，否则直接连接。保存退出。


GFWList URL(Github): https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt

Notwithstanding Github is competent for distribution, to hedge outages or connection issues we still recommend using any URL below.

Official mirror URLs:

    Pagure: https://pagure.io/gfwlist/raw/master/f/gfwlist.txt

    Repo.or.cz: http://repo.or.cz/gfwlist.git/blob_plain/HEAD:/gfwlist.txt

    Bitbucket: https://bitbucket.org/gfwlist/gfwlist/raw/HEAD/gfwlist.txt

    Gitlab: https://gitlab.com/gfwlist/gfwlist/raw/master/gfwlist.txt

    TuxFamily: https://git.tuxfamily.org/gfwlist/gfwlist.git/plain/gfwlist.txt

```