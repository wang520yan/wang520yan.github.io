---
layout:     post
title:      "ML4--matplotlib绘图学习1"
subtitle:   "机器学习第四课"
date:       2020-05-13 00:10:00
author:     "yan"
header-img: "img/image_back_03.jpg"
top-img: "/img/202005/0513001.png"
catalog: true
tags:
    - 机器学习
---
# 介绍
&emsp;&emsp;matplotlib是受MATLAB的启发构建的。MATLAB是数据绘图领域广泛使用的语言和工具。MATLAB语言是面向过程的。利用函数的调用，MATLAB中可以轻松的利用一行命令来绘制直线，然后再用一系列的函数调整结果。

&emsp;&emsp;matplotlib有一套完全仿照MATLAB的函数形式的绘图接口，在matplotlib.pyplot模块中。这套函数接口方便MATLAB用户过度到matplotlib包

官网：http://matplotlib.org/

学习方式：从官网examples入门学习

http://matplotlib.org/examples/index.html
http://matplotlib.org/gallery.html

# 原理
&emsp;&emsp;使用matplotlib绘图的原理，主要就是理解figure(画布)、axes(坐标系)、axis(坐标轴)三者之间的关系。
<div align="center"> <img src="/img/202005/0513002.png"/> </div>

&emsp;&emsp;一个figure(画布)上，可以有多个区域axes(坐标系)，我们在每个坐标系上绘图，也就是说每个axes(坐标系)中，都有一个axis(坐标轴)。

<div align="center"> <img src="/img/202005/0513003.png"/> </div>

&emsp;&emsp;在matplotlib中，figure画布和axes坐标轴并不能显示的看见，我们能够看到的就是一个axis坐标轴的各种图形。

&emsp;&emsp;在使用matplotlib画图时需要设置的参数。
<div align="center"> <img src="/img/202005/0513004.png"/> </div>
# 绘制
&emsp;&emsp;在绘图结构中，figure创建窗口，subplot创建子图。所有的绘画只能在子图上进行。plt表示当前子图，若没有就创建一个子图。所有你会看到一些教程中使用plt进行设置，一些教程使用子图属性进行设置。他们往往存在对应功能函数。

&emsp;&emsp;Figure：面板(图)，matplotlib中的所有图像都是位于figure对象中，一个图像只能有一个figure对象。

&emsp;&emsp;Subplot：子图，figure对象下创建一个或多个subplot对象(即axes)用于绘制图像。
<div align="center"> <img src="/img/202005/0513005.png"/> </div>

`
import matplotlib.pyplot as plt
`

plt.figure() 画布
<div align="center"> <img src="/img/202005/0513006.png"/> </div>

plt.subplot() 划分子图
<div align="center"> <img src="/img/202005/0513007.png"/> </div>
```
plt.plot()
plt.rcdefaults()
plt.rcParams["font.sans-serif"] = "KaiTi"
```
<div align="center"> <img src="/img/202005/0513008.png"/> </div>
plt.title() 子图标题
<div align="center"> <img src="/img/202005/0513009.png"/> </div>
plt.suptitle() 总标题
<div align="center"> <img src="/img/202005/0513010.png"/> </div>
```
plt.tight_layout() 自动调整、填充、消除子图之间的重叠
plt.show()
plt.scatter() 有label图例文字参数，通过plt.legend()指定图例位置等
```
<div align="center"> <img src="/img/202005/0513011.png"/> </div>
<div align="center"> <img src="/img/202005/0513012.png"/> </div>
<div align="center"> <img src="/img/202005/0513013.png"/> </div>
```
plt.text() 设置图内文本
plt.xlabel() 设置坐标轴标签
plt.ylabel()
plt.xlim() 设置坐标取值范围
plt.ylim()
plt.imshow()
plt.axis("off")
```
<div align="center"> <img src="/img/202005/0513014.png"/> </div>
折线图和柱形图 plt.plot(), plt.bar()
<div align="center"> <img src="/img/202005/0513015.png"/> </div>
```
图像处理
from PIL import Image
import matplotlib.pyplot as plt
f = Image.open()
f.format, f.size, f.mode
f.convert()
```
<div align="center"> <img src="/img/202005/0513016.png"/> </div>
```
f.split() 颜色通道分离
Image.merge() 合并
f.resize([720,1280])
f.thumbnail([720,1280]) 直接对原图相进行缩放
f.transpose(Image.FLIP_TOP_BOTTOM)
f.crop([0,0,360,640]) 裁剪
```