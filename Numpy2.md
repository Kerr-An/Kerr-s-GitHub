
# 1、花式索引
切片只能支持连续或等间隔的切片操作，要想实现任意位置的操作，需要使用花式索引fancy slicing

## 1.1、一维花式索引


```python
import numpy as np
```


```python
a = np.arange(0,100,10)
a
```




    array([ 0, 10, 20, 30, 40, 50, 60, 70, 80, 90])



### 花式索引需要指定索引位置（通过列表来索引）


```python
index = [1,2,-3]
y = a[index]
print(y)
```

    [10 20 70]
    

### 使用布尔数组来花式索引


```python
mask = np.array([0,2,2,0,0,1,0,0,1,0],dtype=bool)
mask
```




    array([False,  True,  True, False, False,  True, False, False,  True,
           False])




```python
a[mask]  # mask的长度必须和a相同
```




    array([10, 20, 50, 80])



# 1.2、二维花式索引

## 二维花式索引，需要给定行和列的值：


```python
a = np.array([[0,1,2,3,4,5],[6,7,8,9,10,11],[12,13,14,15,16,17],[18,19,20,21,22,23],[24,25,26,27,28,29],[30,31,32,33,34,35]])
a
```




    array([[ 0,  1,  2,  3,  4,  5],
           [ 6,  7,  8,  9, 10, 11],
           [12, 13, 14, 15, 16, 17],
           [18, 19, 20, 21, 22, 23],
           [24, 25, 26, 27, 28, 29],
           [30, 31, 32, 33, 34, 35]])



## for example:返回一条次对角线的值[1，8，15，22，29]


```python
a[[0,1,2,3,4],[1,2,3,4,5]]
```




    array([ 1,  8, 15, 22, 29])



## 返回最后三行的第1，3，5列


```python
a[-3:,[0,2,4]]
```




    array([[18, 20, 22],
           [24, 26, 28],
           [30, 32, 34]])



## 同样也可以使用mask索引


```python
mask = np.array([1,0,1,0,0,1],dtype=bool)
a[mask,2]
```




    array([ 2, 14, 32])



# 1.3、“不完全”索引

### 只给定索引的时候，返回整行或整列


```python
y = a[:3]
y
```




    array([[ 0,  1,  2,  3,  4,  5],
           [ 6,  7,  8,  9, 10, 11],
           [12, 13, 14, 15, 16, 17]])



### 此时也可使用花式索引去吃第2、3、5行：


```python
con = np.array([0,1,1,0,1,0],dtype=bool)
a[con]
a[con,con]  # 这个并不是取2、3、5行和2、3、5列的交矩阵，
# 而是输出[2,2][3,3][5,5]对应值
```




    array([[ 6,  7,  8,  9, 10, 11],
           [12, 13, 14, 15, 16, 17],
           [24, 25, 26, 27, 28, 29]])






    array([ 7, 14, 28])



### for example:


```python
con1 = np.array([0,1,0,1,0,1],dtype=bool)
con2 = np.array([1,0,1,0,1,0],dtype=bool)
a
a[con1]  # 偶数行
a[con2]  # 奇数行
a[:,con1]  #偶数列
a[:,con2]  #奇数列
a[con1,con2]
```




    array([[ 0,  1,  2,  3,  4,  5],
           [ 6,  7,  8,  9, 10, 11],
           [12, 13, 14, 15, 16, 17],
           [18, 19, 20, 21, 22, 23],
           [24, 25, 26, 27, 28, 29],
           [30, 31, 32, 33, 34, 35]])






    array([[ 6,  7,  8,  9, 10, 11],
           [18, 19, 20, 21, 22, 23],
           [30, 31, 32, 33, 34, 35]])






    array([[ 0,  1,  2,  3,  4,  5],
           [12, 13, 14, 15, 16, 17],
           [24, 25, 26, 27, 28, 29]])






    array([[ 1,  3,  5],
           [ 7,  9, 11],
           [13, 15, 17],
           [19, 21, 23],
           [25, 27, 29],
           [31, 33, 35]])






    array([[ 0,  2,  4],
           [ 6,  8, 10],
           [12, 14, 16],
           [18, 20, 22],
           [24, 26, 28],
           [30, 32, 34]])






    array([ 6, 20, 34])




