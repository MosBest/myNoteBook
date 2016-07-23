# 2016-7-18
天啊！记得笔记没保存，竟没了

## 小记 
1. 如何用cmd打开ipynb文件
    * 在cmd里，敲 ipython notebook 文件路径 即可
## 当天总结
上午：看完了第2节的课程
2：00--3:00：补看第一节的课程
3：00--8：40：晚上：完成第二节的任务，这个浪费了一些时间，因为读题就读了好半天。
8：40--9：30：这一段时间有些迷茫，浮躁。看了一些大公司的面试题，什么什么的，看了一下又看不下去了。这个坏习惯要改啊。
9：30--之后：看了一些其他的例子文章[名校和非名校最重要差距，悄悄影响着我们的一生](http://mp.weixin.qq.com/s?__biz=MzA5NzIyNjgwMA==&mid=2654418131&idx=1&sn=2b6c27c8682573beea405a7904c9b92e&scene=23&srcid=0716WL8oP0qSCLpSiqwsAh45#rd),有些启发，弄了半天转载，都没有成功，最后把时间用于写今天的总结。

回顾了一下，今天把coursera中华盛顿大学的机器学习系列课程第一课看了两节吧！然后完成了他的作业。 
### 今天的效果不是很好 ###
，因为想和课程一起敲代码的，由于是倒着看的，所以不知道他的数据集和标准库在哪！等找到这些资源后，特别是第一次用这个东西，有些生手，所以耽误了一段时间。

### 知识点回顾
主要就是 getting start Sframe-checkpoint 和 predicting house price 。
1. graphlab包是要收费的，但是通过coursera可以申请免费的非商用版本。
2. 如何用cmd打开ipynb文件
    * 在cmd里，敲 ipython notebook 文件路径 即可
3. graphlab.SFrame（A），A可以是字典，SFrame其实是一种数据结构，可以将字典转化成SFrame这种结构。SFrame处理数据非常方便，开源，同时，得出的表格可视化很好，有点像pandas库，都是比起pandas库，SFrame库可以处理更大量的数据，就好像pandas是将数据加载到内存中运行的，而SFrame可以在硬盘中运行（我猜的）。
   #### 他的表格可视化确实不错
4. 他的具体函数就不具体讲了。不会的可以看ipynb里的具体使用情况。下面仅仅讲一些重要的。
```
     import graphlab
     sf =graphlab.SFrame("asdas.csv")    # 读取数据，并转化为SFrame形式
     sf.show()                           #对每一个特征（列）进行简单的统计
     graphlab.canvas.set_target('ipynb') #让图形输出在ipynb页面上，而不是浏览器或其他程序上面
     sf['age'].show(view='Categorical')  #也是对数据进行统计,以表格的形式呈现,可在halp()上查看其他参数
     sf['full name']=sf['First Name']+' '+sf['Last Name']
                                         #增加特征（列），就是这么简单
     sf['Country']=sf['Country'].apply(transform_contury)
                                         #apply函数的应用，transform_cotury为某一函数，数据集是sf['Cou#ntry']
     
     
     sales.show(view='Scatter Plot',x='sqft_living',y='price') 
                                         #发现好像很区分大小写，比如 'scatter plot','Scatter #plot','scatter' 是完全不同的结果
     train_data,test_data=sales.random_split(0.8,seed=2015)
                                         # seed是种子
     sqft_model=graphlab.linear_regression.create(train_data,target='price',features=['sqft_living'])
                                         # 创建线性模型
     sqft_model.evaluate(test_data)      # 用test——datda数据对模型进行评估。
                                         # 输出结果是一个字典,包含最大误差max error,和rmse,
                                         # rss=sqrt(rmse/N)
     
     import matplotlib.pyplot as plt
     %matplotlib inline                  # 让图输出在ipynb

    plt.plot(test_data['sqft_living'],test_data['price'],'.',
             test_data['sqft_living'],sqft_model.predict(test_data),'-')
    
    sqft_model.get('coefficients')       # coefficients是系数的意思
    print my_model.predict(house1)       # 预测
    filter_sales=sales[(sales['sqft_living']>=2000 ) & (sales['sqft_living']<=4000 )]
                                         # 逻辑过滤一些数据
    filter_sales.num_rows()
        

```


# 2016-7-19 
## 小记
1. 简单的线性分类器（就是所说的打分系统）
    以一个餐厅推荐系统为例。
    写了一大串，后移到自己的csdn上面了。[点击这](http://blog.csdn.net/mosbest/article/details/51953523)
2. 混淆矩阵也可以发展到多维的情况
 ![enter description here][1]

[1]: ./images/%E6%97%A0%E6%A0%87%E9%A2%98.png "无标题.png"
3. 一般情况下，数据量越大，误差就会越小，但是即使数据量趋于无穷大，误差也不会为0，因为偏差一定存在。同时，特征越多，模型越复杂，所需要的数据量也就越多。
明天继续

## 总结
今天无话可说。为什么？我天，coursera真是卡啊！！！无话可说，弄了一天都没弄好。在加上wifi总是突然的连不上，必须重新开机才行。看来是要用ubuntu了，
同时发现，登陆coursera的官网（www.coursera.org）比登陆他的子网慢的多，只要www.coursera.org好了，其他的一般就好了。所以以后尽可能跳过这个步骤。
经过陈政的提醒，以后上coursera时把vpn关了。以后可以通过mooc学院登陆coursera [机器学习基础：案例研究](http://mooc.guokr.com/course/6199/Machine-Learning-Foundations--A-Case-Study-Approach/)
[机器学习基础：案例研究](https://www.coursera.org/learn/ml-foundations/home/welcome)
[机器学习：分类](http://mooc.guokr.com/course/6206/Machine-Learning--Classification/)
千万不要直接登陆coursera的官网
千万不要直接登陆coursera的官网
千万不要直接登陆coursera的官网
我天，现在还没有加载完。
 
 今天算是废了！！！
 
 --------------------------------------------- 
# 2016-7-20
## 小记
今天就一直在折腾ubuntu了，还没有折腾完。现在晚上11：30，前几天熬夜，今天想要早点睡，就记下还没看完的文档
[apt官方文档](http://www.debian.org/doc/manuals/apt-howto/index.zh-cn.html#contents)
[实验楼讲得简单方法](https://www.shiyanlou.com/courses/running)
[ubuntu官网资料](http://wiki.ubuntu.org.cn/%E6%96%B0%E6%89%8B%E5%85%A5%E9%97%A8%E6%8C%87%E5%BC%95)
[buntu桌面入门指南 官网](http://wiki.ubuntu.org.cn/Ubuntu%E6%A1%8C%E9%9D%A2%E5%85%A5%E9%97%A8%E6%8C%87%E5%8D%97)
[ubuntu详细的安装与配置](http://wenku.it168.com/d_000030466.shtml)
[菜鸟也能玩转Ubuntu：Ubuntu入门到精通](http://wenku.it168.com/wenji/693)(资料超全)


### 感觉学一个东西，最关键的是你能不能找到好的文档。以后会留下这方面的积累。


----------------------------------
# 2016-7-21 星期四
## 小记
简单的总结一下，今天一天到底都干了什么。
今天一天（其实应该加上昨天一天），弄明白了ubuntu下载软件的原理和方法（是不是很好笑，就干了这）。具体的内容写在了博客里了。
[ubuntu学习 之 如何安装软件](http://blog.csdn.net/mosbest/article/details/51985065)
[装完ubuntu以后的基本配置](http://blog.csdn.net/mosbest/article/details/51983574)(还没写完，明天还要继续，脱了两天了，明天是第三天了)

### 发现两点：
 1. 保存在D:,C: 上的东西，在ubuntu系统下打开，可以打开，但是当你编辑的时候，一定要注意了，小书匠会自动的更改文件的名字，然后你做的修改，都保存到了这个文件里面了，对D:,C:,上的内容并没有什么改变。解决方法是，如果你发现 小书匠  自动的更改文件名的话，那么一定要把文件名改回来。包括后缀名也要加上，这就默认为修改原文件了。
 2. 突然发现，xx-net虽然可以翻墙，但是在  “下载东西”  这方面，明显比不上 搜狐浏览器。但是xx-net可以看视频（明明下载东西时，只有20kb,却可以看ubuntu,真是好奇。）这是在windows下测的，不知道ubuntu是不是这样的。
 3. 突然想到，在mooc学院可以看coursera,在 学堂在线 可以看 dex,那是不是可以不用翻墙啊！！明天试试。

----------------------------------------
# 2016-7-22 星期五
今天上午就把昨天未弄完的东西弄完，把博客的内容补全。
下午准备安装一下kazam录屏软件，但是总是报错，弄了一下午，了解的其他的东西到是挺多的，但是还是没弄好，后来基本确定是 软件源的问题。我用netselect-apt更改源时，直接覆盖了原来的sources.list的内容，也就是原来的软件源被我删除了。
晚上，就是看寒小阳关于深度学习的公开课。然后继续查资料，还是没弄明白。

# 2016-7-23 星期六
今天上午，解决了昨天的问题。网上热心肠的人好多啊！！！弄明白UEFI是啥东西。
下午，开始学习机器学习，主要就是把大作业做完。（在csdn上写了篇关于他的博客，笔记也在这上面）程序同该笔记会一同提交到github上面的。
晚上，没有斗志了，准备做中兴人脸识别的比赛，看完之后，自信心完全没了，还是决定提交一些东西，结果就不管了。

发现：在ubuntu用小书匠运行windows10上面的.md文件时，.md文件必须是绝对路径，及时你cd 到该.md文件的路径下，.md也必须要是绝对路径。

# (从今以后，增加明天的任务，要不然总是没有动力，对最终目标没有安排)

## 明天要做的事
1. 上午：coursera 机器学习：案例研究，
	对每一节课程，每一个知识点，都在当天笔记“小节”部分写下来，以供当天晚上写总结
2. 下午：林轩田老师 《机器学习技法》  ，
	对每一节课程，每一个知识点，都在当天笔记“小节”部分写下来，以供当天晚上写总结
3. 晚上：学习C++
  对每一节课程，每一个知识点，都在当天笔记“小节”部分写下来，以供当天晚上写总结
4. 10:00到宿舍，其他学习的东西就不要看了，写好今天的总结，才是最重要的。第二天早起便是。
5. 填写好明天要完成的表格

--------------------
# 2016-7-24  星期天
## 小节
### 上午

### 下午

### 晚上

## 当天总结


## 明天要做的事
1. 上午：
	对每一节课程，每一个知识点，都在当天笔记“小节”部分写下来，以供当天晚上写总结
2. 下午：
	对每一节课程，每一个知识点，都在当天笔记“小节”部分写下来，以供当天晚上写总结
3. 晚上：
  对每一节课程，每一个知识点，都在当天笔记“小节”部分写下来，以供当天晚上写总结
4. 10:00到宿舍，其他学习的东西就不要看了，写好今天的总结，才是最重要的。第二天早起便是。
5. 填写好明天要完成的表格
