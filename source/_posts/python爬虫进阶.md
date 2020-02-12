---
title: python爬虫进阶
date: 2019-12-04 20:44:25
tags:
	- python
	- 爬虫
categories:
	- python
---
# 1、非结构化数据的下载

```python
import requests


url="图片链接.jpg"
res=requests.get(url,headers)
res.enconding="utf-8"
html=res.content  #将图片转换为二进制字节流
with open("data.jpg","wb") as f:
    f.write(html)
```

```python
import requests
from lxml import etree
from user_headers import L
import random
import os


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
        self.files="./寸金学院"
        if not os.path.exists(self.files): #检测当前路径是否存在同名文件夹
            os.mkdir(self.files)
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
            filename=self.files+"//"+pic_link[-15:] #以图片链接的后15位作为图片的名称
            self.save_pic(pic_link,filename) #调用保存图片的函数

    def save_pic(self,pic_link,filename): #将图片下载到本地的函数
        res=requests.get(pic_link,headers=self.headers)
        res.encoding="utf-8"
        html=res.content
        with open(filename,"wb") as f:
            f.write(html)
            print(filename,"下载成功！")


cunjin=Cunjin()
cunjin.get_t_link()
```
<!--more -->

# 2、bs4选择器

## python -m pip install bs4

### from bs4 import BeautifulSoup

```python
from bs4 import BeautifulSoup

html=""""""
soup=BeautifulSoup(html,"lxml") #将源代码转换为soup对象

```

## 1、节点选择器

```python
soup=BeautifulSoup(html,"lxml") #将源代码转换为soup对象
# data=soup.div
data=soup.a
print(data)
```

## 2、获取节点属性

```python
# data=soup.a.attrs["class"]
data=soup.a["class"]
print(data)
data=soup.div.a["class"] #嵌套选择
print(data)
```

## 3、方法选择器

### 查询所有符合条件的元素，给他传入一些属性或文本，就可以得到所有符合条件的元素

```python
# data=soup.find_all(name="div")  #查找所有节点名称为div的节点信息
# data=soup.find_all(attrs={"id":"link"})
data=soup.find_all(id="link")
print(data)
# data=soup.find_all(class_="d1")
data=soup.find_all("div",class_="d1") # 查找class=d1的div节点信息
print(data)
```

## 4、css选择器

### 使用css选择器，调用select方法，可以查找定位符合条件的元素

```python
#thread_list > li:nth-child(9) > div > div.col2_right.j_threadlist_li_right > div.threadlist_lz.clearfix > div.threadlist_title.pull_left.j_th_tit
```

```python
soup=BeautifulSoup(html,"lxml") #将源代码转换为soup对象
# data=soup.select('div > ul > li') #层级选择
data=soup.select("div.threadlist_title") #通过选择器属性定位节点信息
print(data)
data=soup.select('div > ul > li') #层级选择
print(data)
for i in data:
    print(i.text) #获取节点中的文本信息
    print(i.string)
```

# 3、古诗词项目

## www.gushiwen.org

## 1、获取所有页面的古诗的标题与内容

## 2、存储格式如下：

### 每首古诗单独为一个文件，所有古诗存放在一个文件夹内

### 每首古诗文件内的古诗为，标题独自占一行，内容每遇到句号换行一次

### 如果古诗标题内存在/，需要去除这个/

```python
import requests
from bs4 import BeautifulSoup
import os
from user_headers import L
import random

class Gushi:
    def __init__(self):
        self.url="https://www.gushiwen.org/default_4.aspx"
        self.headers={"User-Agent":random.choice(L)}


    def get_soup(self):
        self.files="./古诗词"
        if not os.path.exists(self.files):
            os.mkdir(self.files)
        res=requests.get(self.url,headers=self.headers)
        res.encoding="utf-8"
        html=res.text
        soup=BeautifulSoup(html,"lxml")
        self.get_data(soup)

    def get_data(self,soup):
        title=soup.select('div > p > a > b') #通过css选择器查找标题内容
        comment=soup.find_all("div",class_="contson") #通过方法选择器查找内容信息
        self.save_data(title,comment) #调用保存信息的函数

    def save_data(self,title,comment):
        for i in range(len(title)): #获取标题和内容列表的索引
            name=title[i].text
            for j in name:
                if j=="/":
                    name=name.replace(j,"")
            filename=self.files+"//"+name
            data=comment[i].text
            with open(filename,"w",encoding="utf-8") as f:
                f.write(name)
                for i in data:
                    f.write(i)
                    if i =="。": #如果写入的字符为。,则添加一个换行符进去，进行换行的操作
                        f.write("\n")
                print("数据存储成功！")



gushi=Gushi()
gushi.get_soup()
```

# 4、json模块

## 用于python数据类型和json数据类型之间的相互转换

## json                                python

### 对象                                       字典

### 数组                                       列表

## 1、json.loads()

