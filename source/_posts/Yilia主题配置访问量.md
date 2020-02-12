---
title: Yilia主题配置访问量
date: 2019-11-29 01:25:39
tags:
		- hexo
categories:
		- hexo
---

## hexo+yilia页脚添加总访问量
##### 脚本方法使用不蒜子计数
安装脚本

要使用不蒜子（官网：http://busuanzi.ibruce.info/）必须在页面中引入busuanzi.js，代码如下：
```
<script async src="//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js"></script>
            <span id="busuanzi_container_site_pv">本站总访问量<span id="busuanzi_value_site_pv"></span>次</span>

```

在themes/yilia/layout/_partial/footer中添加上述脚本

![footer_busuanzi](https://img2018.cnblogs.com/blog/1338341/201810/1338341-20181027102159206-1713161383.png)