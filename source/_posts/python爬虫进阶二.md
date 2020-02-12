---
title: python爬虫进阶二
date: 2019-12-05 23:36:22
tags:
	- python
	- 爬虫
categories:
	- python
---
# 1、python链接mysql数据库

## 1、建立链接

```python
        conn=pymysql.connect(
            host="127.0.0.1",
            port=3306,
            user="root",
            password="123456",
            database="douban"
        )

```

## 2、创建游标对象

```python
cursor=conn.cursor() #创建游标对象
```
<!--more-->
## 3、执行插入数据库操作

```python
sql_insert="""INSERT INTO movie_info(title,actors,regions,release_time,score,rank,types) VALUES (%s,%s,%s,%s,%s,%s,%s)"""
        cursor.executemany(sql_insert,t_list) #插入数据
        conn.commit() #关闭连接
```

```python
import requests
from user_headers import L
import json
import csv
import random
import pymysql

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
            # self.save_data(content) #调用保存数据的函数
            self.save_mysql(content) #调用保存数据库的函数

    def save_data(self,content):
        with open("movie.csv","a",encoding="utf-8",newline="") as f:
            writer=csv.writer(f)
            writer.writerow(content)
            print("数据存储成功！")

    def save_mysql(self,content): #将数据存储到数据库的函数
        t_content = tuple(content)
        t_list=[t_content]
        conn=pymysql.connect(
            host="127.0.0.1",
            port=3306,
            user="root",
            password="123456",
            database="douban"
        )
        cursor=conn.cursor() #创建游标对象
        sql_insert="""INSERT INTO movie_info(title,actors,regions,release_time,score,rank,types) VALUES (%s,%s,%s,%s,%s,%s,%s)"""
        cursor.executemany(sql_insert,t_list) #插入数据
        conn.commit() #关闭连接
        print("数据存储成功！")

douban=Douban()
douban.get_json_data()
```

## 2、有道翻译

```pyth
i: 橙子
from: AUTO
to: AUTO
smartresult: dict
client: fanyideskweb
salt: 15755328116991  #不同
sign: 8426ffae4746b0c256debb05c2fe6360 #不同
ts: 1575532811699 #不同
bv: 6cf12640614e68ba598ee58ceccb0605
doctype: json
version: 2.1
keyfrom: fanyi.web
action: FY_BY_CLICKBUTTION
 
i: 苹果
from: AUTO
to: AUTO
smartresult: dict
client: fanyideskweb
salt: 15755326946679
sign: b8bd75822a971700fe6d340ddff3d580
ts: 1575532694667
bv: 6cf12640614e68ba598ee58ceccb0605
doctype: json
version: 2.1
keyfrom: fanyi.web
action: FY_BY_CLICKBUTTION
```

#### r变量为获取当前时间节点的时间戳 ---> ts

#### i变量为 r+一个0~9之间的随机数 ----> salt

#### e变量为 输入需要翻译的单词

#### sign--> md5加密("fanyideskweb" +e+i+"n%A-rKaT5fb[Gy?;N5@Tj"")

```python
import requests
import json
from user_headers import L
import random
import time
from hashlib import md5
class Youdao:
  def __init__(self):
    self.url="http://fanyi.youdao.com/translate_o?smartresult=dict&smartresult=rule"
    self.headers={"User-Agent":random.choice(L),
984118829@qq.com 姓名 学号
           "Cookie":"OUTFOX_SEARCH_USER_ID=-1431696184@10.169.0.83;
OUTFOX_SEARCH_USER_ID_NCOO=1943625779.162675; JSESSIONID=aaaUBWn5SCFytfQLoev7w;
___rl__test__cookies=1575535864354",
           "Referer":"http://fanyi.youdao.com/"}
  def get_json(self):
    word=input("请输入需要翻译的单词:")
    ts =str(int(time.time() * 10000))  # 获取时间戳
    salt = ts + str(random.randint(0, 9))  # 生成0~9之间的随机整数
    data = "fanyideskweb" + word + salt + "n%A-rKaT5fb[Gy?;N5@Tj"
    s = md5()
    s.update(data.encode())
    sign = s.hexdigest()
    data={
      "i":word,
      "from":"AUTO",
      "to": "ko",
      "smartresult":"dict",
      "client":"fanyideskweb",
      "salt":salt,
      "sign":sign,
      "ts": ts,
      "bv":"6cf12640614e68ba598ee58ceccb0605",
      "doctype":"json",
      "version":"2.1",
      "keyfrom":"fanyi.web",
      "action":"FY_BY_CLICKBUTTION"
   }
    res=requests.post(self.url,headers=self.headers,data=data)
    res.encoding="utf-8"
    html=res.text
    json_data=json.loads(html)
    self.get_data(json_data)
  def get_data(self,json_data):
    data=json_data["translateResult"][0][0]["tgt"]
    print("翻译的结果为:",data)
youdao=Youdao()
youdao.get_json()
```

