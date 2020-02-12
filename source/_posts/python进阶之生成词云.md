---
title: python进阶之生成词云
date: 2019-12-08 10:21:34
tags:
	- python
	- 爬虫
categories:
	- python
---
# 1、词云项目

### 1、对获取的评论数据进行分词

```python
import jieba
def cut_info():
  with open("comment.txt","r",encoding="utf-8") as f:
    text=f.read()
    cut_text=" ".join(jieba.cut(text))
    with open("cut_text.txt","w",encoding="utf-8") as f:
      f.write(cut_text)
cut_info()
```
<!--more-->
### 2、绘制词云

```python
#通过wordcloud模块传入词云相对应的参数
from wordcloud import WordCloud,ImageColorGenerator,STOPWORDS
#将图片变为多维数组的模块，实现图片和文字的交互
from imageio import imread
#使用codecs打开文件，不需要考虑编码格式问题，默认都是用Unicode编码
import codecs
#绘制数学统计制图陌路爱，用它来显示和绘制词云
import matplotlib.pylab as plt
from os import path
class Darw_pic:
  def __init__(self):
    self.font_path="./font/simhei.ttf"  #设置字体路径
    self.image_path="timg.jpg" #设置图片路径
    self.cut_text="cut_text.txt" #设置文本路径
  def get_info(self):
    d=path.dirname(__file__) #获取当前文件的操作路径
    image=imread(self.image_path) #将图片处理为多维数组
    text=codecs.open(path.join(d,self.cut_text),"rb",encoding="utf-8").read() #读取文本
数据
    self.draw_wordcloud(image,text) #调用绘制词云的方法
  def draw_wordcloud(self,image,text):
    stopwords=set(STOPWORDS) #使用默认的屏蔽词
    # 字体路径 图片数组 屏蔽字 背景颜色 最大词数限制 字体最大限制 文本数据
    wordcloud=WordCloud(font_path=self.font_path,mask=image,
              stopwords=stopwords,background_color="white",
              max_words=2000,max_font_size=200).generate(text)
    image_color=ImageColorGenerator(image) #让字体颜色随着图片变色改变
    wordcloud.to_file("wordcloud.jpg") #给生成的词云命名
    plt.imshow(wordcloud.recolor(color_func=image_color)) #生成词云的颜色
    plt.axis("off") #不显示坐标轴
    plt.show() #显示词云
   
draw=Darw_pic()
draw.get_info()
```

![wordcloud](https://github.com/zxk0nly1/python/blob/master/day05/wordcloud.jpg?raw=true)
