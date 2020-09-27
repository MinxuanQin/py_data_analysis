NumPy 的random子库： `np.random.*`  

函数|说明
---|---
rand(d0,d1,..,dn)|浮点数，[0,1),均匀分布，参数表示返回数组的维度信息
randn(d0,d1,..,dn)|标准正态分布
randint(low[,high,shape])|根据shape创建随机整数或整数数组，范围是[low,high)
seed(s)|随机数种子，s是给定的随机值
shuffle(a)|根据数组a的第一轴进行随排列，改变数组x
permutation(a)|同上产生新的乱序数组，不改变x
choice(a[,size,replace,p])|从一维数组a以概率p抽取元素，形成size形状新数组。replace表示是否可以重用元素，默认为False
uniform(low,high,size)|均匀分布
normal(loc,scale,size)|正态分布，loc均值，scale标准差
poisson(lam,size)|泊松分布，lam随机事件发生率  

NumPy 的统计函数： `np.*`

函数|说明
---|---
sum,mean,average,std,var|axis=None是统计函数标配参数
min,max|最小值，最大值
argmin,argmax|...的降一维下标
unravel_index(index,shape)|由shape将一维下标转化为多维下标【几行几列】
ptp(a)|最大值最小值的差
median|中位数

梯度函数
`np.gradient(f)`
