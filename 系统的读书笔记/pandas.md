
[TOC]

# 常用
倒序　range(8,1,-1)


# pandas的数据结构简介
```python
from pandas import Series,DataFrame
import pandas as pd
```
## Series
### 简介
1. Series是一个对象，类似于一维数组，但他任为 对象。他两部分组成。一组数据（各种numpy数据类型）以及一组与数据一一对应的标签（即索引）组成。
索引在左，数据在右，且索引默认为0-n——1，可以认为改变，有点像字典。
2. Series最重要的一个功能是：它在算数运算中自动对齐不同的索引的数据。比如 a+b,如果某一个键在a中存在，在b中不存在，那么a+b的结果的那个键的值为NaN
2. a.values用于得到a的数据 ，a.index用于得到a的索引标签。
3. Series的索引可以通过赋值的方式就地修改 ，直接  a.index=['bob','steve']就修改了
4. Series其实是索引值到数据值的一个映射
```python
n [20]: obj
Out[20]: 
a    1
b    5
c    4
d    3
e    2
dtype: int64

In [21]: 'b' in obj
Out[21]: True
In [23]: 'f' in obj
Out[23]: False

```
### 创建Series
1. 传入数据列表
```python
from pandas import Series,DataFrame
import pandas as pd
obj=Series([1,2,3,7,6])#自动添加默认索引
obj=Series([1,5,4,3,7],index=['a','h','c','f','e'])#认为添加索引
```
2. 传入python字典,这样字典的建keys就是Series的索引
3. 
### 2. Series 常见方法
#### a.values和a.index
 a.values用于得到a的数据 ，a.index用于得到a的索引标签。
### isnull() ,notnull()
可以用pd.isnull(obj)  或者  pd.notnull(obj)
或者obj.isnull() 或者 ogj.notnull()
看对应键是否含有缺失数据
### 切片，访问数据
有点像字典
```python
obj['a']
obg[['a','c','e']]#访问多个
错误 obg[['a','h'],]
```

## DataFrame
其是一个由表格型的数据结构
### 创建DataFrame
1. 直接传入 等长列表 或者numpy数组组成的字典
```python
data={'state':['obo','asd']
	'year':[2000,1000]
	'pop':[1.5,1.9]}

frame=DaaFrame(data)

```
2. 结果DataFrame会自动加上索引.注：索引指的是行名。DataFrame默认给行名加为0——(n-1),当然我们也可以改变行名（索引）
3. 默认情况下，全部列会被有序排列。（即，上面的代码输出时，列的顺序为'pop','state','year'）
```python
#创建DataFrame，且同时改变行名和列名
frame2=DataFrame（data，columns=['year','state','pop','debt']
			index=['one','two','three','four','five']）# columns=用于改变列名,index=用于改变索引（行名）
```
4. 但是如果指定了列序列，则DataFrame的列就会按照指定顺序进行排列
5. 跟Series一样，如果传入的列再数据中找不到，就会产生NA值
6. 一种常见的数据形式是 ==嵌套字典== (也就是字典的字典)，如果将这样的数据传入DataFrame，他就会被解释为：外层字典的键作为列，内层键作为行索引。当然如果想换一下的话，可以转置x.T。
内层字典的键会被合并、排序形成最终的索引。入股显示指定索引，就不会有这种问题。

### DataFrame行，列元素操作

#### 获得DataFrame的行（索引）
方法一：通过名称的方式获取，用索引字段ix
```python
# 以上面frame2的数据为例
#得到行名为‘three’的数据
a=frames.ix['three']#好像得到一个Serices
```

#### 获取DataFrame的列
注意：获取得到的是一个Series
注意：通过索引返回的列只是相应数据的视图而已，并不是副本。通过Series的copy 方法即可显示地复制列。
方法一：data['state']
方法二：data.state
#### DataFrame ==列的== 其他操作
##### 给列元素赋值
	1. 如果是赋上一个标量值
	```
	frame2['debt']=16.5#其实是对'debt'这一列的所有元素都赋值16.5
	```
	2. 如果将列表或者数组赋值给某个列的话，那其长度必须跟DataFrame的长度相匹配
	3. 如果赋值的是一个Series，就会匹配DataFrame的索引，也就是可能存在空位，那么都填上缺失值。
		
