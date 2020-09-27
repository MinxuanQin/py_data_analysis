CSV文件读取
=====
CSV = Comma-Seperated Value,逗号分隔值  

1. `np.savetxt(frame, array, fmt = '%.18e', delimiter = None)`  
+ frame: 文件，字符产生器，可为.gz 或 .bz2 的压缩文件  
+ array: 存入文件的数组  
+ fmt: 写入文件的格式，例：%d, %.2f, %.18e *这里需要引号*
+ delimiter: 分隔字符串，默认是任何空格  

2. `np.loadtxt(frame, dtype = np.float, delimiter = None, unpack = False)`
+ frame: 同上  
+ dtype: 数据类型
+ delimiter: 同上
+ unpack: 若为True，读入属性将分别写入不同变量  

*delimiter很重要，写入不当会导致语法错误（如string无法转换）*

3. `a.tofile(frame, sep = '', format = '%s')`  
任意维度数据写入，sep为空串时写入文件为二进制  

4. `np.fromfile(frame, dtype = float, count = -1, sep = '')`  
任意维度数据读取  
+ count: 读入元素个数，-1表示读入整个文件  

5. 便捷文件存取  
`np.save(fname, array)`或`np.savez(fname, array)`
+ fname: 文件名，扩展名.npy,压缩扩展名.npz
+ array: 数组  
`np.load(fname)`
