Pandas
===
```python
import pandas as pd
% matplotlib inline

df_census = pd.read_csv('census_income_data.csv')
df_census.info()

```
### 绘图
```python
df_census.hist() 
df_census.hist(figsize=(8,8))  #设置宽度

#Pandas 得series 对象也可以调用hist()函数
df_census['age'].hist()

#或者不用hist()函数，改用通用得plot函数,用参数指定形状
df_census['age'].plot(kind='hist')

#汇总每列每个唯一值的数量
df_census['education'].value_counts()
df_census['education'].value_counts().plot(kind='bar') #对此列统计

#每个变量的直方图
pd.plotting.scatter_matrix(df_census, figsize=(15,15));

#绘制2列的散列点图
df_census.plot(x='列1', y ='列2', kind='scatter');
```

### 基本方法
```python
import pandas as pd

df = pd.read_csv('cancer_data.csv')
df.head()

# 返回 dataframe 维度的元组
df.shape

# 返回列的数据类型
df.dtypes

# 虽然供诊断的数据类型是对象，但进一步的
# 调查显示，它是字符串
type(df['diagnosis'][0])

# Pandas 实际上将 dataframe 和序列中的字符串存储为 [指针](https://en.wikipedia.org/wiki/Pointer_(computer_programming) ，因此，数据类型是 object 而不是 str。了解这一点对数据分析来说并不重要，只需知道字符串在 Pandas 中以对象的形式呈现。

# 显示 dataframe 的简明摘要，
# 包括每列非空值的数量
df.info()
# 返回每列数据的有效描述性统计
df.describe()

# 返回 dataframe 中的前几行
# 默认返回前五行
df.head()

# 但是也可以指定你希望返回的行数
df.head(20)


# `.tail()` 返回最后几行，但是也可以指定你希望返回的行数
df.tail(2)

# 查看每列的索引号和标签
for i, v in enumerate(df.columns):
    print(i, v)
'''
0 id
1 diagnosis
2 radius_mean
3 texture_mean
4 perimeter_mean
5 area_mean
6 smoothness_mean
7 compactness_mean
8 concavity_mean
9 concave_points_mean
10 symmetry_mean
11 fractal_dimension_mean
12 radius_SE
13 texture_SE
14 perimeter_SE
15 area_SE
16 smoothness_SE
17 compactness_SE
18 concavity_SE
19 concave_points_SE
20 symmetry_SE
21 fractal_dimension_SE
22 radius_max
23 texture_max
24 perimeter_max
25 area_max
26 smoothness_max
27 compactness_max
28 concavity_max
29 concave_points_max
30 symmetry_max
31 fractal_dimension_max
'''
# 选择从 'id' 到最后一个均值列的所有列
df_means = df.loc[:,'id':'fractal_dimension_mean']
df_means.head()

# 用索引号重复以上步骤
df_means = df.iloc[:,:12]
df_means.head()
```

#### 用mask 从数据中取出特定的行
```python
import pandas as pd
df = pd.read_csv('cancer_data_edited.csv')
df.head()

#将符合条件的数据取出来
df_m = df[df['diagnosis']=='M'] # diagnosis 是列名 M 是值
mask = df['diagnosis'] == 'M'
df_m = df[mask]  
df_m['area'].describe()  #
```