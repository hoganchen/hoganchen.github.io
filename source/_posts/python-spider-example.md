---
title: python简单爬虫示例
date: 2018-06-11 16:21:20
tags: Python
---

<!-- more -->

<ol>

##### 常用User Agent
http://blog.csdn.net/kang_tju/article/details/52563374
http://blkstone.github.io/2016/03/02/crawler-anti-anti-cheat/
https://www.waitig.com/python-%E7%88%AC%E8%99%AB%E4%B8%80%E4%BA%9B%E5%B8%B8%E7%94%A8%E7%9A%84uauser-agent.html
https://www.zhihu.com/question/19553117

https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/User-Agent/Firefox
http://www.webapps-online.com/online-tools/user-agent-strings/dv/browser51854/firefox
https://developers.whatismybrowser.com/useragents/explore/software_name/firefox/9
https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Browser_detection_using_the_user_agent

http://tools.jb51.net/table/useragent
https://zhuanlan.zhihu.com/p/21252983
http://www.gooseeker.com/doc/thread-1829-1-1.html
http://www.skyfox.org/useragent.html
http://blog.csdn.net/tao_627/article/details/42297443
http://blog.csdn.net/u012175089/article/details/61199238
https://www.bbsmax.com/A/GBJr7eZ950/
https://www.bbsmax.com/A/Vx5MjWWgdN/
http://www.361way.com/ieua/692.html
http://www.jianshu.com/p/da6a44d0791e
http://blog.csdn.net/qianqianstd/article/details/52185488
http://www.360doc.com/content/12/1012/21/7662927_241124973.shtml
http://blog.sina.com.cn/s/blog_9513526f0101pjvt.html
http://www.966266.com/jishu/32.html
http://www.cftea.com/c/2010/08/M3TS2JCPZ0IQOW60.asp
http://techseo.cn/python/31.html
```
USER_AGENTS = [
    "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; AcooBrowser; .NET CLR 1.1.4322; .NET CLR 2.0.50727)",
    "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 6.0; Acoo Browser; SLCC1; .NET CLR 2.0.50727; Media Center PC 5.0; .NET CLR 3.0.04506)",
    "Mozilla/4.0 (compatible; MSIE 7.0; AOL 9.5; AOLBuild 4337.35; Windows NT 5.1; .NET CLR 1.1.4322; .NET CLR 2.0.50727)",
    "Mozilla/5.0 (Windows; U; MSIE 9.0; Windows NT 9.0; en-US)",
    "Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; Win64; x64; Trident/5.0; .NET CLR 3.5.30729; .NET CLR 3.0.30729; .NET CLR 2.0.50727; Media Center PC 6.0)",
    "Mozilla/5.0 (compatible; MSIE 8.0; Windows NT 6.0; Trident/4.0; WOW64; Trident/4.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NET CLR 3.0.30729; .NET CLR 1.0.3705; .NET CLR 1.1.4322)",
    "Mozilla/4.0 (compatible; MSIE 7.0b; Windows NT 5.2; .NET CLR 1.1.4322; .NET CLR 2.0.50727; InfoPath.2; .NET CLR 3.0.04506.30)",
    "Mozilla/5.0 (Windows; U; Windows NT 5.1; zh-CN) AppleWebKit/523.15 (KHTML, like Gecko, Safari/419.3) Arora/0.3 (Change: 287 c9dfb30)",
    "Mozilla/5.0 (X11; U; Linux; en-US) AppleWebKit/527+ (KHTML, like Gecko, Safari/419.3) Arora/0.6",
    "Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US; rv:1.8.1.2pre) Gecko/20070215 K-Ninja/2.1.1",
    "Mozilla/5.0 (Windows; U; Windows NT 5.1; zh-CN; rv:1.9) Gecko/20080705 Firefox/3.0 Kapiko/3.0",
    "Mozilla/5.0 (X11; Linux i686; U;) Gecko/20070322 Kazehakase/0.4.5",
    "Mozilla/5.0 (X11; U; Linux i686; en-US; rv:1.9.0.8) Gecko Fedora/1.9.0.8-1.fc10 Kazehakase/0.5.6",
    "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/535.11 (KHTML, like Gecko) Chrome/17.0.963.56 Safari/535.11",
    "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_3) AppleWebKit/535.20 (KHTML, like Gecko) Chrome/19.0.1036.7 Safari/535.20",
    "Opera/9.80 (Macintosh; Intel Mac OS X 10.6.8; U; fr) Presto/2.9.168 Version/11.52",
]

# 随机生成user-agent
class RandomUAMiddleware(object):

    def process_request(self, request, spider):
        request.headers["User-Agent"]=random.choice(USER_AGENTS)


USER_AGENTS = [
    "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; AcooBrowser; .NET CLR 1.1.4322; .NET CLR 2.0.50727)",
    "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 6.0; Acoo Browser; SLCC1; .NET CLR 2.0.50727; Media Center PC 5.0; .NET CLR 3.0.04506)",
    "Mozilla/4.0 (compatible; MSIE 7.0; AOL 9.5; AOLBuild 4337.35; Windows NT 5.1; .NET CLR 1.1.4322; .NET CLR 2.0.50727)",
    "Mozilla/5.0 (Windows; U; MSIE 9.0; Windows NT 9.0; en-US)",
    "Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; Win64; x64; Trident/5.0; .NET CLR 3.5.30729; .NET CLR 3.0.30729; .NET CLR 2.0.50727; Media Center PC 6.0)",
    "Mozilla/5.0 (compatible; MSIE 8.0; Windows NT 6.0; Trident/4.0; WOW64; Trident/4.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NET CLR 3.0.30729; .NET CLR 1.0.3705; .NET CLR 1.1.4322)",
    "Mozilla/4.0 (compatible; MSIE 7.0b; Windows NT 5.2; .NET CLR 1.1.4322; .NET CLR 2.0.50727; InfoPath.2; .NET CLR 3.0.04506.30)",
    "Mozilla/5.0 (Windows; U; Windows NT 5.1; zh-CN) AppleWebKit/523.15 (KHTML, like Gecko, Safari/419.3) Arora/0.3 (Change: 287 c9dfb30)",
    "Mozilla/5.0 (X11; U; Linux; en-US) AppleWebKit/527+ (KHTML, like Gecko, Safari/419.3) Arora/0.6",
    "Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US; rv:1.8.1.2pre) Gecko/20070215 K-Ninja/2.1.1",
    "Mozilla/5.0 (Windows; U; Windows NT 5.1; zh-CN; rv:1.9) Gecko/20080705 Firefox/3.0 Kapiko/3.0",
    "Mozilla/5.0 (X11; Linux i686; U;) Gecko/20070322 Kazehakase/0.4.5",
    "Mozilla/5.0 (X11; U; Linux i686; en-US; rv:1.9.0.8) Gecko Fedora/1.9.0.8-1.fc10 Kazehakase/0.5.6",
    "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/535.11 (KHTML, like Gecko) Chrome/17.0.963.56 Safari/535.11",
    "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_3) AppleWebKit/535.20 (KHTML, like Gecko) Chrome/19.0.1036.7 Safari/535.20",
    "Opera/9.80 (Macintosh; Intel Mac OS X 10.6.8; U; fr) Presto/2.9.168 Version/11.52",
]


USER_AGENTS = [
    "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; AcooBrowser; .NET CLR 1.1.4322; .NET CLR 2.0.50727)",
    "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 6.0; Acoo Browser; SLCC1; .NET CLR 2.0.50727; Media Center PC 5.0; .NET CLR 3.0.04506)",
    "Mozilla/4.0 (compatible; MSIE 7.0; AOL 9.5; AOLBuild 4337.35; Windows NT 5.1; .NET CLR 1.1.4322; .NET CLR 2.0.50727)",
    "Mozilla/5.0 (Windows; U; MSIE 9.0; Windows NT 9.0; en-US)",
    "Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; Win64; x64; Trident/5.0; .NET CLR 3.5.30729; .NET CLR 3.0.30729; .NET CLR 2.0.50727; Media Center PC 6.0)",
    "Mozilla/5.0 (compatible; MSIE 8.0; Windows NT 6.0; Trident/4.0; WOW64; Trident/4.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NET CLR 3.0.30729; .NET CLR 1.0.3705; .NET CLR 1.1.4322)",
    "Mozilla/4.0 (compatible; MSIE 7.0b; Windows NT 5.2; .NET CLR 1.1.4322; .NET CLR 2.0.50727; InfoPath.2; .NET CLR 3.0.04506.30)",
    "Mozilla/5.0 (Windows; U; Windows NT 5.1; zh-CN) AppleWebKit/523.15 (KHTML, like Gecko, Safari/419.3) Arora/0.3 (Change: 287 c9dfb30)",
    "Mozilla/5.0 (X11; U; Linux; en-US) AppleWebKit/527+ (KHTML, like Gecko, Safari/419.3) Arora/0.6",
    "Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US; rv:1.8.1.2pre) Gecko/20070215 K-Ninja/2.1.1",
    "Mozilla/5.0 (Windows; U; Windows NT 5.1; zh-CN; rv:1.9) Gecko/20080705 Firefox/3.0 Kapiko/3.0",
    "Mozilla/5.0 (X11; Linux i686; U;) Gecko/20070322 Kazehakase/0.4.5",
    "Mozilla/5.0 (X11; U; Linux i686; en-US; rv:1.9.0.8) Gecko Fedora/1.9.0.8-1.fc10 Kazehakase/0.5.6",
    "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/535.11 (KHTML, like Gecko) Chrome/17.0.963.56 Safari/535.11",
    "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_3) AppleWebKit/535.20 (KHTML, like Gecko) Chrome/19.0.1036.7 Safari/535.20",
    "Opera/9.80 (Macintosh; Intel Mac OS X 10.6.8; U; fr) Presto/2.9.168 Version/11.52",
]

if __name__=="__main__":
    def process_request(self, request, spider):
        request.headers["User-Agent"]=random.choice(USER_AGENTS)

python 有一个现成的随机生成UA(user-agent)的第三方库：fake-useragent 直接：pip install
fake-useragent 即可。 使用：

    from fake_useragent import UserAgent
       ua = UserAgnet()
       ua.random
```

