---
layout:     post
title:      "ML1--Scikit-Learn简介"
subtitle:   "机器学习第一课"
date:       2020-05-10 00:10:00
author:     "yan"
header-img: "img/image_20200510001.png"
top-img: "/img/image_2020051001.png"
catalog: true
tags:
    - 机器学习
---
# 一、简介

&emsp;&emsp;对Python语言有所了解的科研人员可能都知道SciPy——一个开源的基于Python的科学计算工具包。基于SciPy，目前开发者们针对不同的应用领域已经发展出了为数众多的分支版本，它们被统一称为Scikits，即SciPy工具包的意思。而在这些分支版本中，最有名，也是专门面向机器学习的一个就是Scikit-learn。

&emsp;&emsp;Scikit-learn项目最早由数据科学家David Cournapeau 在2007 年发起，需要NumPy和SciPy等其他包的支持，是Python语言中专门针对机器学习应用而发展起来的一款开源框架。它的维护也主要依靠开源社区。

# 二、特点

&emsp;&emsp;作为专门面向机器学习的Python开源框架，Scikit-learn可以在一定范围内为开发者提供非常好的帮助。它内部实现了各种各样成熟的算法，容易安装和使用，样例丰富，而且教程和文档也非常详细。

&emsp;&emsp;另一方面，Scikit-learn也有缺点。例如它不支持深度学习和强化学习，这在今天已经是应用非常广泛的技术。此外，它也不支持图模型和序列预测，不支持Python之外的语言，不支持PyPy，也不支持GPU加速。

&emsp;&emsp;看到这里可能会有人担心Scikit-learn的性能表现，这里需要指出的是：如果不考虑多层神经网络的相关应用，Scikit-learn的性能表现是非常不错的。究其原因，一方面是因为其内部算法的实现十分高效，另一方面或许可以归功于Cython编译器；通过Cython在Scikit-learn框架内部生成C语言代码的运行方式，Scikit-learn消除了大部分的性能瓶颈。

# 三、主要类或用过的类

&emsp;&emsp;Scikit-learn的基本功能主要被分为六大部分：分类，回归，聚类，数据降维，模型选择和数据预处理。

## （1）Preprocessing 预处理

· 应用：转换输入数据，规范化、编码化

· 模块：preprocessing，feature_extraction，transformer（转换器）

## （2）Dimensionality reduction 降维

· 应用：Visualization（可视化），Increased efficiency（提高效率）

· 算法：主成分分析(PCA)、非负矩阵分解（NMF），feature_selection(特征选择)等

## （3）Classification 分类

· 应用：二元分类问题、多分类问题、Image recognition 图像识别等

· 算法：逻辑回归、SVM，最近邻，随机森林，Naïve Bayes，神经网络等

## （4）Regression 回归

· 应用：Drug response 药物反应，Stock prices 股票价格

· 算法：线性回归、SVR，ridge regression，Lasso，最小角回归（LARS）等

## （5）Clustering 聚类

· 应用：客户细分，分组实验结果

· 算法：k-Means，spectral clustering(谱聚类)，mean-shift（均值漂移）

## （6）Model selection 模型选择

· 目标：通过参数调整提高精度

· 模块：pipeline(流水线)，grid_search（网格搜索），cross_validation( 交叉验证)，metrics（度量），learning_curve（学习曲线）

## （7）模型融合

· 模块：ensemble(集成学习)、

## （8）辅助工具

· 模块：exceptions(异常和警告)、dataset（自带数据集）、utils、sklearn.base

# 四、选择模型流程
&emsp;&emsp;学习 Sklearn 时，不要直接去用，先了解一下都有什么模型方法，然后选择适当的方法，来达到你的目标。

&emsp;&emsp;Sklearn 官网提供了一个流程图，蓝色圆圈内是判断条件，绿色方框内是可以选择的算法：
<div align="center"> <img src="/img/image_2020051001.png"/> </div><br>
&emsp;&emsp;从 START 开始，首先看数据的样本是否 >50，小于则需要收集更多的数据。

&emsp;&emsp;由图中，可以看到算法有四类，**分类，回归，聚类，降维**。