```python
b = np.array([[0,1,2,3],[4,5,6,7],[8,9,10,11],[12,13,14,15]])
b
index1 = np.array([1,1,0,1],dtype=bool)
index2 = np.array([1,0,0,0],dtype=bool)
b[index1,index2]
index3 = np.array([1,0,1,0],dtype=bool)
index4 = np.array([0,1,0,1],dtype=bool)
b[index3,index4]
```




    array([[ 0,  1,  2,  3],
           [ 4,  5,  6,  7],
           [ 8,  9, 10, 11],
           [12, 13, 14, 15]])






    array([ 0,  4, 12])






    array([ 1, 11])



# 1.4、where函数

## 一维数组


```python
a = np.array([0,12,5,20])
```

### 判断数组中元素是不是大于10：


```python
np.where(a>10)
```




    (array([1, 3], dtype=int64),)



### where的返回值是一个元组。返回的是索引位置

### 也可直接用数组操作


```python
a > 10
```




    array([False,  True, False,  True])




```python
a[a>10]
```




    array([12, 20])




```python
a[np.where(a>10)]
```




    array([12, 20])



# 2、数组类型

### 类型转换


```python
a = np.array([1.5,-3],dtype=float)
a
```




    array([ 1.5, -3. ])



## asarray函数


```python
a = np.array([1,2,3])
np.asarray(a,dtype=float)
a
```




    array([1., 2., 3.])






    array([1, 2, 3])



## astype函数
astype函数会生成一个新数组


```python
a = np.array([1,2,3])
a.astype(float)
a
```




    array([1., 2., 3.])






    array([1, 2, 3])



# 3、数组操作

## 豆瓣十部高分电影为例


```python
## 电影名称
mv_name = ['肖生克的救赎','控方证人','美丽人生','阿甘正传','霸王别姬','提坦尼克号','辛德勒的名单','这个杀手不太冷','9','10']
```


```python
## 评分人数
mv_num = np.array([692795,42992,327855,590893,478523,157074,306904,662552,284652,159302])
```


```python
## 评分
mv_score = np.array([9.6,9.5,9.5,9.4,9.4,9.4,9.4,9.3,9.3,9.3])
```


```python
## 电影时长（分钟）
mv_length = np.array([142,116,116,142,171,194,195,133,109,92])
```

## 数组排序

### sort函数


```python
np.sort(mv_num)
```




    array([ 42992, 157074, 159302, 284652, 306904, 327855, 478523, 590893,
           662552, 692795])




```python
mv_num
```




    array([692795,  42992, 327855, 590893, 478523, 157074, 306904, 662552,
           284652, 159302])



### argsort函数
将原数组排序返回对应的索引号


```python
order = np.argsort(mv_num)
order
```




    array([1, 5, 9, 8, 6, 2, 4, 3, 7, 0], dtype=int64)




```python
mv_name[order[0]]  # 评分人数最少的电影
mv_name[order[-1]]  # 评分人数最多的电影
```




    '控方证人'






    '肖生克的救赎'




```python
# 此单元内容忽略
# arr1：2011-2018本二最低控制线
# arr2：2011-2018本二C最低控制线
arr1 = [496,492,459,478,462,460,452,476]
arr2 = [390,398,380,375,398,370,335,363]
a = np.array(arr1)
b = np.array(arr2)
print('本二C控制线和本二控制线分数差：',a-b)
```

    本二C控制线和本二控制线分数差： [106  94  79 103  64  90 117 113]
    

## 求和


```python
np.sum(mv_num)
```




    3703542




```python
mv_num.sum()
```




    3703542



## 最大值