##### Urllib库详解
http://www.bkjia.com/Pythonjc/1043449.html
http://blog.csdn.net/drdairen/article/details/51149498
http://www.bijishequ.com/detail/441751?p=


##### 简单爬虫
```
import urllib.request

page_id = 19523
pan_url = 'http://mebook.cc/download.php?id={}'.format(page_id)
pan_url = 'http://mebook.cc/download.php?id=536'
pan_url = 'http://mebook.cc/page/1'
pan_url = 'http://mebook.cc/download.php?id=16835'

url_request = urllib.request.Request(pan_url)
url_request.add_header('User-agent', 'Mozilla/5.0')
url_open = urllib.request.urlopen(url_request)
html_doc = url_open.read().decode('utf-8')
print(html_doc)

for page_index in range(1, 10):
    pan_url = 'http://mebook.cc/page/{}'.format(page_index)
    url_request = urllib.request.Request(pan_url)
    url_request.add_header('User-agent', 'Mozilla/5.0')
    url_open = urllib.request.urlopen(url_request)
    html_doc = url_open.read().decode('utf-8')
    print(html_doc)


import re
import random
import urllib.request

pan_url = 'http://mebook.cc/'

UserAgentList = ['Mozilla/5.0 (Windows NT 6.1; rv:28.0) Gecko/20100101 Firefox/28.0',
                 'Mozilla/5.0 (X11; Linux i686; rv:30.0) Gecko/20100101 Firefox/30.0',
                 'Mozilla/5.0 (Windows NT 5.1; rv:31.0) Gecko/20100101 Firefox/31.0',
                 'Mozilla/5.0 (Windows NT 6.1; WOW64; rv:33.0) Gecko/20100101 Firefox/33.0',
                 'Mozilla/5.0 (Windows NT 10.0; WOW64; rv:40.0) Gecko/20100101 Firefox/40.0',
                 'Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; Trident/5.0)',
                 'Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; WOW64; Trident/5.0; SLCC2; Media Center PC 6.0; '
                 'InfoPath.3; MS-RTC LM 8; Zune 4.7)',
                 'Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.1; Trident/6.0)',
                 'Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.1; WOW64; Trident/6.0)',
                 'Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.2; Win64; x64; Trident/6.0)',
                 'Mozilla/5.0 (IE 11.0; Windows NT 6.3; Trident/7.0; .NET4.0E; .NET4.0C; rv:11.0) like Gecko',
                 'Mozilla/5.0 (IE 11.0; Windows NT 6.3; WOW64; Trident/7.0; Touch; rv:11.0) like Gecko',
                 'Mozilla/5.0 (Windows NT 6.3; WOW64) AppleWebKit/537.36 '
                 '(KHTML, like Gecko) Chrome/30.0.1599.101 Safari/537.36',
                 'Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 '
                 '(KHTML, like Gecko) Chrome/31.0.1623.0 Safari/537.36',
                 'Mozilla/5.0 (Windows NT 6.2; WOW64) AppleWebKit/537.36 '
                 '(KHTML, like Gecko) Chrome/34.0.1847.116 Safari/537.36',
                 'Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 '
                 '(KHTML, like Gecko) Chrome/37.0.2062.103 Safari/537.36',
                 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_2) AppleWebKit/537.36 '
                 '(KHTML, like Gecko) Chrome/40.0.2214.38 Safari/537.36',
                 'Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 '
                 '(KHTML, like Gecko) Chrome/46.0.2490.71 Safari/537.36',
                 'Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 '
                 '(KHTML, like Gecko) Chrome/51.0.2704.103 Safari/537.36']

url_request = urllib.request.Request(pan_url)
# url_request.add_header('User-agent', 'Mozilla/5.0')
url_request.add_header('User-Agent', random.choice(UserAgentList))
url_open = urllib.request.urlopen(url_request)
html_doc = url_open.read().decode('utf-8')
print(html_doc)

match_obj = re.search(r'title=\'最末页\'>(\d+)</a>', str(html_doc))

if match_obj:
    max_page_num = int(match_obj.group(1))
    print('max page number: {}'.format(max_page_num))

```

