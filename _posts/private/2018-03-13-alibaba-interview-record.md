---
layout: post
title: 记录 Alibaba 2018 春招实习面试
categories: [Private]
description: 投了「阿里巴巴」的春招实习，从一面开始打卡记录
keywords: 阿里巴巴, 2018春招实习, 打卡
tags: [记录]
excerpt: 投了「阿里巴巴」的春招实习，从一面开始打卡记录
---
## 蚂蚁金服实习面试

### 2018-3-13
今天下午两点过收到阿里巴巴面试电话，此时的我正在东莞出差，还好当时手上没有太多的活可以顺利进行面试。  
面试官很 Nice 从开始的电话面试到后面的在线笔试一共花了 3 个小时，电话面试中大概有几个问题没有回答上面，这里得好好准备下。  
问题基本都是针对项目的。
1. influxDb 内部的机制，为啥比 Mysql 效率高？
1. Mq 内部的实现原理？
1. 轻量级锁和重量级锁有什么区别？

关于在线编程题，考了一个在 0, 1 矩阵中找到所有为 1 的区域当中的封闭区域的个数。  
该题从一开始我就使用的是「广度优先」算法去解决，但是最终没有调试出来，很遗憾！  
不知道这次面试怎么样，希望还有二面的机会，即使失败了还有秋招，所以不能松懈下来！

### 2018-3-14
今天是一面后的第 1 天，没有接到二面的通知，问了下内推的师兄，显示的是「面试中」的状态，估计应该放备胎池了吧。今天将 Java 的 Collection 和 Map 相关内容进一步熟悉了下，同时也开始准备算法，今天看的是动态规划。

### 2018-3-15
今天是一面后的第 2 天，没有接到二面通知，个人中心的状态还是「面试中」应该还有机会吧我想。
 
### 2018-3-16
今天是一面后的第 3 天，千呼万唤终于等来了二面，14:26 分打来总共面了 38分38秒。  
面试的时候还是先做自我介绍，然后问了下自己印象比较深的项目经验，然后再问了一个算法题，这个算法题就是在一个只有整数的超大文件(10G以上)里面的重复次数超过 3 次的整数写入到另一个文件。  
这个问题我一开始就说用 HashMap 但是内存肯定是装不下的，然后就说先分割文件，然后再处理。
然后面试官又问怎么分割，分割的依据，我说的取模。  
最后面试官文取模出现某个文件过大怎么办，这个我没想出来。  
其实很简单再对这个文件进行取模即可。。  
在面试官的指点下一步一步接近真相了，但是还差最后一步，我有种不好的预感。。  
希望还有第三面吧。

### 2018-3-17
今天是一面后的第 4 天，今天周六肯定不会有面试电话打过来的，不过自己还是在背考点、刷算法，今天将「动态规划」的一些基本问题刷完了。 今天的阿里巴巴个人中心的状态还是「面试中」

### 2018-3-18
今天是一面后的第 5 天，周天，今天睡到了 10 点才起床，下午刷了三道简单的 LeetCode，今天状态依然是「面试中」，下周希望能有三面。

### 2018-3-19
今天是一面后的第 6 天，周一，今天接到了三面的电话，很激动，但是后果很残酷，被刷了，个人中心显示的是「已回绝」，怎么说呢，心情还是有一点小失落。  
这个面试官很奇怪，没问技术问题都是一些非技术问题，真让人摸不着头脑  
我觉得是一个问题没有处理好，个人的优点是啥，个人的局限性是啥，这两个问题我的好好思考一下。
不过 5 月 9 日还有正式的校招实习流程，这几个自己努力提升自己的技能吧。

--- 

## 钉钉实习面试
### 2018-4-10
被刷快一个月之后居然被钉钉部门给捞起来了，很奇怪。我想估计没什么希望吧，今天晚上 9 点半接到了钉钉的面试电话，很兴奋，也没有多大希望，由于太晚了约的明天下午两点的在线编程测试。

### 2018-4-11
今天面了阿里「钉钉」的在线算法编程测试，一个 N 个数组排序算法，难度比较低，刚好之前总结了排序算法，快排+合并 就搞定了这个题。希望还能有下次面试。说的是一周之内有通知。此时个人中心的状态从「简历评估」变成了「待安排面试」。

### 2018-4-12
今天是「钉钉」一面之后的第 1 天，今天状态还是「待安排面试」。

### 2018-4-13
今天是「钉钉」一面之后的第 2 天，今天状态仍然是「待安排面试」。

