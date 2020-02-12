---
title: python简单爬虫
date: 2019-12-03 19:36:25
tags:
	- pyhton
	- 爬虫
categories:
	- python
---
# 1、python爬虫下载器

## 1、requests模块

### 1、先确定要抓取的网站的地址url

### 2、对url发起请求并获取响应(网页的源代码)

### 3、requests.get()方法

#### 对网页发起请求并获取响应信息

#### requests.get(url,headers={},params={})

#### url:请求的网页的地址

```python
import requests


url="https://www.baidu.com/"  #确定抓取网页的url
res=requests.get(url)  # 对网页发起请求并获取响应信息
res.encoding="utf-8"
html=res.text #解析得到的相应内容
print(html)
```

#### headers:请求携带的浏览器以及操作系统信息

```python
import requests


url="https://www.baidu.com/"  #确定抓取网页的url
headers={"User-Agent":"Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/75.0.3770.142 Safari/537.36"}
res=requests.get(url,headers=headers)  # 对网页发起请求并获取响应信息
res.encoding="utf-8"
html=res.text #解析得到的相应内容
print(html)
```

#### params:请求携带参数的字典

#### 模拟登陆：登陆账号之后寻找登陆的请求，找到用户的cookie信息，然后让请求携带这个信息去请求网页

```python
import requests

url="https://www.baidu.com/s?"
headers={"User-Agent":"Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/534.50 (KHTML, like Gecko) Version/5.1 Safari/534.50",
         "Cookie":"BIDUPSID=20BA20A6474681053EA56436BC4B3D97; PSTM=1574518658; BAIDUID=9276E50B9B762C87B246AFFF86AFE4CB:FG=1; BD_UPN=12314753; ispeed_lsm=2; BDORZ=B490B5EBF6F3CD402E515D22BCDA1598; COOKIE_SESSION=25_0_9_6_9_8_0_0_9_5_3_0_0_0_0_0_1575166622_0_1575337152%7C9%230_0_1575337152%7C1; H_PS_645EC=326b1bFfVwAZMn%2BEr2lUzz5jDYz09GAGHFBdUD0mYZboAS5tNtdv1A7yck4; delPer=0; BDUSS=FpvfnhINXpMeldCMU5NRDQ0STdRNi1QS2RLaDFKSTZHcnR2aEJLZmVxZWpUUTFlRUFBQUFBJCQAAAAAAAAAAAEAAAA2JBrPZmx50sHA-9ChuOe45wAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAKPA5V2jwOVdb; BD_HOME=1; H_PS_PSSID=1438_21105_30210_20698_22159"}
params={
    "wd":"篮球"
}
res=requests.get(url,headers=headers,params=params)
res.encoding="utf-8"
html=res.text
print(res.url) #返回请求的真实url地址
print(html)
```
<!-- more -->
# 2、range()函数

### 整数迭代生成器

```python
import requests

url="https://www.baidu.com/s?"
headers={"User-Agent":"Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/534.50 (KHTML, like Gecko) Version/5.1 Safari/534.50",
         "Cookie":"BIDUPSID=20BA20A6474681053EA56436BC4B3D97; PSTM=1574518658; BAIDUID=9276E50B9B762C87B246AFFF86AFE4CB:FG=1; BD_UPN=12314753; ispeed_lsm=2; BDORZ=B490B5EBF6F3CD402E515D22BCDA1598; COOKIE_SESSION=25_0_9_6_9_8_0_0_9_5_3_0_0_0_0_0_1575166622_0_1575337152%7C9%230_0_1575337152%7C1; H_PS_645EC=326b1bFfVwAZMn%2BEr2lUzz5jDYz09GAGHFBdUD0mYZboAS5tNtdv1A7yck4; delPer=0; BDUSS=FpvfnhINXpMeldCMU5NRDQ0STdRNi1QS2RLaDFKSTZHcnR2aEJLZmVxZWpUUTFlRUFBQUFBJCQAAAAAAAAAAAEAAAA2JBrPZmx50sHA-9ChuOe45wAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAKPA5V2jwOVdb; BD_HOME=1; H_PS_PSSID=1438_21105_30210_20698_22159"}
for page in range(1,5):
    pn=(page-1)*10  #构造翻页参数的值
    params={
        "wd":"篮球",
        "pn":str(pn)
    }
    res=requests.get(url,headers=headers,params=params)
    res.encoding="utf-8"
    html=res.text
    print(res.url) #返回请求的真实url地址
    print(html)
```