##### 爬虫入门
http://yshblog.com/blog/148
http://blog.csdn.net/column/details/why-bug.html
http://blog.csdn.net/Eastmount/article/category/5758691
http://zihaolucky.github.io/using-python-to-build-zhihu-cralwer/
https://www.zhihu.com/question/20899988
https://www.zhihu.com/question/21358581
https://segmentfault.com/a/1190000009111635
http://docs.python-requests.org/zh_CN/latest/user/quickstart.html
http://www.cnblogs.com/yizhenfeng168/p/7078480.html

##### Python爬虫技巧
http://blkstone.github.io/2016/03/02/crawler-anti-anti-cheat/
http://gohom.win/2016/01/21/proxy-py/
http://ningning.today/2015/10/04/python/Python%E7%88%AC%E8%99%AB%E7%9A%84%E4%B8%80%E4%BA%9B%E6%80%BB%E7%BB%93/
http://hamstersi.com/2017/08/Python%E7%88%AC%E8%99%AB%EF%BC%9A%E4%B8%80%E4%BA%9B%E5%B8%B8%E7%94%A8%E7%9A%84%E7%88%AC%E8%99%AB%E6%8A%80%E5%B7%A7%E6%80%BB%E7%BB%93/

http://java.ctolib.com/hellysmile-fake-useragent.html
https://github.com/jhao104/proxy_pool
http://zqdevres.qiniucdn.com/data/20130909104216/index.html

