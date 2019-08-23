
# numpy
## 数组与多维数组的切片和索引


```python
import numpy as np
a = [1,3,5,8,9]
b = np.array([a])
type(b)
print(b)
b.dtype
```




    numpy.ndarray



    [[1 3 5 8 9]]
    




    dtype('int32')




```python
type(b)
c = np.linspace(1,10,6)  # 生成1到10的个数为6的等差数列
c
```




    array([ 1. ,  2.8,  4.6,  6.4,  8.2, 10. ])




```python
# (0,1)的随机数
d = np.random.rand(10)
d
```




    array([0.25294249, 0.20044515, 0.96604538, 0.88388792, 0.61581266,
           0.69625725, 0.83506165, 0.01381954, 0.8949685 , 0.8492919 ])




```python
#  服从正态分布的随机数
e = np.random.randn(10)
e
```




    array([-0.54020389,  2.35006341,  0.52530327,  0.22099286,  1.00264978,
           -1.11837513,  0.81338041,  0.4403969 ,  0.17533863,  1.11411752])




```python
f = np.random.randint(1,10,5)
f
```




    array([6, 7, 4, 6, 4])




```python
b.shape
```




    (1, 5)




```python
b.size
```




    5




```python
b.ndim
```




    2




```python
e.shape  # 数列是一维的
```




    (10,)



# 索引和切片


```python
a = np.array([0,1,2,3])
a[0]
```




    0




```python
a[0]=10  # 修改第一个元素的值
a
```




    array([10,  1,  2,  3])




```python
a = np.array([11,12,13,14,15])  # 切片，支持负索引
a[1:3]
```




    array([12, 13])




```python
a[1:-2]  # 从索引号为1的开始取，取到倒数第3个数（左闭右开）
```




    array([12, 13])



# 省略参数


```python
a[-2:]  # 从倒数第二个取到最后一个数
```




    array([14, 15])




```python
a[::2]  # 从第1个数取到最后一个数，步长为2
```




    array([11, 13, 15])



# Example


```python
# 计算每日电影票房
ob = np.array([21000,22580,23860,25880,27650,29880])  # 累计票房
ob2 = ob[1:]
ob1 = ob[:-1]
ob2-ob1
```




    array([1580, 1280, 2020, 1770, 2230])



# 多维数组及其属性


```python
a = np.array([[0,1,2,3],[10,11,12,13]])
a
```




    array([[ 0,  1,  2,  3],
           [10, 11, 12, 13]])




```python
a.shape
```




    (2, 4)




```python
a.size
```




    8




```python
a.ndim
```




    2




```python
# 一个例子→贝塞尔函数

%matplotlib inline
import numpy as np
import matplotlib.pyplot as plt
from scipy.special import jn
from IPython.display import display, clear_output
import time
x = np.linspace(0,5)
f, ax = plt.subplots()
ax.set_title("Bessel functions")
for n in range(1,11):
   time.sleep(1)
   ax.plot(x, jn(x,n))
   clear_output(wait=True)
   display(f)    
plt.close()
```


![png](output_25_0.png)



```python
b = np.array([[1,2,3,4],[5,6,7,8],[9,10,11,12],[13,14,15,16]])
```


```python
b
b[1]
b[:,1]
b[1:3,1:3]
```




    array([[ 1,  2,  3,  4],
           [ 5,  6,  7,  8],
           [ 9, 10, 11, 12],
           [13, 14, 15, 16]])






    array([5, 6, 7, 8])






    array([ 2,  6, 10, 14])






    array([[ 6,  7],
           [10, 11]])



# 多维数组切片example


```python
c = np.array([[0,1,2,3,4,5],[6,7,8,9,10,11],[12,13,14,15,16,17],[18,19,20,21,22,23],[24,25,26,27,28,29],[30,31,32,33,34,35]])
c
```




    array([[ 0,  1,  2,  3,  4,  5],
           [ 6,  7,  8,  9, 10, 11],
           [12, 13, 14, 15, 16, 17],
           [18, 19, 20, 21, 22, 23],
           [24, 25, 26, 27, 28, 29],
           [30, 31, 32, 33, 34, 35]])



## 取出第一行的第4和第5个元素


```python
c[0,3:5]
```




    array([3, 4])



## 取出最后两行的最后两列


```python
c[-2:,-2:]
```




    array([[28, 29],
           [34, 35]])



## 取出第3、5行的奇数列 


```python
c[2::2,::2]  
# 行索引号为2（第3行）到最后，步长为2：即第3行和第5行；
# 列索引号为从开始到结束，步长为2：即所有奇数列
```




    array([[12, 14, 16],
           [24, 26, 28]])



# 切片的引用机制
## 引用机制意味着python没有为e分配新的空间来存储它的值而是让e指向了d所分配的内存空间，因此，改变e会改变d的值

## 这样做的好处是，对于很大的数组，不用大量复制多余的值，节省了空间。
## 缺点在于：可能会出现改变一个值而另一个值也被改变的情况
## 解决办法：使用copy()方法产生一个复制，这个复制会申请新的内存

### 切片的数据改变会造成原始数据的改变


```python
d = np.array([0,1,2,3,4])
```


```python
e = d[2:4]
e
```




    array([2, 3])




```python
e[0] = 10
d
```




    array([ 0,  1, 10,  3,  4])



### 使用copy()方法产生一个复制


```python
d = np.array([0,1,2,3,4])
e = d[2:4].copy()
e[0] = 10
d
```




    array([0, 1, 2, 3, 4])



## 列表中并不会出现这种情况 


```python
d = [0,1,2,3,4]
e = d[2:4]
e[0] = 10
d
```




    [0, 1, 2, 3, 4]


