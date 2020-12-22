# 索引

## 索引器

### 表的列索引

* 使用[name]取出相应的列，若为单字符串，返回Series对象，若为字符串列表，返回DataFrame。

* 若只需单列，等价于 .name

### 行索引

* Series 与DataFrame的列索引类似。区别之处在于多行索引列表还可由切片[name1:name2:step]（不包含name2）形式生成

* 除字符串索引外，还可由整数构成索引。易混，不常用

### loc索引器

一般形式：name.loc[row,col]

其中 row、col 可为：

* 单元素
* 元素列表
* 切片（头尾被包含，但须唯一）
* 逻辑列表
* 函数，以原数据作输入，上述形式作输出

### iloc索引器

与loc类似，不同在于适用对象变为整数序号值

### query

name.query(str) 将判别条件以字符串形式输入。可通过在字符串内使用@引入外部变量

### 随机抽样

name.sample(n,axis=0,frac=0.3,replace=False,weights)

* n 为抽样数量
* axis 为方向，0为行，1为列
* frac 为抽样比例
* replace 是否放回
* weight 个样本相对概率

## 多级索引

### 多级索引表结构

索引元素由单值变为元组，层级逐次递减。
各级索引名字可由 [varname].index.names 或 [varname].columns.names 获得。索引值由.values 获得。

由get_level_values(lawer)可获得某层索引

### 多级索引中loc索引器

与之前的用法相同，只需将标量替换为元组。元组中元素也可以是列表，代表多行或多列，全选使用 : 表示，例：[(level_0_list,
level_1_list), cols]

在索引前最好对MultiIndex 进行排序以避免性能警告，使用：sort_index()

### IndexSlice对象

定义：idx = pd.IndexSlice

基本形式为：

* loc[idx[row,col]]
* loc[idx[level_0_row,level_1_row],idx[level_0_col,level_1_col]]

### 多级索引的构造

* set_index()
* from_tuples(list_of_tuples,names=indexname)
* from_arrays()
* from_product([list1,list2],names=indexname) 两列表的笛卡儿积

## 常用方法

### 交换

基本方法：

* swaplevel(idx1,idx2,axis=0)
* reorder_levels(idx_list,axis=0)

### 删除

droplevel(idx_list,axis=1)

### 索引属性的修改