&emsp;&emsp;其中分类和回归是监督式学习，即每个数据对应一个label。
聚类是非监督式学习，即没有label。
&emsp;&emsp;另外一类是降维，当数据集有很多很多属性的时候，可以通过降维 算法把属性归纳起来。例如 20 个属性只变成 2 个，注意，这不是挑出 2 个，而是压缩成为 2 个，它们集合了 20 个属性的所有特征，相当于把重要的信息提取的更好，不重要的信息就不要了。

&emsp;&emsp;然后看问题属于哪一类问题，是分类还是回归，还是聚类，就选择相应的算法。当然还要考虑数据的大小，例如 100K 是一个阈值。

&emsp;&emsp;可以发现有些方法是既可以作为分类，也可以作为回归，例如 SGD。

# 五、应用模型
&emsp;&emsp;Sklearn 把所有机器学习的模式整合统一起来了，学会了一个模式就可以通吃其他不同类型的学习模式。
&emsp;&emsp;例如，分类器，
&emsp;&emsp;Sklearn 本身就有很多数据库，可以用来练习。我们用其中 Iris 的数据为例，这种花有四个属性，花瓣的长宽，茎的长宽，根据这些属性把花分为三类。
&emsp;&emsp;我们要用分类器 去把四种类型的花分开。
<div align="center"> <img src="/img/image_20200510002.png"/> </div><br>
&emsp;&emsp;今天用 KNN classifier，就是选择几个临近点，综合它们做个平均来作为预测值。

使用模型的步骤：
1. 导入模块
2. 创建数据
3. 建立模型－训练－预测
## 1. 导入模块
```
from __future__ import print_function
from sklearn import datasets   
from sklearn.cross_validation import train_test_split   
from sklearn.neighbors import KNeighborsClassifier
```
## 2. 创建数据
&emsp;&emsp;加载 iris 的数据，把属性存在 X，类别标签存在 y：
```
iris = datasets.load_iris()
iris_X = iris.data
iris_y = iris.target
```
&emsp;&emsp;观察一下数据集，X 有四个属性，y 有 0，1，2 三类：
```
print(iris_X[:2, :])
print(iris_y)
```
```
"""
[[ 5.1  3.5  1.4  0.2]
 [ 4.9  3.   1.4  0.2]]
[0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
 0 0 0 0 0 0 0 0 0 0 0 0 0 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1
 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2 2 2 2
 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2
 2 2]
 """
```
&emsp;&emsp;把数据集分为训练集和测试集，其中 test_size=0.3，即测试集占总数据的 30%：
```
X_train, X_test, y_train, y_test = train_test_split(
    iris_X, iris_y, test_size=0.3)
```
&emsp;&emsp;可以看到分开后的数据集，顺序也被打乱，这样更有利于学习模型：
```
print(y_train)
```
```
"""
[2 1 0 1 0 0 1 1 1 1 0 0 1 2 1 1 1 0 2 2 1 1 1 1 0 2 2 0 2 2 2 2 2 0 1 2 2
 2 2 2 2 0 1 2 2 1 1 1 0 0 1 2 0 1 0 1 0 1 2 2 0 1 2 2 2 1 1 1 1 2 2 2 1 0
 1 1 0 0 0 2 0 1 0 0 1 2 0 2 2 0 0 2 2 2 1 2 0 0 2 1 2 0 0 1 2]
 """
```
## 3. 定义模型－训练模型－预测

&emsp;&emsp;定义模块方式 KNeighborsClassifier()，用fit 来训练 training data，这一步就完成了训练的所有步骤，后面的 knn 就已经是训练好的模型，可以直接用来 predict 测试集的数据，对比用模型预测的值与真实的值，可以看到大概模拟出了数据，但是有误差，是不会完完全全预测正确的。
```
knn = KNeighborsClassifier()
knn.fit(X_train, y_train)
print(knn.predict(X_test))
print(y_test)
```
```
"""
[2 0 0 1 2 2 0 0 0 1 2 2 1 1 2 1 2 1 0 0 0 2 1 2 0 0 0 0 1 0 2 0 0 2 1 0 1
 0 0 1 0 1 2 0 1]
[2 0 0 1 2 1 0 0 0 1 2 2 1 1 2 1 2 1 0 0 0 2 1 2 0 0 0 0 1 0 2 0 0 2 1 0 1
 0 0 1 0 1 2 0 1]
 """
```
