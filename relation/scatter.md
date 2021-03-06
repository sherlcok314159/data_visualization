### 散点图
散点图绘图时**必须成对**

散点图可对**连续**的两个值的**关系**进行可视化

*A.matplotlib*
```python
import matplotlib.pyplot as plt
from random import randint

#强正相关
x = [range(1,100)]
y = [range(1,100)]
plt.scatter(x,y)
plt.show()

#强负相关
x = [range(1,100)]
y = [range(-1,-100,-1)]
plt.scatter(x,y)
plt.show()

#无相关
x = [randint(1,100) for i in range(100)]
y = [randint(1,100) for i in range(100)]
plt.scatter(x,y)
plt.show()
```

*注意*

*1.* 此处的*x,y*不需要用*numpy*处理，一维列表即可

*2.* 关于参数*marker*，一般默认很好，需要可以去查官方文档

*B.sns-relplot*
```python
import seaborn as sns
d = pd.read_csv("supermarket_sales - Sheet1.csv", parse_dates=["Date"])
#需要注意，parse_dates参数是为统一日期设置的，用的时候不能简单设置为True，要具体
sns.relplot(data = d,x = "Unit price",y = Total)
plt.show()
#关于它的kind参数默认为scatter,可以不写
#也可以像上面的写成
sns.relplot(x=d["Unit price"], y=d["Total"])
#会返回FutureWarning:……
#所以seaborn还是建议写成第一种格式
```
```python
#如果还是想用第一种，但看到warnings又烦
#可以选择过滤警告
import warnings
warnings.filterwarnings("ignore")
#原来的代码块
```

```python
#需要注意的是，sns绘图不接受二维及以上数组
x = [range(100)]#shape(1,100)
y = [range(100)]#shape(1,100)
sns.relplot(x,y)
plt.show()
#ValueError: setting an array element with a sequence.
```
*C.带拟合曲线的散点图*
```python
sns.regplot(x=d["Unit price"], y=d["Total"])
plt.show()
```

前两者绘图能力相差无几，但**sns-relplot会自动添加x,y标签**，较为方便,适合配合*pandas*进行处理数据

但*matplotlib绘图* **接受二维及以上数组**，有些时候可以有奇效

最后一个更适合查看连续值之间的关系，**拟合曲线**使数据之间的关系更加明了

总之，这些都是工具，不用太在意优化某一个，不同的工具不同的场合**挑最优**的用就行


**拓展**

可以利用相关性公式进行计算
```python
import numpy as np 
print(np.corrcoef(x,y))
#[[1. 1.]
# [1. 1.]]
# 因为值是重复出现的，所以一对就行了
print(np.corrcoef(x, y)[0])
#[[1. 1.]
```
- *0-0.09 无相关*
- *0.1-0.3 弱相关*
- *0.3-0.5 中相关*
- *0.5-1.0 强相关*
- *正数-正相关 负数-负相关*

