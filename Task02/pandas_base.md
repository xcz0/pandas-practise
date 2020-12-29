# pandas基础

## 文件

### 读取

基本函数：

* pd.read_csv('data/my_csv.csv')
* pd.read_table('data/my_table.txt')
* pd.read_table('data/my_table.txt')

可选参数：

* header=None 表示第一行不作为列名
* index_col 表示把某一列或几列作为索引
* usecols 表示读取列的集合，默认读取所有的列
* parse_dates 表示需要转化为时间的列
* nrows 表示读取的数据行数
* sep=' \|\|\|\| ' 自定义分割符号
* engine='python' 引擎

### 写入

基本函数：

* df_csv.to_csv('data/my_csv_saved.csv')
* df_excel.to_excel('data/my_excel_saved.xlsx')
* to_csv('data/my_table.txt')
* df_csv.to_markdown()
* df_csv.to_latex()

可选参数：

* index=False 表示去除原文件第一行索引
* sep='\t' 自定义分割符号
* usecols 表示读取列的集合，默认读取所有的列

## 数据结构

### Series

由四个部分组成，分别是：

* data 序列的值
* index = pd.Index([], name='') 索引
* dtype 存储类型
* name 序列的名字

获取信息：

* s.values 数据
* s.index 索引
* s.name 名字
* s.shape 大小
* s[index] 依索引获取数据

### DataFrame

相对于二维的Series, 增加了成员：columns 列索引

获取信息：

* df.values 数据
* df.index 行索引
* df.columns 列索引
* df.shape 大小
* df[col] 依列索引获取数据，当col只有一个时，退化为Series
* df.T 转置

## 常用函数

### 汇总函数

* df.head(n=5) 前n行数据
* df.tail(n=5) 后n行数据
* df.info() 表的信息概况
* df.describe() 表中数值列对应的主要统计量

### 特征统计函数

* df.sum() 
* df.mean() 
* df.median() 
* df.var() 
* df.std()
* df.min()
* df.max()
* df.quantile() 分位数
* df.count() 非缺失值个数
* df.idxmax() 最大值索引
* axis=0 默认为0代表逐列统计，1表示逐行统计