```python
np.max(mv_length)
```




    195




```python
mv_length.max()
```




    195



## 最小值


```python
np.min(mv_score)
```




    9.3




```python
mv_score.min()
```




    9.3



## 均值


```python
np.mean(mv_length)
```




    141.0




```python
mv_length.mean()
```




    141.0



## 标准差


```python
np.std(mv_length)
```




    33.713498780162226




```python
mv_length.std()
```




    33.713498780162226



## 相关系数矩阵


```python
np.cov(mv_score,mv_length)
```




    array([[9.88888889e-03, 4.55555556e-01],
           [4.55555556e-01, 1.26288889e+03]])



# 多维数组操作

## 数组形状


```python
a = np.arange(6)
a
```




    array([0, 1, 2, 3, 4, 5])




```python
a.shape = (2,3)
a
```




    array([[0, 1, 2],
           [3, 4, 5]])




```python
a.shape
```




    (2, 3)




```python
a
```




    array([[0, 1, 2],
           [3, 4, 5]])



## shape会改变原数组，而reshape不会


```python
a = np.arange(6)
a
```




    array([0, 1, 2, 3, 4, 5])




```python
a.reshape(2,3)
```




    array([[0, 1, 2],
           [3, 4, 5]])




```python
a
```




    array([0, 1, 2, 3, 4, 5])



## 转置


```python
a = a.reshape(2,3)
a
```




    array([[0, 1, 2],
           [3, 4, 5]])




```python
a.T
```




    array([[0, 3],
           [1, 4],
           [2, 5]])




```python
a.transpose()
```




    array([[0, 3],
           [1, 4],
           [2, 5]])




```python
a  # a并没有变化
```




    array([[0, 1, 2],
           [3, 4, 5]])



# 数组连接

## concatenate((a0,a1,...,aN),axis=0),axis = 0是按列拼接，1为行


```python
x = np.array([[0,1,2],[10,11,12]])
y = np.array([[50,51,52],[60,61,62]])
print(x.shape)
print(y.shape)
```

    (2, 3)
    (2, 3)
    

## 默认纵向拼接


```python
z = np.concatenate((x,y))
z
```




    array([[ 0,  1,  2],
           [10, 11, 12],
           [50, 51, 52],
           [60, 61, 62]])




```python
z = np.concatenate((x,y),axis=1)
z
```




    array([[ 0,  1,  2, 50, 51, 52],
           [10, 11, 12, 60, 61, 62]])



## x和y的形状是一样的，还可以将他们连接成三维数组
通过两个二维，再增加一个维度


```python
z = np.array((x,y))
z
```




    array([[[ 0,  1,  2],
            [10, 11, 12]],
    
           [[50, 51, 52],
            [60, 61, 62]]])



## 对应数组堆叠的以上三种情况，也有对应的三个函数
vstack
hstack
dstack


```python
np.vstack((x,y))
```




    array([[ 0,  1,  2],
           [10, 11, 12],
           [50, 51, 52],
           [60, 61, 62]])




```python
np.hstack((x,y))
```




    array([[ 0,  1,  2, 50, 51, 52],
           [10, 11, 12, 60, 61, 62]])




```python
np.dstack((x,y))
```




    array([[[ 0, 50],
            [ 1, 51],
            [ 2, 52]],
    
           [[10, 60],
            [11, 61],
            [12, 62]]])



# numpy内置函数


```python
a = np.array([-1,0,5,-5,3])
```


```python
np.abs(a)  # 绝对值
```




    array([1, 0, 5, 5, 3])




```python
np.exp(a)  # 指数e
```




    array([3.67879441e-01, 1.00000000e+00, 1.48413159e+02, 6.73794700e-03,
           2.00855369e+01])




```python
np.median(a)  # 中值
```




    0.0




```python
np.cumsum(a)  # 累计和
```




    array([-1, -1,  4, -1,  2], dtype=int32)



# numpy内置函数非常多，不需要死记硬背，要懂得查资料
