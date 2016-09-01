1. 以后用graphlab继续数据分析，因为他的data.show()真的是太好用了
2. graphlab可以和pandas.dataframe格式互换
```
data=pd.DataFrame()
g=graphlab.SFrame(data)
f=g.to_dataframe()
```