https://www.zhihu.com/topic/19577498
https://www.zhihu.com/question/35461941
https://github.com/lining0806/PythonSpiderNotes

##### 爬虫与反爬虫
https://zhuanlan.zhihu.com/p/20520370
https://www.zhihu.com/question/28168585
https://www.zhihu.com/question/26221432

##### BeautifulSoup教程
http://beautifulsoup.readthedocs.io/zh_CN/latest/
https://www.gitbook.com/book/wizardforcel/bs4-doc/details
https://www.crifan.com/files/doc/docbook/python_topic_beautifulsoup/release/pdf/python_topic_beautifulsoup.pdf
http://www.jianshu.com/p/154211515a41

##### Scrapy教程
http://scrapy-chs.readthedocs.io/zh_CN/latest/index.html

##### 爬虫实战项目
http://www.jianshu.com/p/78684e5a7916
https://zhuanlan.zhihu.com/p/25172216
http://python.jobbole.com/88325/
http://yz0515.com/2017/03/29/%E7%88%AC%E8%99%AB%E5%AE%9E%E6%88%98%E2%80%94%E2%80%94%E5%B0%86%E5%BB%96%E9%9B%AA%E5%B3%B0%E7%9A%84%E6%95%99%E7%A8%8B%E8%BD%AC%E6%8D%A2%E6%88%90PDF%E7%94%B5%E5%AD%90%E4%B9%A6/

