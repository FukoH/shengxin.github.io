---
title: '如何在Jupyter里以不同的运行模式使用Pyspark'
date: 2018-04-28
excerpt: 如题
permalink: /posts/2018/04/如何在Jupyter里以不同的运行模式使用Pyspark/
tags:
  - Data Science
  - Data Engineering
---

假设你的环境已经安装好了以下东西,如何详细的安装它们不在本文的讨论范围之内
具体的可疑参考[三分钟搞定jupyter和pyspark整合](https://blog.sicara.com/get-started-pyspark-jupyter-guide-tutorial-ae2fe84f594f)
1. anaconda2
2. findspark
3. pyspark

这里多说一句,spark1.几的版本以下的只支持python2.几的支持python2和3.具体是spark2.几,笔者没有详细调查.
## 如何以不同的模式运行pyspark
我们都知道,spark是分为local,standalone,yarn-client,yarn-cluster等运行模式的.既然想用jupyter,自然是想要交互式的,那么如何以不同的模式来交互呢?

笔者总结如下:
1. local模式

>import findspark
findspark.init()
from pyspark import SparkContext
sc = SparkContext("local", "First App")

2.standalone
需要传入地址和端口
>import findspark
findspark.init()
from pyspark import SparkContext
sc = SparkContext("spark://192.168.5.129:7077", "First App")

3.yarn-client
>import findspark
findspark.init()
from pyspark import SparkContext
sc = SparkContext("yarn-client", "First App")

3.yarn-cluster
cluster模式一般都是开发完成后,直接用来执行用的,不适用于交互模式,笔者也没有尝试过.在此就不介绍了.

## 关于SparkContext

其实SparkContext这个类,每个位置可以传的参数,是和shell命令行对应的,注意到了这一点,看看文档就知道每个参数可以接受什么样的值了.具体内容可以看spark[官方文档](http://spark.apache.org/docs/latest/submitting-applications.html).