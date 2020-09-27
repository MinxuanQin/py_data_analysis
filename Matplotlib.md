## Matplotlib库
[Matplatlib库效果](http://matplotlib.org/gallery.html)  

matplotlib由各种可视化类组成，`matplotlib.pyplot`是绘制各种可视化图形的子库。
```
import matplotlib.pyplot as plt
plt.plot([3,1,4,5,2])
ply.ylabel("Grade")
plt.savefig('test', dpi = 600)  #存为png文件
plt.show()
```
![exp1](https://github.com/MinxuanQin/py_data_analysis/blob/master/Fig_exp1.png)  
输入一个列表/数组时，参数被当作y轴，x轴以索引自动生成。