##### 搜索引擎蜘蛛爬虫User Agent一览
http://www.wilf.cn/post/search-engine-bots.html
```
今天分析研究了两个网站的 Apache 日志，分析日志虽然很无聊，但却是很有意义的事情，比如跟踪 SPAM 的 User Agent。顺便整理出一些搜索引擎爬虫的 User Agent，在这里分享一下，也欢迎补充。
微软

“msnbot-media/1.1 (+http://search.msn.com/msnbot.htm)”
msnbot，大多数已经被bingbot替代了，现在偶尔还可以看到。

“Mozilla/5.0 (compatible; bingbot/2.0; +http://www.bing.com/bingbot.htm)”
bing，必应
搜搜

“Sosospider+(+http://help.soso.com/webspider.htm)”
腾讯搜搜

“Sosoimagespider+(+http://help.soso.com/soso-image-spider.htm)”
搜搜图片
雅虎

“Mozilla/5.0 (compatible; Yahoo! Slurp; http://help.yahoo.com/help/us/ysearch/slurp)”
雅虎英文

“Yahoo! Slurp China”
“Mozilla/5.0 (compatible; Yahoo! Slurp China; http://misc.yahoo.com.cn/help.html)”
雅虎中国
搜狗

“http://pic.sogou.com” “Sogou Pic Spider/3.0(+http://www.sogou.com/docs/help/webmasters.htm#07)”
搜狗图片

“Sogou web spider/4.0(+http://www.sogou.com/docs/help/webmasters.htm#07)”
搜狗，搜狗的蜘蛛程序做的很不好，总是进入死循环，已经分别在 robots.txt 和 设置中屏蔽掉

Google

“Mozilla/5.0 (compatible; Googlebot/2.1; +http://www.google.com/bot.html)”
Google

“Googlebot-Image/1.0”
Google图片搜索

“Mediapartners-Google”
未知

“FeedBurner/1.0 (http://www.FeedBurner.com)”
feedburner

“AdsBot-Google-Mobile (+http://www.google.com/mobile/adsbot.html) Mozilla (iPhone; U; CPU iPhone OS 3 0 like Mac OS X) AppleWebKit (KHTML, like Gecko) Mobile Safari”
Adwords移动网络
百度

“Baiduspider-image+(+http://www.baidu.com/search/spider.htm)”
百度图片

“Mozilla/5.0 (compatible; Baiduspider/2.0; +http://www.baidu.com/search/spider.html)”
亲爱的百度蜘蛛

“Mozilla/5.0 (Windows; U; Windows NT 5.1; zh-CN; rv:1.9.2.8;baidu Transcoder) Gecko/20100722 Firefox/3.6.8 ( .NET CLR 3.5.30729)”
baidu+Transcoder 是用户用手机浏览网站留下的记录，Transcoder 是代码转换器，把网站转码成手机用户上网看到的网页留下的记录
360

Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; Trident/5.0); 360Spider
360搜索
其他搜索引擎

“Mozilla/5.0 (compatible; YoudaoBot/1.0; http://www.youdao.com/help/webmaster/spider/; )”
网易有道

“Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US) Speedy Spider (http://www.entireweb.com/about/search_tech/speedy_spider/)”
来自瑞典的搜索引擎，网站看起来很不错，http://www.entireweb.com

“jikespider \”Mozilla/5.0”
即刻搜索，原人民搜索，搜索引擎国家队，已倒闭

“Mozilla/5.0 (compatible; YandexBot/3.0; +http://yandex.com/bots)”
俄罗斯yandex

Mozilla/5.0 (compatible; EasouSpider; +http://www.easou.com/search/spider.html)
宜搜，不认识，一直不停抓取，已屏蔽
其他已知bot

“HuaweiSymantecSpider/1.0+DSE-support@huaweisymantec.com+(compatible; MSIE 7.0; Windows NT 5.1; Trident/4.0; .NET CLR 2.0.50727; .NET CLR 3.0.4506.2152; .NET CLR ; http://www.huaweisymantec.com/cn/IRL/spider)”
华为赛门铁克蜘蛛，是华为赛门铁克科技有限公司网页信誉分析系统的一个页面爬取程序，其作用是用于爬取互联网网页并进行信誉分析，从而检查该网站上的是否含有恶意代码。
http://baike.baidu.com/view/5994606.htm

qiniu-imgstg-spider-1.0
七牛镜像蜘蛛

“xFruits/1.0 (http://www.xfruits.com)”
xFruits，聚合rss用的

Feedly/1.0 (+http://www.feedly.com/fetcher.html; like FeedFetcher-Google)
Feedly，Google Reader 关闭后一直用这个

Mozilla/5.0 (compatible;YoudaoFeedFetcher/1.0;http://www.youdao.com/help/reader/faq/topic006/;1 subscribers;)
有道阅读

FeedDemon/4.5 (http://www.feeddemon.com/; Microsoft Windows)
一款离线RSS阅读器

“Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; JianKongBao Monitor 1.1)”
监控宝

DNSPod-Monitor/2.0
DNSPod监控

“Mozilla 5.0 (compatible; Feedsky crawler /1.0; http://www.feedsky.com)”
Feedsky

“Xianguo.com 1 Subscribers”
鲜果

360spider(http://webscan.360.cn)
360网站安全检测

“yrspider Mozilla/5.0 (compatible; YRSpider; +http://www.yunrang.com/yrspider.html)”
云壤公司，http://www.yunrang.com/yrspider.html
其他未知bot

“Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1; EmbeddedWB 14.52 from: http://www.bsalsa.com/ EmbeddedWB 14.52; .NET CLR 2.0.50727)”
怀疑为发布SPAM用的，因为总是在获取注册页面和验证码

Mozilla/5.0 (compatible; LinkpadBot/1.06; +http://www.linkpad.ru)
LinkpadBot，看域名知道是来自俄罗斯的

Mozilla/5.0 (compatible; SISTRIX Crawler; http://crawler.sistrix.net/)
又一个国外的

“Mozilla/5.0 (compatible; MJ12bot/v1.4.0; http://www.majestic12.co.uk/bot.php?+)”
来自英国的未知bot

“Mozilla/5.0 (compatible; Ezooms/1.0; ezooms.bot@gmail.com)”
未知

“IS Alpha/Nutch-1.1”
未知

Nutch Spider/Nutch-2.2.1
貌似是上面那个进化来的

“BlogPulseLive (support@blogpulse.com)”

“findlinks/2.0.2 (+http://wortschatz.uni-leipzig.de/findlinks/)”
来自德国的未知bot

“Mozilla/4.0 (compatible; MSIE 6.0; AugustBot/augstbot@163.com)”
未知，貌似与网易有关

“InternetSeer.com”
未知

“Mozilla/5.0 (compatible; DotBot/1.1; http://www.dotnetdotcom.org/, crawler@dotnetdotcom.org)”
未知，已更新为下面的

Mozilla/5.0 (compatible; DotBot/1.1; http://www.opensiteexplorer.org/dotbot, help@moz.com)
DotBot，不认识

“http://www.internet-zarabotok.net/” “Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.2; Win64; AMD64)”
来自俄罗斯的未知bot

Mozilla/5.0 (X11; U; Linux x86_64; en-US; rv:1.9.0.19; aggregator:Spinn3r (Spinn3r 3.1); http://spinn3r.com/robot) Gecko/2010040121 Firefox/3.0.19
Spinn3r，不认识

Mozilla/5.0 (compatible; Exabot/3.0; +http://www.exabot.com/go/robot)
Exabot，还是不认识

Mozilla/5.0 (compatible; Exabot/3.0 (BiggerBetter); +http://www.exabot.com/go/robot)
Exabot，不认识

psbot/0.1 (+http://www.picsearch.com/bot.html)
psbot，不认识

TurnitinBot/3.0 (http://www.turnitin.com/robot/crawlerinfo.html)
TurnitinBot，不认识
```

