

```python
import pandas as pd
import numpy as np
```

# 1.1 Pandas 基本数据结构
有两种常用基本结构：
●Series:
  ●一维数组，与numpy中的类似，Series能保存不同的数据类型，字符串、boolean值、数字等。
●DataFrame
  ●二维的表格型数据结构，很多功能与R中的data.frame类似，可以将DataFrame理解为Series的容器。以下主要以DataFrame为主。
# 1.2 Pandas库的Series类型

### 1.2.1 一维Series可以用一维列表初始化


```python
s1 =  pd.Series([1,3,5,np.nan,6,8])
s1
print(s1)
```




    0    1.0
    1    3.0
    2    5.0
    3    NaN
    4    6.0
    5    8.0
    dtype: float64



    0    1.0
    1    3.0
    2    5.0
    3    NaN
    4    6.0
    5    8.0
    dtype: float64
    


```python
s2 =  pd.Series([1,3,5,np.nan,6,8],index=['a','b','c','d','e','f'])
s2
print(s2)
```




    a    1.0
    b    3.0
    c    5.0
    d    NaN
    e    6.0
    f    8.0
    dtype: float64



    a    1.0
    b    3.0
    c    5.0
    d    NaN
    e    6.0
    f    8.0
    dtype: float64
    

### 1.2.2 索引——数据的行标签


```python
s1.index
```




    RangeIndex(start=0, stop=6, step=1)




```python
s2.index
```




    Index(['a', 'b', 'c', 'd', 'e', 'f'], dtype='object')




```python
s1.values
```




    array([ 1.,  3.,  5., nan,  6.,  8.])




```python
s2.values
```




    array([ 1.,  3.,  5., nan,  6.,  8.])



### 1.2.3 值


```python
s1[0]
```




    1.0




```python
s1[5]
```




    8.0



### 1.2.4 切片


```python
s1[2:5]
```




    2    5.0
    3    NaN
    4    6.0
    dtype: float64




```python
s1[::2]
```




    0    1.0
    2    5.0
    4    6.0
    dtype: float64



### 1.2.5 索引赋值


```python
s1.index.name = '索引'
s1
```




    索引
    0    1.0
    1    3.0
    2    5.0
    3    NaN
    4    6.0
    5    8.0
    dtype: float64




```python
s2.index.name = '索引'
s2
```




    索引
    a    1.0
    b    3.0
    c    5.0
    d    NaN
    e    6.0
    f    8.0
    dtype: float64




```python
s1.index.name = '索引'
s1
```




    索引
    0    1.0
    1    3.0
    2    5.0
    3    NaN
    4    6.0
    5    8.0
    dtype: float64




```python
s3 = pd.Series([1,2.5,3,3.9,4,4.6,5])
s3
```




    0    1.0
    1    2.5
    2    3.0
    3    3.9
    4    4.0
    5    4.6
    6    5.0
    dtype: float64




```python
s3.index = list('abcdefg')
s3
```




    a    1.0
    b    2.5
    c    3.0
    d    3.9
    e    4.0
    f    4.6
    g    5.0
    dtype: float64



## 注意： **非默认索引的Series数据进行切片时是双闭区间，而不是左闭右开（如下）


```python
s3['a':'c']
```




    a    1.0
    b    2.5
    c    3.0
    dtype: float64




```python
s3[0:3]
```




    a    1.0
    b    2.5
    c    3.0
    dtype: float64



# 1.3 Pandas库的DataFrame类型

### 1.3.1 DataFrame是个二维结构，这里首先构造一组时间序列，作为第一维的下标：


```python
date = pd.date_range('20180101',periods=6)
#data = pd.data_range('时间起点',periods=时间个数)
print(date)
```

    DatetimeIndex(['2018-01-01', '2018-01-02', '2018-01-03', '2018-01-04',
                   '2018-01-05', '2018-01-06'],
                  dtype='datetime64[ns]', freq='D')
    

### 1.3.2 然后创建一个DataFrame的结构：


```python
df = pd.DataFrame(np.random.randn(6,4))
#  df = pd.DataFrame(二维数组)
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.492267</td>
      <td>0.632658</td>
      <td>1.013323</td>
      <td>-1.045695</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.536520</td>
      <td>1.152260</td>
      <td>0.665290</td>
      <td>2.167152</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.363372</td>
      <td>1.568730</td>
      <td>-0.725366</td>
      <td>-0.911244</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.654414</td>
      <td>0.008248</td>
      <td>-0.286533</td>
      <td>0.539505</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-1.178671</td>
      <td>-0.269790</td>
      <td>0.133095</td>
      <td>0.089573</td>
    </tr>
    <tr>
      <th>5</th>
      <td>-0.024761</td>
      <td>-1.254991</td>
      <td>0.078256</td>
      <td>-0.376459</td>
    </tr>
  </tbody>
</table>
</div>



### 1.3.3 DataFrame结构如果不指定index和columns的话，行和列的索引都是从0开始的


```python
df = pd.DataFrame(np.random.randn(6,4),index=date,columns=list('ABCD'))
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-01-01</th>
      <td>0.510127</td>
      <td>1.387267</td>
      <td>-1.447808</td>
      <td>0.778595</td>
    </tr>
    <tr>
      <th>2018-01-02</th>
      <td>1.608911</td>
      <td>-2.330537</td>
      <td>0.583199</td>
      <td>-0.045780</td>
    </tr>
    <tr>
      <th>2018-01-03</th>
      <td>-0.598623</td>
      <td>-0.473693</td>
      <td>0.114480</td>
      <td>0.158898</td>
    </tr>
    <tr>
      <th>2018-01-04</th>
      <td>-2.057511</td>
      <td>2.650395</td>
      <td>-1.502864</td>
      <td>1.057791</td>
    </tr>
    <tr>
      <th>2018-01-05</th>
      <td>0.637374</td>
      <td>-0.742565</td>
      <td>0.089562</td>
      <td>0.316206</td>
    </tr>
    <tr>
      <th>2018-01-06</th>
      <td>0.440903</td>
      <td>1.982713</td>
      <td>0.195229</td>
      <td>0.419910</td>
    </tr>
  </tbody>
</table>
</div>



### 1.3.4 除了向DataFrame传入二维数组，也可以使用字典传入数据


