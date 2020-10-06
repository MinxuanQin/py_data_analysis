Pandas 是 python的第三方库，提供高性能易用数据类型和分析工具。基于numpy实现，常与Numpy与Matplotlib一同使用。  

### 引用
`import pandas as pd`

### 理解
2个数据类型：Series, DataFrame  
基于上述类型的各类操作：基本操作，运算操作，特征类操作，关联类操作  

### Series类型
由一组数据和与之相关的数据索引组成  
index_0 --> data_a  
index_1 --> data_b  
index_2 --> data_c  
index_3 --> data_d  
可由以下类型创建：Python列表，标量值，字典，ndarray，其他函数。
+ Python列表
```
import pandas as pd
b = pd.Series([9,8,7,6],index=['a','b','c','d'])
```
index与列表元素个数一致  
+ 标量值  
```
s = pd.Series(25,index = ['a','b','c'])
```
index不能省略;表达尺寸  
+ 字典  
```
d = pd.Series({'a':9,'b':8,'c':7})
d = pd.Seires({'a':9,'b':8,'c':7}, index = ['c','a','b','d'])
#d将会显示为NaN
```
键表示索引，index从字典中进行选择操作
+ ndarray
```
import numpy as np
import pandas as pd
n = pd.Series(np.arange(5), index = np.arange(9,4,-1))
```
索引和数据都可以通过ndarray类型创建  
+ 基本操作  
类似ndarray类型和字典类型  
```
import pandas as pd
b = pd.Series([9,8,7,6],index=['a','b','c','d'])
b.index  #获得数据
b.values  #获得索引
```
第三行代码结果为`Index(['a','b','c','d'],dtype='object')`;  
第四行代码结果为`array([9,8,7,6], dtype=int64)`  
```
b['b']
b[1]  #自定义索引和自动索引并存，但不能混用
```
Numpy的运算和操作可用于Series类型  
可以通过自定义索引的列表/自动索引进行切片  
存在保留字in操作  
使用.get()方法  
自动对齐不同索引的数据  
名字存储在.name中，可以随时修改  

### DataFrame类型  
由共用相同索引的一组列组成  
index_0 --> data_a  data_1  data_w  
index_1 --> data_b  data_2  data_x  
index_2 --> data_c  data_3  data_y  
index_3 --> data_d  data_4  data_z  
表格型数据类型，每列值类型可以不同，既有行索引(index)又有列索引(column)（行axis=0;列axis=1）  
可由ndarray，字典，Series，其他DataFrame类型创建  
+ 二维ndarray对象  
```
d = pd.DataFrame(np.arange(10).reshape(2,5))
#有自动行索引和自动列索引
```
+ 一维ndarray对象字典创建  
```
dt = {'one': pd.Series([1,2,3], index=['a','b','c']),
      'two': pd.Series([9,8,7,6], index=['a','b','c','d'])}
#'one','two'为列索引
pd.DataFrame(dt, index=['b','c','d'],column=['two','three'])
#output:
#  two three
#b  8   NaN
#c  7   NaN
#d  6   NaN
#数据根据行列索引自动补齐
```
+ 列表类型字典创建  
```
dl={'one':[1,2,3,4],'two':[9,8,7,6]}
d = pd.DataFrame(dl,index=['a','b','c','d'])
```

属性包括：d.index,d.columns,d.values(输出显示dtype='object')  
*输出`d.ix['c2']`可以得到一行数据*  
基本操作类同Series，依据行列索引；DataFrame是二维带标签数组  

### Pandas库的数据类型操作  
+ 增加/重排：重新索引`.reindex(index=[...]/columns=[...])`;删除：`drop([...])`(删除列时添加参数axis=1)  

|参数|说明|
|---|---|
|index,columns|新的自定义索引|
|fill_value|重新索引时，用于填充缺失位置的值|
|method|填充方法。ffill当前值向前填充，bfill向后|
|limit|最大填充量|
|copy|默认True，**生成新的对象**，False时，新旧相等不复制|
```
newc = d.columns.insert(4,'新增')  #4是自动列索引
newd = d.reindex(columns = newc, fill_value = 200)
```
+ 索引类型  
Series和DataFrame的索引是Index类型，不可修改  

|方法|说明|
|--|--|
|.append(idx)|连接另一个Index对象，产生新的|
|.diff(idx)|计算差集，产生新的|
|.intersection(idx)|计算交集|
|.union(idx)|计算并集|
|.delete(loc)|删除loc处元素|
|.insert(loc,e)|在loc处增加新元素e|

### Pandas库数据类型运算  
+ 算数运算根据行列索引自动补齐后运算，默认产生浮点数  
+ 补齐自动填充NaN(空值)
+ 方法形式运算：  
`.add/sub/mul/div(d,**argws)`可选参数，如`fill_value`(替代NaN后参与运算)
+ 不同维度为广播运算，一维Series默认在轴1参与运算(axis=0指定列运算)
+ 比较运算：只比较相同索引，不补齐;不同维度间进行广播运算

### 数据排序  
* `.sort_index(axis=0,ascending=True)`在指定轴(axis=0/1)根据索引进行排序，默认升序(ascending=True/False)  
* `Series.sort_values(axis=0,ascending=True)`/`DataFrame.sort_values(by,axis=0,ascending=True)`,'by'为axis轴上某个索引/索引列表，**NaN统一放到排序末尾**

### 基本统计分析
|方法|说明|
|--|--|
|.sum()|计算总和，按轴0计算，下同|
|.count()|非NaN值的数量|
|.mean(),.median()|算数平均值/算数中位数|
|.var(),.std()|方差/标准差|
|.min(),.max()|最小/最大值|
|.describe()|针对0轴（各列）的统计汇总，<br>*type为'pandas.core.series.Series'/'pandas.core.frame.DataFrame'*|
|.argmin()/.argmax()|适用于Series,计算数据最大/最小所在位置的索引位置（自动索引）|
|.idxmin()/.idxmax()|适用于Series,计算数据最大/最小所在位置的索引（自定义索引）|

### 累计统计函数  
|方法|说明|
|---|---|
|.cumsum()|累计和
|.cumprod()|累计积
|.cummax()/.cummin()|最大/最小值

滚动计算（窗口计算）`.rolling(w).sum()/mean,var,std,min,max`(位置不足以窗口运算时输出NaN)

### 相关性分析  
+ 协方差（>0正相关，=0独立无关）`.cov()`计算协方差矩阵  
+ Poisson相关系数（r取值范围[-1,1]）`.corr()`计算相关系数矩阵，Pearson,Spearman,Kendall等系数  