##### 爬虫与正则表达式
```
import re
import urllib.request

pan_url = 'http://mebook.cc/download.php?id=6064'
pan_url = 'http://mebook.cc/6064.html'
pan_url = 'http://mebook.cc/download.php?id=7456'

url_request = urllib.request.Request(pan_url)
url_request.add_header('User-agent', 'Mozilla/5.0')
url_open = urllib.request.urlopen(url_request)
html_doc = url_open.read().decode('utf-8')
print(html_doc)

match_obj = re.search(r'下载列表\s*：\s*<a\s*href=\"\s*(http[s]*://pan.baidu.com/s/\w+)\s*\w*\"\s*target=\"\w+\">百度网盘', html_doc)
print(match_obj.group(1))

match_obj = re.search(r'网盘密码\s*：\s*百度网盘密码\s*：\s*[密码: ]*\s*(\w{4})', html_doc)
print(match_obj.group(1))

html_doc = '''<div class="desc">
<h3>下载文件资源信息</h3>
<p>文件名称：《徐志摩全集(1-6)(套装共6册) 》</p>
<p>文件大小：</p>
<p>适用版本：</p>
<p>更新日期：2016.8.27</p>
<p>作者信息：</p>
<p>网盘密码：百度网盘密码：密码: kdus&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</p>
<p></p>
</div>
<div class="clear"></div>
<div class="list">
        下载列表：<a href="https://pan.baidu.com/s/1bpgIMNP " target="_blank">百度网盘</a></div>
<div class="clear"></div>

<div class="desc" style="border:none">'''
# html_doc = '<p>网盘密码：百度网盘密码：密码：kdus&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</p>'
# match_obj = re.search(r'网盘密码\s*：\s*百度网盘密码\s*：\s*(?:密码: )?\s*(\w{4})', html_doc)
# match_obj = re.search(r'网盘密码\s*：\s*百度网盘密码\s*：\s*(?:密码)?(?:：|:)?\s*(\w{4})', html_doc)
match_obj = re.search(r'网盘密码\s*：\s*百度网盘密码\s*：\s*(?:密码)?[：|:]?\s*(\w{4})', html_doc)
print(match_obj.group(1))


html_doc = '''<div id="content">
<p><img src="http://mebook.cc/wp-content/uploads/2016/11/36381479124678.jpg"/></p>
<h2>内容简介：</h2>
<p><span style="font-family: 微软雅黑, &#39;Microsoft YaHei&#39;; font-size: 18px;">诞生于1000年前日本平安时代的《源氏物语(插图典藏版)》，是世界上最早的小说。它以一种贵族化的华丽、唯美，以及史学家般的恢弘，向我们讲述了一段流传千年、以源氏为主的四代人与众多女子的伤感爱情故事，也展开了一幅平安时代的社会风貌、自然景观和贵族们华丽奢靡的生活画卷，体现出日本民族特有的“物哀”之美。同时，书中选用了《源氏物语绘卷》《洛中洛外图屏风》等众多日本国宝级绘画作品，并运用现代图解手法，生动地展示了那个时代的风情风貌，以及那些不为人知的、隐藏的细节，使读者能够更深入地了解一个与现代不同的日本。</span></p>
<p><span style="font-family: 微软雅黑, &#39;Microsoft YaHei&#39;; font-size: 18px;">[idl id=下载 t=进入下载列表]<a href="http://pan.baidu.com/s/1hsLUkhY" target="_blank">百度网盘</a>(提取码：rmsi)|<a href="http://download.cloud.189.cn/v5/downloadFile.action?downloadRequest=1_DBD790DAAC93CCAFFC32C4D1AC385C2CC3947B6342479BEEFD9C8105E0F42593335F37FA44DC4DE096F07C8FE03C54B6F3C27AA2EF0E1F741A19AC1041846A2D15D8907CAE136C593799EAC0BC6FFD23B3974CCC71127CBFB1563C480600C2566BA31E04509A3E67B9D8CDC67E43C7D244633840C56683FA3CD3CB359E6589552A610603" target="_self">epub</a>|<a href="http://download.cloud.189.cn/v5/downloadFile.action?downloadRequest=1_7D6AC6D1567CB47A3D81EF4E0795625DBE5FDA234F8A6F5CF0428E655D70F19272827A99613C765C4691F736CFD067EBFF08D69E6992677244703C204C8599398EC2AE3EA92232060720D49147FD21EF300134FFAAB534BB8E3B9FC378014D2F6B0A7D8936987E8E44741F38D816A113458C140FF816DCA83A1FAFE477DDFFD935A72EE6" target="_self">mobi</a>|<a href="http://download.cloud.189.cn/v5/downloadFile.action?downloadRequest=1_B9B57AB5491EB66A3C4C5E16956D1AE4673ED6E339D215CF9A864D16D2AF22DC0E6E4CCC1DC2046931D5D686783C168C92B074238D4C9A0C3CE637ADDFEAD002D9F4E160FB96E30D485579930FFF2FECBA27C656DB4C79B54EBA45CDD887FFFAB9AF695B4367C20F087D816FF17B72AD9C90050AC8F885B8B3CFE9E5C2CEC6FAED7645B6" target="_self">azw3</a>|<a href="http://cloud.189.cn/t/q6zuAzBriq6n" target="_blank">天翼云盘</a>(访问码:6425)[/idl]</span></p>
<p></p>
</div>'''

html_doc = '''<p><span style="font-family: 微软雅黑, &quot;Microsoft YaHei&quot;; font-size: 18px;">[idl id=下载 t=进入下载列表]<a href="http://pan.baidu.com/s/1pLIrTSB" target="_blank" style="color: rgb(84, 141, 212); text-decoration: underline;"><span style="font-family: 微软雅黑, &quot;Microsoft YaHei&quot;; font-size: 18px; color: rgb(84, 141, 212);">百度网盘</span></a><span style="font-family: 微软雅黑, &quot;Microsoft YaHei&quot;; font-size: 18px; color: rgb(84, 141, 212);">(提取码：7uwd)|</span><a href="http://download.cloud.189.cn/v5/downloadFile.action?downloadRequest=1_F7C626497FD27A70D2852700C441DC1250B7EBCC9B4E838AD4D02332611E2AF8F60DF399B7605D56DDE7D9D60AF747412D9DB70FEAB95AD98C67BC2F83F8F905CCED31D94FE64C1E3DF6B54BDFC82BE1CFA4DF7018C609002BA2B385C2E9C2367D4757537587980D661501C4A5817524DD1251B9B423D7BD83FC771CED435C2D96F435E0" target="_self" style="color: rgb(84, 141, 212); text-decoration: underline;"><span style="font-family: 微软雅黑, &quot;Microsoft YaHei&quot;; font-size: 18px; color: rgb(84, 141, 212);">epub</span></a><span style="font-family: 微软雅黑, &quot;Microsoft YaHei&quot;; font-size: 18px; color: rgb(84, 141, 212);">|</span><a href="http://download.cloud.189.cn/v5/downloadFile.action?downloadRequest=1_A123400A335DD70D3BCDAA76491AD90030AE4F1B12ED0ED8E4C127720F7372D2DC3EF08C3781258DB2A0032B126AF9E1B4CF3B4C8DCFB45EE856B19A8D20C6FB59013C38DF1CDE9CC93DAF79BCDD6D681BEB71E15F81C8267B5E42229E88A4304E3EB2693E1DA97264EFD98B1811888657FC127D187C3D530D8F9096514DEA9A9B6FD965" target="_self" style="color: rgb(84, 141, 212); text-decoration: underline;"><span style="font-family: 微软雅黑, &quot;Microsoft YaHei&quot;; font-size: 18px; color: rgb(84, 141, 212);">mobi</span></a><span style="font-family: 微软雅黑, &quot;Microsoft YaHei&quot;; font-size: 18px; color: rgb(84, 141, 212);">|</span><a href="http://download.cloud.189.cn/v5/downloadFile.action?downloadRequest=1_CF93663014530A9A4744DB3208C6791939D4953FC7ED1DE1AC1E915F905A572A186DBC4B9E1047832FE06CC45652457FE21A97CAF7026492561ADA2AE6B8A4180FF95C25190EB5FB588F864A2E3654B716733B470C9706A7596345B1B67C5D0F98E9FEC57A5AB8CE1E96C1EABE687F3EF4DAC5B4A57AC295CDA689DCB4B7A0E1C953DCC2" target="_self" style="color: rgb(84, 141, 212); text-decoration: underline;"><span style="font-family: 微软雅黑, &quot;Microsoft YaHei&quot;; font-size: 18px; color: rgb(84, 141, 212);">azw3</span></a>[/idl]</span></p>
<p></p>
</div>'''

match_obj = re.search(r'\"(http[s]*://pan.baidu.com/s/\w+)\s*\w*\"\s*target=\"\w+\"', html_doc)
print(match_obj.group(1))

match_obj = re.search(r'提取码\s*：\s*(\w{4})', html_doc)
print(match_obj.group(1))
```