```python
df2 = pd.DataFrame({'A':1.,'B':pd.Timestamp('20181001'),'C':pd.Series(1,index=list(range(4)),dtype=float),'D':np.array([3]*4,dtype=int),'E':pd.Categorical(['test','train','test','train']),'F':'abc'},index=list('abcd'))
df2
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
      <th>F</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>1.0</td>
      <td>2018-10-01</td>
      <td>NaN</td>
      <td>3</td>
      <td>test</td>
      <td>abc</td>
    </tr>
    <tr>
      <th>b</th>
      <td>1.0</td>
      <td>2018-10-01</td>
      <td>NaN</td>
      <td>3</td>
      <td>train</td>
      <td>abc</td>
    </tr>
    <tr>
      <th>c</th>
      <td>1.0</td>
      <td>2018-10-01</td>
      <td>NaN</td>
      <td>3</td>
      <td>test</td>
      <td>abc</td>
    </tr>
    <tr>
      <th>d</th>
      <td>1.0</td>
      <td>2018-10-01</td>
      <td>NaN</td>
      <td>3</td>
      <td>train</td>
      <td>abc</td>
    </tr>
  </tbody>
</table>
</div>



### 1.3.5 字典的每个key代表一列，其value可以是各种能够转化为Series的对象

### 与Series所要求的类型都一致不同，DataFrame只要求每一列数据的格式相同

### 1.3.6 查看数据

### 头尾数据

####  head和tail方法可以分别查看最前面几行和最后面几行的数据（默认为5）


```python
df.head(3)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-01-01</th>
      <td>0.510127</td>
      <td>1.387267</td>
      <td>-1.447808</td>
      <td>0.778595</td>
    </tr>
    <tr>
      <th>2018-01-02</th>
      <td>1.608911</td>
      <td>-2.330537</td>
      <td>0.583199</td>
      <td>-0.045780</td>
    </tr>
    <tr>
      <th>2018-01-03</th>
      <td>-0.598623</td>
      <td>-0.473693</td>
      <td>0.114480</td>
      <td>0.158898</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.tail()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-01-02</th>
      <td>1.608911</td>
      <td>-2.330537</td>
      <td>0.583199</td>
      <td>-0.045780</td>
    </tr>
    <tr>
      <th>2018-01-03</th>
      <td>-0.598623</td>
      <td>-0.473693</td>
      <td>0.114480</td>
      <td>0.158898</td>
    </tr>
    <tr>
      <th>2018-01-04</th>
      <td>-2.057511</td>
      <td>2.650395</td>
      <td>-1.502864</td>
      <td>1.057791</td>
    </tr>
    <tr>
      <th>2018-01-05</th>
      <td>0.637374</td>
      <td>-0.742565</td>
      <td>0.089562</td>
      <td>0.316206</td>
    </tr>
    <tr>
      <th>2018-01-06</th>
      <td>0.440903</td>
      <td>1.982713</td>
      <td>0.195229</td>
      <td>0.419910</td>
    </tr>
  </tbody>
</table>
</div>



### 1.3.7 查看数据列的类型


```python
df2.dtypes
```




    A           float64
    B    datetime64[ns]
    C           float64
    D             int32
    E          category
    F            object
    dtype: object



### 1.3.8 下标，列标，数据

#### 下标使用index属性查看：


```python
df.index
```




    DatetimeIndex(['2018-01-01', '2018-01-02', '2018-01-03', '2018-01-04',
                   '2018-01-05', '2018-01-06'],
                  dtype='datetime64[ns]', freq='D')



#### 列标使用columns属性查看：


```python
df.columns
```




    Index(['A', 'B', 'C', 'D'], dtype='object')



#### 数据值使用values属性查看：


```python
df.values
```




    array([[ 0.51012685,  1.38726664, -1.44780784,  0.7785948 ],
           [ 1.6089106 , -2.33053672,  0.58319861, -0.04578028],
           [-0.59862302, -0.47369279,  0.11447977,  0.15889816],
           [-2.05751119,  2.65039477, -1.50286415,  1.05779093],
           [ 0.63737413, -0.74256466,  0.08956246,  0.31620579],
           [ 0.44090264,  1.98271337,  0.19522882,  0.41990999]])



## 1.4 pandas读取数据及数据操作

### 以豆瓣的电影数据作为深入了解pandas的示例：


```python
df = pd.read_excel(r'C:\Users\lelove\Desktop\data\作业3\豆瓣电影数据.xlsx',index_col=0)
#  这里如果不加index_col=0的话那么会出现表格中索引也变为一列——Unnamed：0
#  如果数据文件格式为csv，则使用的函数为pd.read_csv
#  输入文件路径时，反斜杠+字母可能会形成转义字符，因此在路径前加r表示不需要转义
```