##### 添加新列
为不存在的列赋值会自动创建出一个序列
frame2之前没有'eastern'这一列可以直接 `frame2['eastern']=15 `，就会自动增加新列‘eastern’
##### 删除列
用del关键字
del frame2['eastern']

#### DataFrame常见方法
1. a.values
以二维ndarray的形式返回DataFrame中的数据。
2. a.index
3. a.colums	


### DataFrame的索引index
1. DataFrame的索引是不可改变的。
2. 索引index的常见方法和属性 见书《利用python进行数据分析》第126页（可能是137页）

# 基本功能
## 更换索引和列名 a.reindex([])和a.ix()
hotelminprice_comp.columns='hotelid','starttime','minprice'
### a.reindex()
1. 对于原先的数据obj,更换其索引值
```python
obj2=obj.reindex(['q','w','e'],fill_value=0)
```
上面的代码中。fill_value= 用于将更改索引后的新对象可能出现的缺失值设定为0，如果没用fill_value=的话，那么缺失值就默认为Nan.

2. 插值方法  method=
obj.reindex(data,method='具体方法')

3. a.reindex()也可以修改列名，或者两个都修改。如果仅传入一个序列，则会重新索引行。
```python
frame=DataFrame(data,index=[],columns=[])
#修改列名
frame.reindex(columns=[...] )
#索引和列名一起x修改
frame.reindex(index=[...],columns=[...] )
```

### a.ix()
frame.ix(['a','b'],['v','r']) #前一个是修改索引，后一个是修改列名
## 丢弃指定轴上的项
用a.drop()的方法，既可以丢弃索引，也可以丢弃列名。产生的是新对象
### 对于Series
```python
obj=Series(data,index=['q','r','y','u','o','m'])
new_ogj=ogj.drop(['o','m'])

```
###对于DataFrame
默认丢弃行 data.drop(['q','t'])
丢弃列 data.drop(['q','t'],axis=1)

## 索引、切片、选取和过滤
### 对于Series
通过索引来切片
obj[['y','w']] ,  obj['y':'w'](仅仅这种情况包含末端)
通过数据的位置
obj[[1,5]],obj[2:7],
### 对于DataFrame　
汇总的方法见书《利用python进行数据分析》的第132页（１４３页）表５－６
１．　获取列
data[['asd','qwe','yui']] , data['gfhg']
2.   获取行

	*　通过切片的方式data[2:6]

	*  通过布尔型数据选择行
		data[data['列名']>4]
	*  通过索引字段 ix
		data.ix[['行名','..','..']，['列名','..','..']] 
		data.ix[2]表示第３行
	


## 算术运算和数据填充
一般计算时，会根据索引进行匹配，然后计算。如果有的数据不匹配，那该索引或者列依然会出现，只是结果为ＮＡｎ。要想解决这种问题，那就用　运算方法和他的fill_value=这个参数。
同时DataFrame与Series运算时，一般是行运算，要想解决这种问题，那就用　运算方法和他的axis＝指定轴。
运算方法：以下分别为　+-*/
ａ.add(b,axis=0,fill_value=0)　
ａ.subb,axis=0,fill_value=0)　
ａ.div(b,axis=0,fill_value=0)　
ａ.mul(b,axis=0,fill_value=0)　

## apply()函数的运用
## 排序
用sort_index()
### 对于Ｓｅｒｉｃｅｓ
１．按照索引排序
obj.sort_index()
２．　按照值排序
obj.order()
### 对于DataFrame
1. 按照索引排序
可以根据任意一个轴上的索引进行排序
frame.sort_index()对行索引排序
obj.sort_index(axis=1)对列排序
２．　按照值排序
根据一个或多个列进行排序
用ａ.sort_index(by=['列名１','列名２'])

