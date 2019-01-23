---
image:
  teaser: fig_RF_1.jpg

layout: article
title: Gini Impurity
date: 2019-01-20
categories: notes
author: chunyi_hsiao
tags: [Decision Tree, Gini Impurity Index]
share: true
---

Directly get into the topic, about the *Gini Impurity Index (Gini)*.

![Diagram](/../images/fig_RF_1.jpg){:width="480"}  
*The illustration of Random Forest*

There is a really good introduction (for me) of *Gini* from a blog from [Zhihu](https://zhuanlan.zhihu.com/p/36795866):

(|我们需要一个能定量评估分类效果的函数，通常把它叫做不纯度函数(Impurity Function)。可以想象一个节点中样本类型越多、分布越均匀不纯度越高，举个例子，[+++-—] 要比 [+++++-] 的不纯度高，因为分布均匀，前者传递的信息是模糊的，后者则能相对明确地代表 “+” 这个状态。我们的目的是要在子節点中获得尽可能小的不纯度，即每一次切分都让不纯度降低。假设数据总共有K个类型，对于当前节点t，类型为k的数据所占...|)

To translate that quote in English, he declared some important points: 
- Impurity Function (A function for evaluating the performance of classification)
- The more classes in one node to be classified, the higher impurity, and vice versa.
- Purpose is to obtain the impurity as small as possible covered all nodes.

### *TODO*
- Write in detail.
