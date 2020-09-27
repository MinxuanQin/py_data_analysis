## Matplotlib库
[Matplatlib库效果](http://matplotlib.org/gallery.html)  

matplotlib由各种可视化类组成，`matplotlib.pyplot`是绘制各种可视化图形的子库。
```
import matplotlib.pyplot as plt
plt.plot([0,2,4,6,8],[3,1,4,5,2])
plt.ylabel("Grade")
plt.axis([-1,10,0,6])
plt.savefig('test', dpi = 600)  #存为png文件
plt.show()
```
![exp1](https://github.com/MinxuanQin/py_data_analysis/blob/master/Fig_exp1.png)  
+ 输入一个列表/数组时，参数被当作y轴，x轴以索引自动生成。  
+ 当有两个以上参数时，按照x轴和y轴顺序绘制数据点。  
+ `plt.axis([xmin,xmax,ymin,ymax])`用于界定x轴y轴范围。  

##### pyplot绘图区域
`plt.subplot(nrows, ncols, plot_number)` 指定添加的子图位置，表示在包含nrows行ncols的网格中（**即划定大小**）占据第index个位置。index是从最左上角开始向右从1计数的。去掉逗号需要令三个参数每一个都小于10。    
```
import numpy as np
import matplotlib.pyplot as plt

def f(t):
  return np.exp(-t) * np.cos(2*np.pi*t)

a = np.arange(0.0, 5.0, 0.02)

plt.subplot(211)
plt.plot(a, f(a))

plt.subplot(212)
plt.plot(a, np.cos(2*np.pi*t), 'r--')
plt.show()
```

##### plot()函数
`plt.plot(x, y, format_string, **kwargs)`  
+ format_string: 控制曲线格式字符串;=颜色字符+风格字符+标记字符  
+ **kwargs: 第二组或更多(x,y,format_string)
[linestyle('dashed'),marker('o'),markerfacecolor('blue'),markersize(20)...]  
*绘制多条曲线时，各曲线x不能忽略*  

|颜色|说明|颜色|说明|
|----|:--:|----|:--:|
|'b'|蓝|'m'|洋红，magenta|
|'g'|绿|'y'|黄|
|'r'|红|'k'|黑|
|'c'|青绿，cyan|'w'|白|
#008000|RGB某颜色|'0.8'|灰度值字符串|

![color example](https://github.com/MinxuanQin/pics/blob/master/pyw2/exp3.png)  

|风格字符|说明
|:-----:|:---:|
|'-'|实线|
|'--'|破折线|
|'-.'|点划线|
|':'|虚线|
|'' ''|无线条|

![style example](https://github.com/MinxuanQin/pics/blob/master/pyw2/exp4.png)

|标记字符|说明|标记字符|说明|标记字符|说明|
|:--:|:--:|:-------:|:---:|:----:|:---:|
|'.'|点标记|'1'|下花三角|'h'|竖六边形|
|','|像素标记<br>（极小点）|'2'|上花三角|'H'|横六边形|
|'o'|实心圈|'3'|左花三角|'+'|十字|
|'v'|倒三角|'4'|右花三角|'x'|x标记|
|'^'|上三角|'s'|实心方形|'D'|菱形|
|'>'|右三角|'p'|实心五角|'d'|瘦菱形|
|'<'|左上角|'*'|星形|'|'|垂直线|

![mark example](https://github.com/MinxuanQin/pics/blob/master/pyw2/exp5.png)  

##### pyplot中文显示  
1. `matplotlib.rcParams['font.family'] = 'SimHei'`  'SimHei'表示黑体  

|属性|说明|
|:--|:---|
|'font.family'|显示字体名字|
|'font.style'|字体风格,'normal'/'italic'（斜体）|
|'font.size'|字体大小，整数字号或'large','x-small'|  

`rcParams['font.family']`  
|中文字体|说明|
|-------|----|
|'SimHei'|中文黑体|
|'Kaiti'|中文楷体|
|'LiSu'|中文隶书|
|'FangSong'|中文仿宋|
|'YouYuan'|中文幼圆|
|'STSong'|华文宋体|  

2. 在有中文输出的地方添加 fontproperties
```
plt.xlabel('横轴：时间',fontproperites = 'SimHei',fontsize = 20)
plt.ylabel('纵轴：振幅',fontproperites = 'SimHei',fontsize = 20)
```
##### pyplot文本显示  
|函数|说明|
|---|----|
|plt.xlabel()<br>plt.ylabel()|对x/y轴添加文本标签|
|plt.title()|对图形整体添加文本标签|
|plt.text()|在任意位置增加文本|
|plt.annotate()|增加带箭头注解|

+ `plt.annotate(s, xy=arrow_crd, xytexy = text_crd, arrowprops = dict)`  
![实例效果（含注解）](https://github.com/MinxuanQin/pics/blob/master/pyw2/exp9.png)

##### pyplot子绘图区域  
`plt.subplot2grid(GridSpec, CurSpec, colspan=1, rowspan=1)`  
设定网格(GridSpec)，选中网格(CurSpec)，确定选中行列区域位置(设定大小)，编号从0开始(适用于CurSpec)  
+ GridSpec类
```
import matplotlib.gridspec as gridspec

gs = gridspec.GridSpec(3,3)

ax1 = plt.subplot(gs[0,:])
ax2 = plt.subplot(gs[1,:-1])
ax3 = plt.subplot(gs[1:,-1])
ax4 = plt.subplot(gs[2,0])
ax5 = plt.subplot(gs[2,1])
```
![实例效果（子绘图分区）](https://github.com/MinxuanQin/pics/blob/master/pyw2/exp10.png)
