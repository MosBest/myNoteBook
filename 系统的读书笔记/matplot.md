[toc]

# matplotlib
1. import matplotlib.pyplot as plt
1. %matplotlib  inline#qt 或者不填
2. plot() 或者close()
3. 
fig,axes=plt.subplot(2,3)
axes[0,1].scatter()
axes[1,1].hist()
ax.set_xlim()
ax.set_xicks()
ax.set_ticklabels()

# pandas 的绘图方法
## 线形图
对于Series
s=Series(...)
s.plot(xticks=,xlim=,yticks=,ylim=)
![这里写图片描述](http://img.blog.csdn.net/20160816084100962)
![这里写图片描述](http://img.blog.csdn.net/20160816084201366)
对于dataframe
df.plot()#在一个subplot上面各列汇制一条线
![这里写图片描述](http://img.blog.csdn.net/20160816084243851)
## 柱状图
![这里写图片描述](http://img.blog.csdn.net/20160816084434027)
 ![这里写图片描述](http://img.blog.csdn.net/20160816084550575)
 
![这里写图片描述](http://img.blog.csdn.net/20160816084810452)
## 直方图 可以表示数据出现的频数
![这里写图片描述](http://img.blog.csdn.net/20160816085228546) 
s=Series(......)
s.hist(...)
## 密度图 通常和直方图画在一起
在plot()里加上kind='kde'
![这里写图片描述](http://img.blog.csdn.net/20160816085726729)
即形如
![这里写图片描述](http://img.blog.csdn.net/20160816085810871)
## 散点图
![这里写图片描述](http://img.blog.csdn.net/20160816090035578)
## 散点矩阵图
![这里写图片描述](http://img.blog.csdn.net/20160816090131253)
![这里写图片描述](http://img.blog.csdn.net/20160816090223581)