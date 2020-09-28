### 基本图表函数  
| 函数 | 说明  |
| :------------- | :------------- |
| plt.plot(x,y,fmt,...) | 坐标图 |
| plt.boxplot(data.notch,position) | 箱型图 |
| plt.bar(left,height,width,bottom) | 条形图 |
| plt.barh(width,bottom,left,height) | 横向条形图 |
| plt.polar(thata,r) | 极坐标图 |
| plt.pie(data,explode) | 饼图 |
| plt.psd(x,NFFT=256,pad_to,Fs) | 功率谱密度图 |
| plt.specgram(x,NFFT=256,pad_to,F) | 谱图 |
| plt.cohere(x,y,NFFT=256,Fs) | X-Y相关性函数 |
| plt.scatter(x,y) | 散点图，x和y长度相同 |
| plt.step(x,y,where) | 步阶图 |
| plt.hist(x,bins,normed) | 直方图 |
| plt.contour(X,Y,Z,N) | 等值图 |
| plt.vlines() | 垂直图 |
| plt.stem(x,y,linefmt,markerfmt) | 柴火图 |
| plt.plot_date() | 数据日期 |

### 饼图绘制
```
import matplotlib.pyplot as plt

labels = 'Frogs', 'Hogs', 'Dogs', 'Logs'
sizes = [15, 30, 45, 10]
explode = (0, 0.1, 0, 0)

plt.pie(sizes, explode=explode, labels=labels,
        autopct='%1.1f%%', shadow=False, startangle=90)
plt.show()
```
[解释文档链接](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.pie.html)
![结果实例1](https://github.com/MinxuanQin/pics/blob/master/pyw2/pie_1.png)  

### 直方图绘制
```
import matplotlib.pyplot as plt
import numpy as np

np.random.seed(0)
mu, sigma = 100, 20
a = np.random.normal(mu, sigma, size = 100)

plt.hist(a,20,density = True, histtype='stepfilled', facecolor='b',
         alpha=0.75)
plt.title('Histogram')

plt.show()
```
[解释文档链接](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.hist.html)
+ density 表示 norme = 1  
+ alpha 表示不透明度  

![结果示例：bar = 20](https://github.com/MinxuanQin/pics/blob/master/pyw2/hist_1.png)  
![结果示例：bar = 40](https://github.com/MinxuanQin/pics/blob/master/pyw2/hist_2.png)

### 极坐标图绘制  
```
import numpy as np
import matplotlib.pyplot as plt

N = 20
theta = np.linspace(0.0,2*np.pi,N,endpoint=False)  #角度数据
radii = 10*np.random.rand(N)   #级径数据
width = np.pi / 4 * np.random.rand(N)   #极区所占区域

ax = plt.subplot(111,projection= 'polar')
bars = ax.bar(theta,radii,width=width,bottom=0.0)

for r,bar in zip(radii, bars):
    bar.set_facecolor(plt.cm.viridis(r/10.))  #颜色深浅与极径大小有关
    bar.set_alpha(0.5)

plt.show()
```
![结果示例1,N = 20](https://github.com/MinxuanQin/pics/blob/master/pyw2/polar_1.png)
![结果示例2,N = 40](https://github.com/MinxuanQin/pics/blob/master/pyw2/polar_2.png)  
```
import numpy as np
import matplotlib.pyplot as plt

N=20
theta = np.linspace(0,2*np.pi,N,endpoint=False)
radii = 10*np.random.rand(N)

plt.polar(theta, radii)
plt.show()
```
![结果示例3,用plt.polar()作画](https://github.com/MinxuanQin/pics/blob/master/pyw2/polar_3.png)

### 散点图绘制  
```
import numpy as np
import matplotlib.pyplot as plt

fig, ax = plt.subplots()  #第一返回值为figure,后续为subplots
ax.plot(10*np.random.randn(100),10*np.random.randn(100),'o')
ax.set_title('Simple Scatter')

plt.show()
```
![结果示例1,使用random库函数](https://github.com/MinxuanQin/pics/blob/master/pyw2/scatter_1.png)
```
import numpy as np
import matplotlib.pyplot as plt

theta = np.arange(0,2*np.pi, np.pi/4)  # 数据角度
r = np.arange(1,9,1)  #数据极径
area = 100*np.arange(1,9,1)  # 数据散点面积
colors = theta

ax2 = plt.subplot(111,projection='polar')
ax2.scatter(theta, r, c=colors, s=area, cmap = 'hsv', alpha =0.75)

plt.show()
```
![结果示例2,集散点图](https://github.com/MinxuanQin/pics/blob/master/pyw2/scatter_2.png)
```
plt.scatter(10*np.random.randn(100),10*np.random.randn(100))
```
![结果示例3,使用plt.scatter()](https://github.com/MinxuanQin/pics/blob/master/pyw2/scatter_3.png)