## 排名
用a.rank()并不知道他有什么用
## 行索引有重复值的情况
比如a=DataFrame(data,index=['a','a','a','a','b'])
发现这种a的行索引有４行都是'a'，但是这是正确的语法。如果上面输出'a'的话，那么４行数据将一起输出。
可以赢a.index.is_unique看结构的行索引是否有重复值，即是否唯一。

## 汇总和计算描述，数理统计
### 数理统计　相关方法
相关系数corr()	协方差cov()
series　是：a.corr(b)  , a.cov(b) 其中a,b都为Series,返回的是一个数值
DataFrame　是：frame.corr() , frame.cov() ,  返回的是没两个列之间的数值，所以结果是一个矩阵。是自己的列与自己的另一列的计算值。
用DataFrame的corrwith(),就可以计算DataFrame与其他的Series,或DataFrame的相关系数了。frame.corrwith(a)



![图片](http://img.blog.csdn.net/20160811104147170)
![这里写图片描述](http://img.blog.csdn.net/20160811104156657)
见书１４４页（ｐｄｆ１５５页）。
比如求和方法 frame.sum()　　有axis= ,和　skipna=True
用a.describe()把所有的情况都打印出来了。

一般是对列求和，可以通过frame.sum(axis=1)来指定轴
运算时，如有ＮａＮ的话，如果某一列全为NaN，那么结果就为NaN.如果那一列不是，那么系统会把那一列的NaN去掉，仅仅对正常数据运算。可以用skipna=False解决，这样只要某一列有一个ＮＡＮ,那么那一列结果就为NaN。
### 唯一值，值计算，成员资格访问
obj.unique()　，　obj.value_counts()  ,obj.isin(['a','t'])
![这里写图片描述](http://img.blog.csdn.net/20160811111524375)

# 处理缺失数据
## 缺失值处理方法
![这里写图片描述](http://img.blog.csdn.net/20160812183920342)
## 滤除缺失数据
用dropna
１．对于Series
方法１:dropna返回一个仅含非空数据和索引的Series
data.dropna()
方法２：data[data.notnull()]
2. 对于DataFrame
dropna默认丢弃任何含有缺失值的行
传入how='all',将只丢弃全为ＮＡ的那些行
传入axis=1,就可以丢弃列


## 填充缺失数据
用方法fillna完成
data.fillna(2) #所有的缺失值都填为2
若传入字典，则可以对不同的列实行填充. data.fillna({'列名１'：２，＇列名９＇：６})
fillna默认会返回新对象，但是也可以对现有的对象进行修改．
可以对fillna传入对reindex有效的插值方法

fillna函数的参数
![这里写图片描述](http://img.blog.csdn.net/20160812185603992)

## 层次化索引
没怎么看，估计用不到，用到了再看吧！！！

##　整数索引
１．一般索引是整数时，可能会引起莫名奇妙的错误．因为你索引时，python并不知道你这是基于　标签的索引，还是　　基于位置的索引．但是如果索引不是非整数，那么就不存在这个问题．
２．如果你轴索引含有索引器，那么根据整数进行数据选取的操作将总是面向标签的．（不是很懂）
### Series的iget_value和DataFrame的irow，icol　　，data.iloc[]
data.loc[..,..]是用标签索引

他们都是基于　位置的索引，而不是标签的索引．

### DataFrame data.iloc[]
data.iloc[:,0:5]
DataFrame data.iloc[]是基于　位置的索引，非常好用
# 数据读取，存储
读取文本格式数据
read_csv(),默认分割符为＇，＇  read_table()默认分割符为＇\t＇
二者可以混用，只需更改参数sep=','
有的表格的分隔符混用，很混乱，这时用以上两个函数时，在设置sep=　的值时，要考虑正则表达式
`read_csv()`　　和　`read_table()`　函数参数
![这里写图片描述](http://img.blog.csdn.net/20160812193812501) 
![这里写图片描述](http://img.blog.csdn.net/20160812193823892) 
![这里写图片描述](http://img.blog.csdn.net/20160812193831798)