#### 用于将json--->python数据类型

```python
import json

json_data="""[{"name":"小明"},{"age":"20"},{"sex":"男"}]"""
print(json_data)
print(type(json_data))
# for i in json_data:
#     print(i)

data=json.loads(json_data) #将json-->python
print(data)
print(type(data))
for i in data:
    print(i)
```

## 2、json.dumps()

#### 用于将python--->json数据类型

```python
#json.dumps使用的默认编码是ASCII编码，ensure_ascii=False参数的作用就是不适用和这个编码格式
json_text=json.dumps(data,indent=2,ensure_ascii=False)
with open("data.json","w",encoding="utf-8") as f:
    f.write(json_text)
```

# 5、bilibili小视频

## 1、抓包 找到存放视频信息的真实请求

## 2、分析请求参数，找到可变的参数信息

## 3、构造参数字典，然后对url发起请求

## 4、发起请求后得到json数据，然后将json数据转换为python数据

## 5、解析数据，获取视频的下载地址

## 6、将视频下载到本地文件夹

```python
import requests
import json
import os
from user_headers import L
import random
import string

class Bilibili:
    def __init__(self):
        self.url="https://api.vc.bilibili.com/board/v1/ranking/top?"
        self.headers={"User-Agent":random.choice(L)}
        self.all_chars=string.whitespace+string.punctuation #设置一个变量绑定所有的空白字符以及特殊字符
        self.files="./B站视频"

    def get_json(self):  # 对网页发起请求并获取json信息的函数
        if not os.path.exists(self.files):
            os.mkdir(self.files)
        for i in range(1,82,10):
            params={
                "page_size":"10",
                "next_offset": str(i),
                "tag": "小视频",
                "type":"tag_general_week",
                "platform":"pc"
            }
            res=requests.get(self.url,headers=self.headers,params=params)
            res.encoding="utf-8"
            html=res.text
            json_data=json.loads(html)# 将获取的json数据转换为python数据类型
            self.get_video_url(json_data) #调用获取视频链接的函数

    def get_video_url(self,json_data): # 解析json数据获取视频下载链接的函数
        for i in json_data["data"]["items"]:
            video_url=i["item"]["video_playurl"] #获取视频的地址
            name=i["item"]["description"] #获取视频的名称
            if len(name) > 15:
                name=name[-15:]
            for j in name:
                if j in self.all_chars: #如果标题中存在特殊字符，就替换为空字符
                    name=name.replace(j,"")
            filename=self.files+"//"+name+".mp4"
            self.save_video(video_url,filename) #调用保存视频的函数


    def save_video(self,video_url,filename): # 保存视频到本地的函数
        res=requests.get(video_url,headers=self.headers)
        res.encoding="utf-8"
        html=res.content
        with open(filename,"wb") as f:
            f.write(html)
            print(filename,"下载成功！")


bili=Bilibili()
bili.get_json()
```

# 6、豆瓣电影排行

## 1、通过分析查找任意一个类型的电影榜单

## 2、找到存放电影信息的请求

## 3、获取所有的电影数据

#### 电影名称  演员信息 国家 上映时间 评分 排名 电影类型

## 4、将所有的数据存储到excel表格或者数据库

```python
import requests
from user_headers import L
import json
import csv
import random

class Douban:
    def __init__(self):
        self.url="https://movie.douban.com/j/chart/top_list?"
        self.headers={"User-Agent":random.choice(L)}

    def get_json_data(self):
        with open("movie.csv","w",encoding="utf-8",newline="") as f:
            writer=csv.writer(f)
            writer.writerow(["电影名称","演员信息","国家","上映时间","评分","排名","电影类型"])
        for i in range(0,81,20):
            params={
                "type":"13",
                "interval_id":"100:90",
                "action":"",
                "start":str(i),
                "limit":"20"
            }
            res=requests.get(self.url,headers=self.headers,params=params)
            res.encoding="utf-8"
            html=res.text
            json_data=json.loads(html) #将源代码转换为json数据
            self.get_data(json_data) #调用获取信息的函数


    def get_data(self,json_data):
        for i in json_data:
            title=i["title"]  #获取电影名称
            actors=i["actors"] #获取演员信息   list
            actors=",".join(actors)
            regions=i["regions"] #获取国家信息  list
            regions=",".join(regions)
            release_date=i["release_date"] #获取上映时间
            score=i["score"] #获取评分信息
            rank=i["rank"] #获取排名信息
            types=i["types"] #获取类型信息   list
            types=",".join(types)
            content=[title,actors,regions,release_date,score,rank,types]
            self.save_data(content) #调用保存数据的函数

    def save_data(self,content):
        with open("movie.csv","a",encoding="utf-8",newline="") as f:
            writer=csv.writer(f)
            writer.writerow(content)
            print("数据存储成功！")

douban=Douban()
douban.get_json_data()
```