### 2018-4-14
今天是「钉钉」一面之后的第 3 天，今天状态终于更新成「面试中」，熟悉的字眼，熟悉的心情，这次要好好把握。

### 2018-4-15
今天是「钉钉」一面之后的第 4 天，今天周末肯定不会有面试通知，今天把之前准备的知识点内容都过一遍，加深印象。  
今天我想到了自己的优缺点的答案。

### 2018-4-16
今天是「钉钉」一面之后的第 5 天，今天周一终于迎来了二面，二面一开始就是做题居然和一面一样的排序题，这真是让我觉得有点意外
二面的过的还是蛮顺畅的，就做了个题然后问了下多线程和锁方面的问题，二面完了之后然后一面的面试官叫我继续做了个大题，明天中午
之前交给他，这时候已经是晚上 20：:30 了，题目是「用多线程处理一个超过 100G 的文本，将其反序输出」这种大文本处理的题目是阿里
最喜欢考的，之前「蚂蚁金服」三面的时候面试官也问了一个类似的问题，不过这次需要自己动手写出来，然后我花了两个小时就写出来了，只是
还有编码问题没有解决。

### 2018-4-17
今天是 「钉钉」一面之后的第 6 天，今天我将昨天安排的题目写出来交给了面试官，今天的状态还是「面试中」。

### 2018-4-18
今天是「钉钉」一面之后的第 7 天，今天头晕，但是没有接到面试通知，状态仍然还是「面试中」。

### 2018-4-19
今天是「钉钉」一面之后的第 8 天，今天晚上 22:12 接到了「钉钉」的面试电话，终于迎来了第三面还是这么晚的时候，不知道「钉钉」部门一天
加班加多久，今天主要面了下个人性格，问了你喜欢什么样的人和老师，有了上次的经验之后这次还好能够从容应对，一共面了 27分14 秒。面完之后
个人状态仍然是「面试中」，心中窃喜。

### 2018-4-20
今天是「钉钉」一面之后的第 9 天，身体不舒服，去医院输液了，熬夜过多导致身体虚弱。
> 2019-4-1：只是颈椎病的锅，现在已经好很多了

### 2018-4-21
今天是「钉钉」一面之后的第 10 天，停电加之身体不舒服，头晕，休息一天。

### 2018-4-22
今天是「钉钉」一面之后的第 11 天，周末继续休息。

### 2018-4-23
今天是「钉钉」一面之后的第 12 天，今天状态稍微恢复了点，但是还是依然没法完全集中注意力，今天晚上没有加班，今天仍然没有接到 4 面通知，状态「面试中」。

### 2018-4-24
今天是「钉钉」一面之后的第 13 天，今天没有接到「钉钉」的面试通知，倒是接到了「七牛」的面试预约，明天下午两点面试「七牛」。

### 2018-4-25
今天是「钉钉」一面之后的第 14 天，今天没有接到「钉钉」的面试，今天面试了「七牛」，感觉还行。

### 2018-4-26
今天是「钉钉」一面之后的第 15 天，今天没有接到「钉钉」的面试，今天身体状况依然糟糕。

### 2018-4-27
今天是「钉钉」一面之后的第 16 天，今天没有接到「钉钉」的面试，今天继续休息。

### 2018-4-28
今天是「钉钉」一面之后的第 17 天，今天没有接到「钉钉」的面试，今天从启东回成都了，爽。

### 2018-4-29
今天是「钉钉」一面之后的第 18 天，今天五一放假。

### 2018-4-30
今天是「钉钉」一面之后的第 19 天，今天五一放假。

### 2018-5-1
今天是「钉钉」一面之后的第 20 天，今天五一放假。

### 2018-5-2
今天是「钉钉」一面之后的第 21 天，今天没有接到「钉钉」的面试。

### 2018-5-3
今天是「钉钉」一面之后的第 22 天，今天终于迎来了「钉钉」的 HR 面试，问了几个问题。
1. 对加班怎么看待
1. 个人压力最大的时刻
1. 怎么解决团队融合问题
1. 介绍某个项目个人的职责

### 2018-5-16
1. 今天是钉钉一面之后的第 35 天，今天收到了入职体检消息，个人中心变成了「已发起 Offer 流程」

### 2018-5-25
1. 今天是钉钉一面之后的第 44 天，今天周五，下周一就要去入职了，周天的飞机。

#### 2018-8-11
1. 完成钉钉实习，主管说转正面试通过了，静等九月的结果

#### 2018-8-30
1. 钉钉刷新了状态，变成了「待更进 offer」