# 3、起点小说

```python
import requests
from user_headers import L
import random

url="https://www.qidian.com/all?"
headers={"User-Agent":random.choice(L)}
for page in range(1,5):
    params={
        "page":str(page)
    }
    res=requests.get(url,headers=headers,params=params)
    res.encoding="utf-8"
    html=res.text
    filenmae="第"+str(page)+"页.html"
    with open(filenmae,"w",encoding="utf-8") as f:
        f.write(html)
        print(filenmae,"下载成功！")
```

# 4、解析模块

### 正则表达式

### bs4

### xpath表达式

# 5、正则表达式

## import re  导入正则表达式模块

## 1、re.match()方法

### 从字符串的开头进行匹配，返回符合正则表达式的数据

#### 如果字符串的开头和正则表达式不匹配的话，直接返回None对象

| 元字符 | 作用                                 |
| ------ | ------------------------------------ |
| \s     | 匹配一个空白字符                     |
| \w     | 匹配字母数字下划线普通字符           |
| \W     | 匹配特殊字符                         |
| \d     | 匹配一个数字                         |
| .      | 代表匹配任意字符(\n除外)             |
| +      | 匹配前面的表达式多次                 |
| {m}    | 精确匹配前面的表达式m次              |
| ?      | 非贪婪匹配                           |
| ()     | 分组(想要什么数据就给什么数据加括号) |
| *      | 匹配出现1次或任意次的字符            |
| ^      | 从头开始匹配                         |
| $      | 匹配到末尾结束                       |

```python
import re

s="hello world 1234 5678 你好"
# result=re.match('^h\w\w\w\w\s\w{5}',s)
# result=re.match('^h(\w{4}\s\w{5})\s(\d{4}\s\d{4})',s)
result=re.search('^h.*',s)
print(result.group())
```

## 2、贪婪匹配与非贪婪匹配

### 贪婪匹配:在正则表达式匹配成功的前提下，尽可能多的匹配数据(.*)

### 非贪婪匹配:在正则表达式匹配成功的前提下，尽可能少的匹配数据(.*?)

```python
import re

s="hello world 12345678 你好"
# result=re.match('^h\w\w\w\w\s\w{5}',s)
# result=re.match('^h(\w{4}\s\w{5})\s(\d{4}\s\d{4})',s)
# result=re.search('^h.*',s)
result=re.match('^h(.*?)(\d+)',s)
print(result.group(1))
print(result.group(2))
```

## 3、search()方法

### 扫描整个字符串，返回第一个符合正则表达式的数据

```python
result=re.search('\w\s',s)
print(result.group())
```

#### 如果字符串中有多个区间满足正则表达式，也只能返回第一个满足的数据

## 4、findall()方法

### 扫描整个字符串，返回所有满足正则表达式的数据列表

### findall里没有group()方法

```python
result=re.findall('\w\s',s)
print(result)
```

## 5、标志位

### 正则表达式可以通过一些标志位来满足一些特殊的需求

#### re.S 代表可以进行多行匹配

```python
result=re.findall('.*',s,re.S)
print(result)
```

## 6、re.compile()

### 将字符串编译为一个正则表达式对象

```python
p=re.compile('.*',re.S)
result=re.findall(p,s)
print(result)
```

# 6、起点小说解析