```python
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>名字</th>
      <th>投票人数</th>
      <th>类型</th>
      <th>产地</th>
      <th>上映时间</th>
      <th>时长</th>
      <th>年代</th>
      <th>评分</th>
      <th>首映地点</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>肖申克的救赎</td>
      <td>692795.0</td>
      <td>剧情/犯罪</td>
      <td>美国</td>
      <td>1994-09-10 00:00:00</td>
      <td>142</td>
      <td>1994</td>
      <td>9.6</td>
      <td>多伦多电影节</td>
    </tr>
    <tr>
      <th>1</th>
      <td>控方证人</td>
      <td>42995.0</td>
      <td>剧情/悬疑/犯罪</td>
      <td>美国</td>
      <td>1957-12-17 00:00:00</td>
      <td>116</td>
      <td>1957</td>
      <td>9.5</td>
      <td>美国</td>
    </tr>
    <tr>
      <th>2</th>
      <td>美丽人生</td>
      <td>327855.0</td>
      <td>剧情/喜剧/爱情</td>
      <td>意大利</td>
      <td>1997-12-20 00:00:00</td>
      <td>116</td>
      <td>1997</td>
      <td>9.5</td>
      <td>意大利</td>
    </tr>
    <tr>
      <th>3</th>
      <td>阿甘正传</td>
      <td>580897.0</td>
      <td>剧情/爱情</td>
      <td>美国</td>
      <td>1994-06-23 00:00:00</td>
      <td>142</td>
      <td>1994</td>
      <td>9.4</td>
      <td>洛杉矶首映</td>
    </tr>
    <tr>
      <th>4</th>
      <td>霸王别姬</td>
      <td>478523.0</td>
      <td>剧情/爱情/同性</td>
      <td>中国大陆</td>
      <td>1993-01-01 00:00:00</td>
      <td>171</td>
      <td>1993</td>
      <td>9.4</td>
      <td>香港</td>
    </tr>
  </tbody>
</table>
</div>



### 1.4.1 行操作

#### 1.4.1.1主要用iloc（浏览指定行的信息）


```python
df.iloc[0]
```




    名字                   肖申克的救赎
    投票人数                 692795
    类型                    剧情/犯罪
    产地                       美国
    上映时间    1994-09-10 00:00:00
    时长                      142
    年代                     1994
    评分                      9.6
    首映地点                 多伦多电影节
    Name: 0, dtype: object




```python
df.iloc[0:5]
#  左闭右开
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>名字</th>
      <th>投票人数</th>
      <th>类型</th>
      <th>产地</th>
      <th>上映时间</th>
      <th>时长</th>
      <th>年代</th>
      <th>评分</th>
      <th>首映地点</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>肖申克的救赎</td>
      <td>692795.0</td>
      <td>剧情/犯罪</td>
      <td>美国</td>
      <td>1994-09-10 00:00:00</td>
      <td>142</td>
      <td>1994</td>
      <td>9.6</td>
      <td>多伦多电影节</td>
    </tr>
    <tr>
      <th>1</th>
      <td>控方证人</td>
      <td>42995.0</td>
      <td>剧情/悬疑/犯罪</td>
      <td>美国</td>
      <td>1957-12-17 00:00:00</td>
      <td>116</td>
      <td>1957</td>
      <td>9.5</td>
      <td>美国</td>
    </tr>
    <tr>
      <th>2</th>
      <td>美丽人生</td>
      <td>327855.0</td>
      <td>剧情/喜剧/爱情</td>
      <td>意大利</td>
      <td>1997-12-20 00:00:00</td>
      <td>116</td>
      <td>1997</td>
      <td>9.5</td>
      <td>意大利</td>
    </tr>
    <tr>
      <th>3</th>
      <td>阿甘正传</td>
      <td>580897.0</td>
      <td>剧情/爱情</td>
      <td>美国</td>
      <td>1994-06-23 00:00:00</td>
      <td>142</td>
      <td>1994</td>
      <td>9.4</td>
      <td>洛杉矶首映</td>
    </tr>
    <tr>
      <th>4</th>
      <td>霸王别姬</td>
      <td>478523.0</td>
      <td>剧情/爱情/同性</td>
      <td>中国大陆</td>
      <td>1993-01-01 00:00:00</td>
      <td>171</td>
      <td>1993</td>
      <td>9.4</td>
      <td>香港</td>
    </tr>
  </tbody>
</table>
</div>



#### 1.4.1.2 也可以使用loc


```python
df.loc[0:5]
#  双闭区间
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>名字</th>
      <th>投票人数</th>
      <th>类型</th>
      <th>产地</th>
      <th>上映时间</th>
      <th>时长</th>
      <th>年代</th>
      <th>评分</th>
      <th>首映地点</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>肖申克的救赎</td>
      <td>692795.0</td>
      <td>剧情/犯罪</td>
      <td>美国</td>
      <td>1994-09-10 00:00:00</td>
      <td>142</td>
      <td>1994</td>
      <td>9.6</td>
      <td>多伦多电影节</td>
    </tr>
    <tr>
      <th>1</th>
      <td>控方证人</td>
      <td>42995.0</td>
      <td>剧情/悬疑/犯罪</td>
      <td>美国</td>
      <td>1957-12-17 00:00:00</td>
      <td>116</td>
      <td>1957</td>
      <td>9.5</td>
      <td>美国</td>
    </tr>
    <tr>
      <th>2</th>
      <td>美丽人生</td>
      <td>327855.0</td>
      <td>剧情/喜剧/爱情</td>
      <td>意大利</td>
      <td>1997-12-20 00:00:00</td>
      <td>116</td>
      <td>1997</td>
      <td>9.5</td>
      <td>意大利</td>
    </tr>
    <tr>
      <th>3</th>
      <td>阿甘正传</td>
      <td>580897.0</td>
      <td>剧情/爱情</td>
      <td>美国</td>
      <td>1994-06-23 00:00:00</td>
      <td>142</td>
      <td>1994</td>
      <td>9.4</td>
      <td>洛杉矶首映</td>
    </tr>
    <tr>
      <th>4</th>
      <td>霸王别姬</td>
      <td>478523.0</td>
      <td>剧情/爱情/同性</td>
      <td>中国大陆</td>
      <td>1993-01-01 00:00:00</td>
      <td>171</td>
      <td>1993</td>
      <td>9.4</td>
      <td>香港</td>
    </tr>
    <tr>
      <th>5</th>
      <td>泰坦尼克号</td>
      <td>157074.0</td>
      <td>剧情/爱情/灾难</td>
      <td>美国</td>
      <td>2012-04-10 00:00:00</td>
      <td>194</td>
      <td>2012</td>
      <td>9.4</td>
      <td>中国大陆</td>
    </tr>
  </tbody>
</table>
</div>



#### 1.4.1.3 添加一行append


```python
dit = {'名字':'复仇者联盟3','投票人数':123456,'类型':'剧情/科幻','上映时间':'2018-05-04 00:00:00','时长':142,'年代':2018,'评分':np.nan,'首映地点':'美国'}
s = pd.Series(dit)
s.name = 38738
```


```python
s
```




    名字                   复仇者联盟3
    投票人数                 123456
    类型                    剧情/科幻
    上映时间    2018-05-04 00:00:00
    时长                      142
    年代                     2018
    评分                      8.7
    首映地点                     美国
    Name: 38738, dtype: object




```python
df = df.append(s)
df[-5:]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>名字</th>
      <th>投票人数</th>
      <th>类型</th>
      <th>产地</th>
      <th>上映时间</th>
      <th>时长</th>
      <th>年代</th>
      <th>评分</th>
      <th>首映地点</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>38734</th>
      <td>1935年</td>
      <td>57.0</td>
      <td>喜剧/歌舞</td>
      <td>美国</td>
      <td>1935-03-15 00:00:00</td>
      <td>98</td>
      <td>1935</td>
      <td>7.6</td>
      <td>美国</td>
    </tr>
    <tr>
      <th>38735</th>
      <td>血溅画屏</td>
      <td>95.0</td>
      <td>剧情/悬疑/犯罪/武侠/古装</td>
      <td>中国大陆</td>
      <td>1905-06-08 00:00:00</td>
      <td>91</td>
      <td>1986</td>
      <td>7.1</td>
      <td>美国</td>
    </tr>
    <tr>
      <th>38736</th>
      <td>魔窟中的幻想</td>
      <td>51.0</td>
      <td>惊悚/恐怖/儿童</td>
      <td>中国大陆</td>
      <td>1905-06-08 00:00:00</td>
      <td>78</td>
      <td>1986</td>
      <td>8.0</td>
      <td>美国</td>
    </tr>
    <tr>
      <th>38737</th>
      <td>列宁格勒围困之星火战役 Блокада: Фильм 2: Ленинградский ме...</td>
      <td>32.0</td>
      <td>剧情/战争</td>
      <td>苏联</td>
      <td>1905-05-30 00:00:00</td>
      <td>97</td>
      <td>1977</td>
      <td>6.6</td>
      <td>美国</td>
    </tr>
    <tr>
      <th>38738</th>
      <td>复仇者联盟3</td>
      <td>123456.0</td>
      <td>剧情/科幻</td>
      <td>NaN</td>
      <td>2018-05-04 00:00:00</td>
      <td>142</td>
      <td>2018</td>
      <td>NaN</td>
      <td>美国</td>
    </tr>
  </tbody>
