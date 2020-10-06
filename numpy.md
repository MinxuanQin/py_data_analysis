Numpy库
=====
#### 引用
`import numpy as np`

#### N维数组对象：ndarray  
1. 去掉循环，更像单个数据  
2. 经过优化提升运算速度
3. 同类型 --》 节省运算及存储空间  
+ 实际数据+元数据（维度，类型）
+ 要求类型相同（同质），下标从0开始  
+ 输出为[]形式，元素由空格分割
+ 轴（axis）保存数据的维度；秩（rank）轴的数量  

属性 | 说明
--- | ---
.ndim|秩，即轴/维度数量
.shape|尺度，对于matrix，n行m列
.size|n*m
.dtype|ndarray对象元素类型
.itemsize|元素大小，以字节为单位

数据类型 | 说明
---|---
bool|True/False
intc|int32/64,同C中int
intp|int32/64,索引中整数，同C中ssize_t
int8|[-128,127]
int16|[-32768,32767]
int32|[-2^31,2^31 - 1]
int64|[-2^63,2^63 - 1]  
float16|16位半精度浮点数：1位符号位，5位指数，10位指数
float32|32位半精度浮点数：1位符号位，8位指数，23位指数
float64|64位半精度浮点数：1位符号位，11位指数，52位指数
complex32/64|复数，实部虚部均为32/64位浮点数

*与之相似的有uint8/16/32/64*  
**非同质ndarray对象尽量避免**  
dtype = object, 例：`np.array([ [0,1,2,3,4],[9,8,7,6] ])`  

#### 创建方法
1. Python中的列表，元组中,*允许混合*  
`x = np.array(list/tuple, dtype = np.float32)`
2. Numpy中函数，`arrage, ones, zeros`  

函数|说明
---|---
np.arange(n)|元素从n到n-1
np.ones(shape)|shape为元组类型，全1数组
np.zeros(shape)|全0数组<br>`np.zeros((3,6), dtype = np.int32)`
np.full(shape,val)|每个元素值为val
np.eye(n)|正方n*n单位矩阵，对角线为1，其余为0
np.ones_like(a)<br>np.zeros_like(a)<br>np.full_like(a,val)|根据数组a的形状
np.linspace()|根据起止数据等间距填充<br>`np.linspace(1,10,4)`<br>`np.linspace(1,10,4, endpoint = False)`
np.concatenate()|合并数组

3. 字节流中(raw butes)
4. 文件中读取特定形式  

#### ndarray数组的变换  
函数 | 说明
--- | ---
.reshape(shape)|不改变元素，原数组不变
.resize(shape)|修改原数组
.swapaxes(ax1,ax2)|调换两个维度
.flatten()|降维，返回折叠后的一维数组，原数组不变

**类型变换**：`new_a = a.astype(new_type)` 该指令一定会创建一个新的数组，即便两个类型一致  
**ndarray数组向列表转换**： `ls = a.tolist()`  

#### ndarray数组的操作  
索引：获取特定元素  
切片：获取元素子集  
*对多位数组：一个维度一个索引值，用逗号分隔

#### ndarray数组的运算  
1. 与标量的运算作用于每一个元素
2. numpy一元函数

函数|说明
---|---
np.abs(x)<br>np.fabs()|各元素绝对值
np.sqrt(x)|各元素平方根
np.square(x)|各元素平方
np.log(x)<br>np.log10(x)<br>np.log2(x)|计算对数
np.ceil(x)<br>np.floor(x)|计算各元素相应值
np.rint(x)|各元素四舍五入值
np.modf(x)|小数和整数部分以两个独立数组形式返回
np.cos(h)(x)<br>(sin,tan同理)|计算相应函数值
np.exp(x)|计算指数
np.sign(x)|各元素符合值：1，0，-1

3. numpy二元函数

|函数|说明
|---|---
|+ - * / **|各元素进行对应运算  
|np.maximum(x,y) np.fmax()<br>np.minimum(x,y) np.fmin()|最大值/最小值计算
|np.mod(x,y)|元素级模运算
|np.copysign(x,y)|数组y各元素的符号赋值给数组x对应元素
|> < >= <= == !=|算数比较，产生布尔型数组