```python
import re

html="""
<div class="book-mid-info">
                    <h4><a href="//book.qidian.com/info/1004608738" target="_blank" data-eid="qd_B58" data-bid="1004608738">圣墟</a></h4>
                    <p class="author">
                        <img src="//qidian.gtimg.com/qd/images/ico/user.f22d3.png"><a class="name" href="//my.qidian.com/author/4362453" data-eid="qd_B59" target="_blank">辰东</a><em>|</em><a href="//www.qidian.com/xuanhuan" target="_blank" data-eid="qd_B60">玄幻</a><i>·</i><a class="go-sub-type" data-typeid="21" data-subtypeid="8" href="javascript:" data-eid="qd_B61">东方玄幻</a><em>|</em><span>连载</span>
                        
                    </p>
                    <p class="intro">
                        在破败中崛起，在寂灭中复苏。沧海成尘，雷电枯竭，那一缕幽雾又一次临近大地，世间的枷锁被打开了，一个全新的世界就此揭开神秘的一角……
                    </p>
                    <p class="update"><span><style>@font-face { font-family: CjUTgyWy; src: url('https://qidian.gtimg.com/qd_anti_spider/CjUTgyWy.eot?') format('eot'); src: url('https://qidian.gtimg.com/qd_anti_spider/CjUTgyWy.woff') format('woff'), url('https://qidian.gtimg.com/qd_anti_spider/CjUTgyWy.ttf') format('truetype'); } .CjUTgyWy { font-family: 'CjUTgyWy' !important;     display: initial !important; color: inherit !important; vertical-align: initial !important; }</style><span class="CjUTgyWy"></span>万字</span>
                        
                    </p>
                </div>
"""
p=re.compile('<div class="book-mid-info">.*?data-bid.*?>(.*?)</a>.*?class="intro">(.*?)</p>',re.S)
data=re.findall(p,html)
print(data)
```

#### 面向对象

```python
import requests
import re
from user_headers import L
import random

class Qidian:
    def __init__(self):
        self.url = "https://www.qidian.com/all?"
        self.headers = {"User-Agent": random.choice(L)}

    def change_page(self):  # 进行翻页的函数
        for page in range(1,5):
            params={
                "page":str(page)
            }
            self.get_html(params)  # 调用获取网页源代码的函数

    def get_html(self,params):  # 获取网页源代码的函数
        res=requests.get(self.url,headers=self.headers,params=params)
        res.encoding="utf-8"
        html=res.text
        self.get_data(html)  # 调用解析数据的函数

    def get_data(self,html):  # 解析网页数据的函数
        p = re.compile('<div class="book-mid-info">.*?data-bid.*?>(.*?)</a>.*?class="intro">(.*?)</p>', re.S)
        data = re.findall(p, html)
        print(data)


    def save_data(self):  # 保存数据的函数
        pass

qidian=Qidian()
qidian.change_page()
```

# 7、csv文件的操作

```python
import csv

L=["小明","20","男"]
L1=["小红","25","女"]
with open("data.csv","w",encoding="utf-8",newline="") as f: #newline参数是为了防止出现空行
    writer=csv.writer(f)  #创建写入对象
    writer.writerow(L)
    writer.writerow(L1)
```

```python
import requests
import re
from user_headers import L
import random
import csv

class Qidian:
    def __init__(self):
        self.url = "https://www.qidian.com/all?"
        self.headers = {"User-Agent": random.choice(L)}

    def change_page(self):  # 进行翻页的函数
        with open("xiaoshuo.csv", "a", encoding="utf-8", newline="") as f:
            writer = csv.writer(f)
            writer.writerow(["小说名称","小说简介"])
        for page in range(1,5):
            params={
                "page":str(page)
            }
            self.get_html(params)  # 调用获取网页源代码的函数

    def get_html(self,params):  # 获取网页源代码的函数
        res=requests.get(self.url,headers=self.headers,params=params)
        res.encoding="utf-8"
        html=res.text
        self.get_data(html)  # 调用解析数据的函数

    def get_data(self,html):  # 解析网页数据的函数
        p = re.compile('<div class="book-mid-info">.*?data-bid.*?>(.*?)</a>.*?class="intro">(.*?)</p>', re.S)
        data = re.findall(p, html)
        self.save_data(data) #调用保存数据的函数

    def save_data(self,data):  # 保存数据的函数
        for i in data:
            title=i[0]  #获取小说的名称
            text=i[1].strip()  #获取小说的简介 strip()代表去掉字符串两边的空白字符以及换行符
            content=[title,text] #创建写入csv文件的数据列表
            with open("xiaoshuo.csv","a",encoding="utf-8",newline="") as f:
                writer=csv.writer(f)
                writer.writerow(content)
                print("数据写入成功！")


qidian=Qidian()
qidian.change_page()
```