</table>
</div>



#### 1.4.1.4 删除一行drop


```python
df = df.drop([38738])
df[-5:]
```


    ---------------------------------------------------------------------------

    KeyError                                  Traceback (most recent call last)

    <ipython-input-102-1dadc80316c1> in <module>
    ----> 1 df = df.drop([38738])
          2 df[-5:]
    

    E:\Anaconda\lib\site-packages\pandas\core\frame.py in drop(self, labels, axis, index, columns, level, inplace, errors)
       3938                                            index=index, columns=columns,
       3939                                            level=level, inplace=inplace,
    -> 3940                                            errors=errors)
       3941 
       3942     @rewrite_axis_style_signature('mapper', [('copy', True),
    

    E:\Anaconda\lib\site-packages\pandas\core\generic.py in drop(self, labels, axis, index, columns, level, inplace, errors)
       3778         for axis, labels in axes.items():
       3779             if labels is not None:
    -> 3780                 obj = obj._drop_axis(labels, axis, level=level, errors=errors)
       3781 
       3782         if inplace:
    

    E:\Anaconda\lib\site-packages\pandas\core\generic.py in _drop_axis(self, labels, axis, level, errors)
       3810                 new_axis = axis.drop(labels, level=level, errors=errors)
       3811             else:
    -> 3812                 new_axis = axis.drop(labels, errors=errors)
       3813             result = self.reindex(**{axis_name: new_axis})
       3814 
    

    E:\Anaconda\lib\site-packages\pandas\core\indexes\base.py in drop(self, labels, errors)
       4963             if errors != 'ignore':
       4964                 raise KeyError(
    -> 4965                     '{} not found in axis'.format(labels[mask]))
       4966             indexer = indexer[~mask]
       4967         return self.delete(indexer)
    

    KeyError: '[38738] not found in axis'


### 1.4.2 列操作


```python
df.columns
```




    Index(['名字', '投票人数', '类型', '产地', '上映时间', '时长', '年代', '评分', '首映地点'], dtype='object')




```python
df['名字'][:5]
```




    0    肖申克的救赎
    1      控方证人
    2     美丽人生 
    3      阿甘正传
    4      霸王别姬
    Name: 名字, dtype: object




```python
df['名字'][5]
```




    '泰坦尼克号 '



### 取其中多列


```python
df[['名字','类型']][1:5]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>名字</th>
      <th>类型</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>控方证人</td>
      <td>剧情/悬疑/犯罪</td>
    </tr>
    <tr>
      <th>2</th>
      <td>美丽人生</td>
      <td>剧情/喜剧/爱情</td>
    </tr>
    <tr>
      <th>3</th>
      <td>阿甘正传</td>
      <td>剧情/爱情</td>
    </tr>
    <tr>
      <th>4</th>
      <td>霸王别姬</td>
      <td>剧情/爱情/同性</td>
    </tr>
  </tbody>
</table>
</div>



#### 1.4.2.1 增加一列


```python
df['序号'] = range(1,len(df)+1)
df[:5]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>名字</th>
      <th>投票人数</th>
      <th>类型</th>
      <th>产地</th>
      <th>上映时间</th>
      <th>时长</th>
      <th>年代</th>
      <th>评分</th>
      <th>首映地点</th>
      <th>序号</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>肖申克的救赎</td>
      <td>692795.0</td>
      <td>剧情/犯罪</td>
      <td>美国</td>
      <td>1994-09-10 00:00:00</td>
      <td>142</td>
      <td>1994</td>
      <td>9.6</td>
      <td>多伦多电影节</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>控方证人</td>
      <td>42995.0</td>
      <td>剧情/悬疑/犯罪</td>
      <td>美国</td>
      <td>1957-12-17 00:00:00</td>
      <td>116</td>
      <td>1957</td>
      <td>9.5</td>
      <td>美国</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>美丽人生</td>
      <td>327855.0</td>
      <td>剧情/喜剧/爱情</td>
      <td>意大利</td>
      <td>1997-12-20 00:00:00</td>
      <td>116</td>
      <td>1997</td>
      <td>9.5</td>
      <td>意大利</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>阿甘正传</td>
      <td>580897.0</td>
      <td>剧情/爱情</td>
      <td>美国</td>
      <td>1994-06-23 00:00:00</td>
      <td>142</td>
      <td>1994</td>
      <td>9.4</td>
      <td>洛杉矶首映</td>
      <td>4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>霸王别姬</td>
      <td>478523.0</td>
      <td>剧情/爱情/同性</td>
      <td>中国大陆</td>
      <td>1993-01-01 00:00:00</td>
      <td>171</td>
      <td>1993</td>
      <td>9.4</td>
      <td>香港</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>



#### 1.4.2.2 删除一列


```python
df = df.drop('序号',axis=1)
df[:5]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>名字</th>
      <th>投票人数</th>
      <th>类型</th>
      <th>产地</th>
      <th>上映时间</th>
      <th>时长</th>
      <th>年代</th>
      <th>评分</th>
      <th>首映地点</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>肖申克的救赎</td>
      <td>692795.0</td>
      <td>剧情/犯罪</td>
      <td>美国</td>
      <td>1994-09-10 00:00:00</td>
      <td>142</td>
      <td>1994</td>
      <td>9.6</td>
      <td>多伦多电影节</td>
    </tr>
    <tr>
      <th>1</th>
      <td>控方证人</td>
      <td>42995.0</td>
      <td>剧情/悬疑/犯罪</td>
      <td>美国</td>
      <td>1957-12-17 00:00:00</td>
      <td>116</td>
      <td>1957</td>
      <td>9.5</td>
      <td>美国</td>
    </tr>
    <tr>
      <th>2</th>
      <td>美丽人生</td>
      <td>327855.0</td>
      <td>剧情/喜剧/爱情</td>
      <td>意大利</td>
      <td>1997-12-20 00:00:00</td>
      <td>116</td>
      <td>1997</td>
      <td>9.5</td>
      <td>意大利</td>
    </tr>
    <tr>
      <th>3</th>
      <td>阿甘正传</td>
      <td>580897.0</td>
      <td>剧情/爱情</td>
      <td>美国</td>
      <td>1994-06-23 00:00:00</td>
      <td>142</td>
      <td>1994</td>
      <td>9.4</td>
      <td>洛杉矶首映</td>
    </tr>
    <tr>
      <th>4</th>
      <td>霸王别姬</td>
      <td>478523.0</td>
      <td>剧情/爱情/同性</td>
      <td>中国大陆</td>
      <td>1993-01-01 00:00:00</td>
      <td>171</td>
      <td>1993</td>
      <td>9.4</td>
      <td>香港</td>
    </tr>
  </tbody>
</table>
</div>



#### 1.4.2.3 通过标签选择数据

##### df.loc[[index].[column]]


```python
df.loc[1,'名字'] #  取一行一列
```




    '控方证人'




```python
df.loc[[1,3,5,7,9],['名字','评分']]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>名字</th>
      <th>评分</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>控方证人</td>
      <td>9.5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>阿甘正传</td>
      <td>9.4</td>
    </tr>
    <tr>
      <th>5</th>
      <td>泰坦尼克号</td>
      <td>9.4</td>
    </tr>
    <tr>
      <th>7</th>
      <td>新世纪福音战士剧场版：Air/真心为你 新世紀エヴァンゲリオン劇場版 Ai</td>
      <td>9.4</td>
    </tr>
    <tr>
      <th>9</th>
      <td>这个杀手不太冷</td>
      <td>9.4</td>
    </tr>
  </tbody>
</table>
</div>



### 1.5 条件选择

#### 1.5.1 选取产地为美国的所有电影


```python
df['产地'] == '美国'
```




    0         True
    1         True
    2        False
    3         True
    4        False
    5         True
    6         True
    7        False
    8        False
    9        False
    10       False
    11        True
    12       False
    13        True
    14       False
    15        True
    16        True
    17        True
    18       False
    19        True
    20        True
    21       False
    22        True
    23       False
    24       False
    25       False
    26        True
    27        True
    28       False
    29       False
             ...  
    38709    False
    38710    False
    38711     True
    38712    False
    38713     True
    38714    False
    38715    False
    38716    False
    38717    False
    38718    False
    38719     True
    38720    False
    38721    False
    38722     True
    38723     True
    38724     True
    38725    False
    38726     True
    38727    False
    38728     True
    38729    False
    38730    False
    38731    False
    38732     True
    38733    False
    38734     True
    38735    False
    38736    False
    38737    False
    38738    False
    Name: 产地, Length: 38739, dtype: bool




```python
df[df['产地']=='美国'][:5]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>名字</th>
      <th>投票人数</th>
      <th>类型</th>
      <th>产地</th>
      <th>上映时间</th>
      <th>时长</th>
      <th>年代</th>
      <th>评分</th>
      <th>首映地点</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>肖申克的救赎</td>
      <td>692795.0</td>
      <td>剧情/犯罪</td>
      <td>美国</td>
      <td>1994-09-10 00:00:00</td>
      <td>142</td>
      <td>1994</td>
      <td>9.6</td>
      <td>多伦多电影节</td>
    </tr>
    <tr>
      <th>1</th>
      <td>控方证人</td>
      <td>42995.0</td>
      <td>剧情/悬疑/犯罪</td>
      <td>美国</td>
      <td>1957-12-17 00:00:00</td>
      <td>116</td>
      <td>1957</td>
      <td>9.5</td>
      <td>美国</td>
    </tr>
    <tr>
      <th>3</th>
      <td>阿甘正传</td>
      <td>580897.0</td>
      <td>剧情/爱情</td>
      <td>美国</td>
      <td>1994-06-23 00:00:00</td>
      <td>142</td>
      <td>1994</td>
      <td>9.4</td>
      <td>洛杉矶首映</td>
    </tr>
    <tr>
      <th>5</th>
      <td>泰坦尼克号</td>
      <td>157074.0</td>
      <td>剧情/爱情/灾难</td>
      <td>美国</td>
      <td>2012-04-10 00:00:00</td>
      <td>194</td>
      <td>2012</td>
      <td>9.4</td>
      <td>中国大陆</td>
    </tr>
    <tr>
      <th>6</th>
      <td>辛德勒的名单</td>
      <td>306904.0</td>
      <td>剧情/历史/战争</td>
      <td>美国</td>
      <td>1993-11-30 00:00:00</td>
      <td>195</td>
      <td>1993</td>
      <td>9.4</td>
      <td>华盛顿首映</td>
    </tr>
  </tbody>
</table>
</div>



#### 1.5.2 选取产地为美国的电影，且评分大于9分


```python
df[(df['产地'] == '美国')&(df['评分']>9)][:5]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>名字</th>
      <th>投票人数</th>
      <th>类型</th>
      <th>产地</th>
      <th>上映时间</th>
      <th>时长</th>
      <th>年代</th>
      <th>评分</th>
      <th>首映地点</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>肖申克的救赎</td>
      <td>692795.0</td>
      <td>剧情/犯罪</td>
      <td>美国</td>
      <td>1994-09-10 00:00:00</td>
      <td>142</td>
      <td>1994</td>
      <td>9.6</td>
      <td>多伦多电影节</td>
    </tr>
    <tr>
      <th>1</th>
      <td>控方证人</td>
      <td>42995.0</td>
      <td>剧情/悬疑/犯罪</td>
      <td>美国</td>
      <td>1957-12-17 00:00:00</td>
      <td>116</td>
      <td>1957</td>
      <td>9.5</td>
      <td>美国</td>
    </tr>
    <tr>
      <th>3</th>
      <td>阿甘正传</td>
      <td>580897.0</td>
      <td>剧情/爱情</td>
      <td>美国</td>
      <td>1994-06-23 00:00:00</td>
      <td>142</td>
      <td>1994</td>
      <td>9.4</td>
      <td>洛杉矶首映</td>
    </tr>
    <tr>
      <th>5</th>
      <td>泰坦尼克号</td>
      <td>157074.0</td>
      <td>剧情/爱情/灾难</td>
      <td>美国</td>
      <td>2012-04-10 00:00:00</td>
      <td>194</td>
      <td>2012</td>
      <td>9.4</td>
      <td>中国大陆</td>
    </tr>
    <tr>
      <th>6</th>
      <td>辛德勒的名单</td>
      <td>306904.0</td>
      <td>剧情/历史/战争</td>
      <td>美国</td>
      <td>1993-11-30 00:00:00</td>
      <td>195</td>
      <td>1993</td>
      <td>9.4</td>
      <td>华盛顿首映</td>
    </tr>
  </tbody>
</table>
</div>




```python
df[(df.产地=='美国')&(df.评分>9)][:5] #  效果同上
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>名字</th>
      <th>投票人数</th>
      <th>类型</th>
      <th>产地</th>
      <th>上映时间</th>
      <th>时长</th>
      <th>年代</th>
      <th>评分</th>
      <th>首映地点</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>肖申克的救赎</td>
      <td>692795.0</td>
      <td>剧情/犯罪</td>
      <td>美国</td>
      <td>1994-09-10 00:00:00</td>
      <td>142</td>
      <td>1994</td>
      <td>9.6</td>
      <td>多伦多电影节</td>
    </tr>
    <tr>
      <th>1</th>
      <td>控方证人</td>
      <td>42995.0</td>
      <td>剧情/悬疑/犯罪</td>
      <td>美国</td>
      <td>1957-12-17 00:00:00</td>
      <td>116</td>
      <td>1957</td>
      <td>9.5</td>
      <td>美国</td>
    </tr>
    <tr>
      <th>3</th>
      <td>阿甘正传</td>
      <td>580897.0</td>
      <td>剧情/爱情</td>
      <td>美国</td>
      <td>1994-06-23 00:00:00</td>
      <td>142</td>
      <td>1994</td>
      <td>9.4</td>
      <td>洛杉矶首映</td>
    </tr>
    <tr>
      <th>5</th>
      <td>泰坦尼克号</td>
      <td>157074.0</td>
      <td>剧情/爱情/灾难</td>
      <td>美国</td>
      <td>2012-04-10 00:00:00</td>
      <td>194</td>
      <td>2012</td>
      <td>9.4</td>
      <td>中国大陆</td>
    </tr>
    <tr>
      <th>6</th>
      <td>辛德勒的名单</td>
      <td>306904.0</td>
      <td>剧情/历史/战争</td>
      <td>美国</td>
      <td>1993-11-30 00:00:00</td>
      <td>195</td>
      <td>1993</td>
      <td>9.4</td>
      <td>华盛顿首映</td>
    </tr>
  </tbody>
</table>
</div>



#### 1.5.3 选取产地为美国或中国大陆的电影，并且评分大于9


```python
df[((df.产地=='美国')|(df.产地=='中国大陆'))&(df.评分>9)][:10]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>名字</th>
      <th>投票人数</th>
      <th>类型</th>
      <th>产地</th>
      <th>上映时间</th>
      <th>时长</th>
      <th>年代</th>
      <th>评分</th>
      <th>首映地点</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>肖申克的救赎</td>
      <td>692795.0</td>
      <td>剧情/犯罪</td>
      <td>美国</td>
      <td>1994-09-10 00:00:00</td>
      <td>142</td>
      <td>1994</td>
      <td>9.6</td>
      <td>多伦多电影节</td>
    </tr>
    <tr>
      <th>1</th>
      <td>控方证人</td>
      <td>42995.0</td>
      <td>剧情/悬疑/犯罪</td>
      <td>美国</td>
      <td>1957-12-17 00:00:00</td>
      <td>116</td>
      <td>1957</td>
      <td>9.5</td>
      <td>美国</td>
    </tr>
    <tr>
      <th>3</th>
      <td>阿甘正传</td>
      <td>580897.0</td>
      <td>剧情/爱情</td>
      <td>美国</td>
      <td>1994-06-23 00:00:00</td>
      <td>142</td>
      <td>1994</td>
      <td>9.4</td>
      <td>洛杉矶首映</td>
    </tr>
    <tr>
      <th>4</th>
      <td>霸王别姬</td>
      <td>478523.0</td>
      <td>剧情/爱情/同性</td>
      <td>中国大陆</td>
      <td>1993-01-01 00:00:00</td>
      <td>171</td>
      <td>1993</td>
      <td>9.4</td>
      <td>香港</td>
    </tr>
    <tr>
      <th>5</th>
      <td>泰坦尼克号</td>
      <td>157074.0</td>
      <td>剧情/爱情/灾难</td>
      <td>美国</td>
      <td>2012-04-10 00:00:00</td>
      <td>194</td>
      <td>2012</td>
      <td>9.4</td>
      <td>中国大陆</td>
    </tr>
    <tr>
      <th>6</th>
      <td>辛德勒的名单</td>
      <td>306904.0</td>
      <td>剧情/历史/战争</td>
      <td>美国</td>
      <td>1993-11-30 00:00:00</td>
      <td>195</td>
      <td>1993</td>
      <td>9.4</td>
      <td>华盛顿首映</td>
    </tr>
    <tr>
      <th>11</th>
      <td>疯狂动物城</td>
      <td>284652.0</td>
      <td>喜剧/动作/动画/冒险</td>
      <td>美国</td>
      <td>2016-03-04 00:00:00</td>
      <td>109</td>
      <td>2016</td>
      <td>9.3</td>
      <td>中国大陆/美国</td>
    </tr>
    <tr>
      <th>13</th>
      <td>海豚湾</td>
      <td>159302.0</td>
      <td>纪录片</td>
      <td>美国</td>
      <td>2009-07-31 00:00:00</td>
      <td>92</td>
      <td>2009</td>
      <td>9.3</td>
      <td>美国</td>
    </tr>
    <tr>
      <th>15</th>
      <td>机器人总动员</td>
      <td>421734.0</td>
      <td>喜剧/爱情/科幻/动画/冒险</td>
      <td>美国</td>
      <td>2008-06-27 00:00:00</td>
      <td>98</td>
      <td>2008</td>
      <td>9.3</td>
      <td>美国</td>
    </tr>
    <tr>
      <th>16</th>
      <td>十二怒汉</td>
      <td>134949.0</td>
      <td>剧情</td>
      <td>美国</td>
      <td>1957-04-01 00:00:00</td>
      <td>96</td>
      <td>1957</td>
      <td>9.3</td>
      <td>美国</td>
    </tr>
  </tbody>
</table>
</div>



### 1.6 缺失值及异常值处理（数据清理常用）


```python
df1 = pd.read_excel(r'C:\Users\lelove\Desktop\data\补充\缺失值处理方法.xlsx')
df1
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>方法</th>
      <th>说明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>dropna</td>
      <td>根据标签中的缺失值进行过滤，删除缺失值</td>
    </tr>
    <tr>
      <th>1</th>
      <td>fillna</td>
      <td>对缺失值进行填充</td>
    </tr>
    <tr>
      <th>2</th>
      <td>isnull</td>
      <td>返回一个布尔值对象，判断哪些值是缺失值</td>
    </tr>
    <tr>
      <th>3</th>
      <td>notnull</td>
      <td>isnull的否定式</td>
    </tr>
  </tbody>
</table>
</div>



#### 1.6.1 判断缺失值


```python
df.isnull()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>名字</th>
      <th>投票人数</th>
      <th>类型</th>
      <th>产地</th>
      <th>上映时间</th>
      <th>时长</th>
      <th>年代</th>
      <th>评分</th>
      <th>首映地点</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>5</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>6</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>7</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>8</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>9</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>10</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>11</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>12</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>13</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>14</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>15</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>16</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>17</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>18</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>19</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>20</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>21</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>22</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>23</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>24</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>25</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>26</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>27</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>28</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>29</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>38709</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>38710</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>38711</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>38712</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>38713</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>38714</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>38715</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>38716</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>38717</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>38718</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>38719</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>38720</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>38721</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>38722</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>38723</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>38724</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>38725</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>38726</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>38727</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>38728</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>38729</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>38730</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>38731</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>38732</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>38733</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>38734</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>38735</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>38736</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>38737</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>38738</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
<p>38739 rows × 9 columns</p>
</div>




```python
df[df['名字'].isnull()][:10]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>名字</th>
      <th>投票人数</th>
      <th>类型</th>
      <th>产地</th>
      <th>上映时间</th>
      <th>时长</th>
      <th>年代</th>
      <th>评分</th>
      <th>首映地点</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>231</th>
      <td>NaN</td>
      <td>144.0</td>
      <td>纪录片/音乐</td>
      <td>韩国</td>
      <td>2011-02-02 00:00:00</td>
      <td>90</td>
      <td>2011</td>
      <td>9.7</td>
      <td>美国</td>
    </tr>
    <tr>
      <th>361</th>
      <td>NaN</td>
      <td>80.0</td>
      <td>短片</td>
      <td>其他</td>
      <td>1905-05-17 00:00:00</td>
      <td>4</td>
      <td>1964</td>
      <td>5.7</td>
      <td>美国</td>
    </tr>
    <tr>
      <th>369</th>
      <td>NaN</td>
      <td>5315.0</td>
      <td>剧情</td>
      <td>日本</td>
      <td>2004-07-10 00:00:00</td>
      <td>111</td>
      <td>2004</td>
      <td>7.5</td>
      <td>日本</td>
    </tr>
    <tr>
      <th>372</th>
      <td>NaN</td>
      <td>263.0</td>
      <td>短片/音乐</td>
      <td>英国</td>
      <td>1998-06-30 00:00:00</td>
      <td>34</td>
      <td>1998</td>
      <td>9.2</td>
      <td>美国</td>
    </tr>
    <tr>
      <th>374</th>
      <td>NaN</td>
      <td>47.0</td>
      <td>短片</td>
      <td>其他</td>
      <td>1905-05-17 00:00:00</td>
      <td>3</td>
      <td>1964</td>
      <td>6.7</td>
      <td>美国</td>
    </tr>
    <tr>
      <th>375</th>
      <td>NaN</td>
      <td>1193.0</td>
      <td>短片/音乐</td>
      <td>法国</td>
      <td>1905-07-01 00:00:00</td>
      <td>10</td>
      <td>2010</td>
      <td>7.7</td>
      <td>美国</td>
    </tr>
    <tr>
      <th>411</th>
      <td>NaN</td>
      <td>32.0</td>
      <td>短片</td>
      <td>其他</td>
      <td>1905-05-17 00:00:00</td>
      <td>3</td>
      <td>1964</td>
      <td>7.0</td>
      <td>美国</td>
    </tr>
    <tr>
      <th>432</th>
      <td>NaN</td>
      <td>1081.0</td>
      <td>剧情/动作/惊悚/犯罪</td>
      <td>美国</td>
      <td>2016-02-26 00:00:00</td>
      <td>115</td>
      <td>2016</td>
      <td>6.0</td>
      <td>美国</td>
    </tr>
    <tr>
      <th>441</th>
      <td>NaN</td>
      <td>213.0</td>
      <td>恐怖</td>
      <td>美国</td>
      <td>2007-03-06 00:00:00</td>
      <td>83</td>
      <td>2007</td>
      <td>3.2</td>
      <td>美国</td>
    </tr>
    <tr>
      <th>448</th>
      <td>NaN</td>
      <td>110.0</td>
      <td>纪录片</td>
      <td>荷兰</td>
      <td>2002-04-19 00:00:00</td>
      <td>48</td>
      <td>2000</td>
      <td>9.3</td>
      <td>美国</td>
    </tr>
  </tbody>
</table>
</div>



#### 1.6.2 填充缺失值


```python
df[df['投票人数'].isnull()][:10]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>名字</th>
      <th>投票人数</th>
      <th>类型</th>
      <th>产地</th>
      <th>上映时间</th>
      <th>时长</th>
      <th>年代</th>
      <th>评分</th>
      <th>首映地点</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>




```python
df[df['时长'].isnull()][:10]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>名字</th>
      <th>投票人数</th>
      <th>类型</th>
      <th>产地</th>
      <th>上映时间</th>
      <th>时长</th>
      <th>年代</th>
      <th>评分</th>
      <th>首映地点</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>




```python
df[df['评分'].isnull()][:10]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>名字</th>
      <th>投票人数</th>
      <th>类型</th>
      <th>产地</th>
      <th>上映时间</th>
      <th>时长</th>
      <th>年代</th>
      <th>评分</th>
      <th>首映地点</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>38738</th>
      <td>复仇者联盟3</td>
      <td>123456.0</td>
      <td>剧情/科幻</td>
      <td>NaN</td>
      <td>2018-05-04 00:00:00</td>
      <td>142</td>
      <td>2018</td>
      <td>NaN</td>
      <td>美国</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['评分'].fillna(np.mean(df['评分']),inplace=True)
#  以所有评分的均值填充
df[-5:]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>名字</th>
      <th>投票人数</th>
      <th>类型</th>
      <th>产地</th>
      <th>上映时间</th>
      <th>时长</th>
      <th>年代</th>
      <th>评分</th>
      <th>首映地点</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>38734</th>
      <td>1935年</td>
      <td>57.0</td>
      <td>喜剧/歌舞</td>
      <td>美国</td>
      <td>1935-03-15 00:00:00</td>
      <td>98</td>
      <td>1935</td>
      <td>7.600000</td>
      <td>美国</td>
    </tr>
    <tr>
      <th>38735</th>
      <td>血溅画屏</td>
      <td>95.0</td>
      <td>剧情/悬疑/犯罪/武侠/古装</td>
      <td>中国大陆</td>
      <td>1905-06-08 00:00:00</td>
      <td>91</td>
      <td>1986</td>
      <td>7.100000</td>
      <td>美国</td>
    </tr>
    <tr>
      <th>38736</th>
      <td>魔窟中的幻想</td>
      <td>51.0</td>
      <td>惊悚/恐怖/儿童</td>
      <td>中国大陆</td>
      <td>1905-06-08 00:00:00</td>
      <td>78</td>
      <td>1986</td>
      <td>8.000000</td>
      <td>美国</td>
    </tr>
    <tr>
      <th>38737</th>
      <td>列宁格勒围困之星火战役 Блокада: Фильм 2: Ленинградский ме...</td>
      <td>32.0</td>
      <td>剧情/战争</td>
      <td>苏联</td>
      <td>1905-05-30 00:00:00</td>
      <td>97</td>
      <td>1977</td>
      <td>6.600000</td>
      <td>美国</td>
    </tr>
    <tr>
      <th>38738</th>
      <td>复仇者联盟3</td>
      <td>123456.0</td>
      <td>剧情/科幻</td>
      <td>NaN</td>
      <td>2018-05-04 00:00:00</td>
      <td>142</td>
      <td>2018</td>
      <td>6.935704</td>
      <td>美国</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.fillna('未知电影') #  此操作会对所有缺失值填充括号内的内容（谨慎使用，会改变原数据）
```


```python
df2 = df.fillna('未知电影') #  将所有缺失值填充‘未知电影’赋值给df2
df2[df2['名字'].isnull()] #  结果显示没有未填充数据。
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>名字</th>
      <th>投票人数</th>
      <th>类型</th>
      <th>产地</th>
      <th>上映时间</th>
      <th>时长</th>
      <th>年代</th>
      <th>评分</th>
      <th>首映地点</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>



#### 1.6.3 删除缺失值
df.dropna()参数：

how='all':删除全为空值的行或列
inplace=True:覆盖之前的数据
axis=0:选择行或列

```python
len(df)
```




    38175




```python
df2 = df.dropna()
```


```python
len(df2)
```




    38175




```python
df.dropna(inplace=True)
```

### 1.7 处理异常值
异常值，即在数据集中存在不合理的值，又称离群点。比如年龄为-1，笔记本电脑重量为1吨等，都属于异常值的范围

```python
df[df.投票人数<0]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>名字</th>
      <th>投票人数</th>
      <th>类型</th>
      <th>产地</th>
      <th>上映时间</th>
      <th>时长</th>
      <th>年代</th>
      <th>评分</th>
      <th>首映地点</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>19777</th>
      <td>皇家大贼 皇家大</td>
      <td>-80.0</td>
      <td>剧情/犯罪</td>
      <td>中国香港</td>
      <td>1985-05-31 00:00:00</td>
      <td>60</td>
      <td>1985</td>
      <td>6.3</td>
      <td>美国</td>
    </tr>
    <tr>
      <th>19786</th>
      <td>日本的垃圾去中国大陆 にっぽんの“ゴミ” 大陆へ渡る ～中国式リサイクル錬</td>
      <td>-80.0</td>
      <td>纪录片</td>
      <td>日本</td>
      <td>1905-06-26 00:00:00</td>
      <td>60</td>
      <td>2004</td>
      <td>7.9</td>
      <td>美国</td>
    </tr>
    <tr>
      <th>19797</th>
      <td>女教徒</td>
      <td>-118.0</td>
      <td>剧情</td>
      <td>法国</td>
      <td>1966-05-06 00:00:00</td>
      <td>135</td>
      <td>1966</td>
      <td>7.8</td>
      <td>美国</td>
    </tr>
  </tbody>
</table>
</div>




```python
df[df.投票人数%1!=0]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>名字</th>
      <th>投票人数</th>
      <th>类型</th>
      <th>产地</th>
      <th>上映时间</th>
      <th>时长</th>
      <th>年代</th>
      <th>评分</th>
      <th>首映地点</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>19791</th>
      <td>女教师 女教</td>
      <td>8.30</td>
      <td>剧情/犯罪</td>
      <td>日本</td>
      <td>1977-10-29 00:00:00</td>
      <td>100</td>
      <td>1977</td>
      <td>6.6</td>
      <td>日本</td>
    </tr>
    <tr>
      <th>19804</th>
      <td>女郎漫游仙境 ドレミファ娘の血は騒</td>
      <td>5.90</td>
      <td>喜剧/歌舞</td>
      <td>日本</td>
      <td>1985-11-03 00:00:00</td>
      <td>80</td>
      <td>1985</td>
      <td>6.7</td>
      <td>日本</td>
    </tr>
    <tr>
      <th>19820</th>
      <td>女仆日记</td>
      <td>12.87</td>
      <td>剧情</td>
      <td>法国</td>
      <td>2015-04-01 00:00:00</td>
      <td>96</td>
      <td>2015</td>
      <td>5.7</td>
      <td>法国</td>
    </tr>
    <tr>
      <th>38055</th>
      <td>逃出亚卡拉</td>
      <td>12.87</td>
      <td>剧情/动作/惊悚/犯罪</td>
      <td>美国</td>
      <td>1979-09-20 00:00:00</td>
      <td>112</td>
      <td>1979</td>
      <td>7.8</td>
      <td>美国</td>
    </tr>
  </tbody>
</table>
</div>




```python
df = df[df.投票人数>0]
df = df[df.投票人数%1==0]
```


```python
len(df)
```




    38168



#### 对于异常值，一般来说数量偏少，在不影响整体数据分析的情况下，直接删除即可。

#### 其他属性的异常值处理，在格式转换部分，进一步讨论。

### 1.8 数据保存

#### 数据处理之后，然后将数据重新保存到movie_data.xlsx


```python
df.to_excel('movie_data.xlsx')
```
