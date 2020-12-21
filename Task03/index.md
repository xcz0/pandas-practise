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
各级索引名字可由 [varname].index.names 或 [varname].columns.names 获得。值由.values 获得。