# 8、猫眼电影

```python
html="""
<div class="movie-item-info">
        <p class="name"><a href="/films/1203" title="霸王别姬" data-act="boarditem-click" data-val="{movieId:1203}">霸王别姬</a></p>
        <p class="star">
                主演：张国荣,张丰毅,巩俐
        </p>
<p class="releasetime">上映时间：1993-07-26</p>    </div>
"""

import re

p=re.compile('<div class="movie-item-info">.*?title="(.*?)".*?class="star">(.*?)</p>.*?class="releasetime">(.*?)</p>',re.S)
data=re.findall(p,html)
print(data)
```

# 9、xpath解析器

## from lxml import etree

## from lxml import html

### xpath解析器是在xml文档中寻找数据的一种工具

| 元字符 | 作用                   |
| ------ | ---------------------- |
| /      | 获取当前节点           |
| //     | 获取当前节点的子孙节点 |
| @      | 获取节点的属性         |
| text() | 获取节点的文本信息     |
| ../    | 获取当前节点的父节点   |

```python
from lxml import etree

html="""
<div class="movie-item-info">
        <p class="name"><a href="/films/13824" title="射雕英雄传之东成西就" data-act="boarditem-click" data-val="{movieId:13824}">射雕英雄传之东成西就</a></p>
        <p class="star">
                主演：张国荣,梁朝伟,张学友</p>
        <p class="releasetime">上映时间：1993-02-05(中国香港)</p>    
</div>
<div class="d1">
        <li id="link1">百度</li>
        <li id="link2">新浪</li>
        <li id="link3">网易</li>
        <p>hello world</p>
        <p>你好世界！</p>
</div>
"""
parse_html=etree.HTML(html) #将网页源代码转换成xpath对象
#获取class=movie-item-info的div节点下的class=name的p节点下的a节点的title属性
data=parse_html.xpath('//div[@class="movie-item-info"]/p[@class="name"]/a/@title')
# data=parse_html.xpath('//div') #获取所有的div节点
# data=parse_html.xpath('//p')
# data=parse_html.xpath('//div/p') #获取div节点下的p节点的信息
# data=parse_html.xpath('//div[@class="d1"]/p') #获取class=d1的div节点下p节点的信息
# data=parse_html.xpath('//div[@class="d1"]/p/text()') #获取class=d1的div节点下的p节点中的文本信息
# data=parse_html.xpath('//div[@class="d1"]/p[1]/text()') #获取class=d1的div节点下的第一个p节点中的文本信息
print(data)
```

# 10、学院官网

```python
import requests
from lxml import etree
from user_headers import L
import random


class Cunjin:
    def __init__(self):
        self.url="http://www.gdcjxy.com/index.html"
        self.headers={"User-Agent":random.choice(L)}

    def get_html(self,url):  #获取网页源代码并将源代码转换成xpath的函数
        res=requests.get(url,headers=self.headers)
        res.encoding="utf-8"
        html=res.text
        parse_html=etree.HTML(html) #将源代码转换为xpath对象
        return parse_html

    def get_t_link(self): #获取帖子中的站内链接的函数并拼接成完整链接
        parse_html=self.get_html(self.url) #对官网主页发起请求
        t_url=parse_html.xpath('//a[@class="p"]/@href')
        for link in t_url:
            url="http://www.gdcjxy.com"+link
            self.get_pic_url(url) #调用获取图片链接的函数


    def get_pic_url(self,url): #获取所有图片链接的函数
        parse_html=self.get_html(url)
        pic_url=parse_html.xpath('//span[@style="font-size:18px;"]/img/@src')
        for link in pic_url:
            pic_link="http://www.gdcjxy.com"+link
            print(pic_link)

    def save_pic(self): #将图片下载到本地的函数
        pass

cunjin=Cunjin()
cunjin.get_t_link()
```

