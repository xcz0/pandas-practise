# 分组

## 模式及对象

### groupby对象

gb=df.groupby(condition)。其中condition 为分组依据，可分为：

* 单列索引名，按列中元素值分组
* bool 类型的等长 Series ，按 True/False 分组
* np.array 等长数组，按数组中元素分组
* 条件列表，按各条件组合值分组

常用属性：

* ngroups 分组数量
* groups 返回dict，键为组名，值为包含的行索引
* size() 各组元素个数
* get_ggroup(groupname_tuple) 传入组名，返回对应所有行

### 使用形式

gb[data].func()。其中data为所需分组数据，常使用列索引名，func()为使用操作。常用操作有：

* 聚会函数，每组返回一标量
* 变换函数，每组返回一个 Series 类型
* 过滤函数，每组返回所在行本身

## 聚合函数

### 内置聚合函数

常用内置聚合函数：

* max/min/mean/median/count/idxmax/idxmin/quantile/sum/std/var/
* all/any 全为真/任意为真
* mad  mean absolute deviation 偏差绝对值的平均
* sem standard error of the mean
* skew 偏度

### agg

agg用于补充内置函数不足：

* 使用多个函数 gb.agg(['sum', 'idxmax', 'skew'])
* 对特定的列使用特定的聚合函数 gb.agg({'Height':['mean','max'], 'Weight':'count'})
* 自定义函数 gb.agg(lambda x: x.mean()-x.min())
* 聚合结果重命名 gb.agg((func_name, func)) 。使用对一个或者多个列使用单个聚合的时候，重命名需要加方括号，否则就不知道是新的名字还是手误输错的内置函数字符串 gb.agg([('my_sum', 'sum')])

## 变换和过滤

### 变换函数

返回长度相同的序列，常用内置函数为累积函数，类似滑窗： cumcount/cumsum/cumprod/cummax/cummin 。若 skipna=False 则不忽略 NaN 。

transform() 与 agg 类似，可自定义函数，但不能通过传入字典来对指定列使用特定的变换。transform 还可以返回一个标量，这会使得结果被广播到其所在的整个组。

rank(method='average', ascending=True, na_option='keep', pct=False, axis=0)，Provide the rank of values within each group。 method：{‘average’, ‘min’, ‘max’, ‘first’, ‘dense’}

### 组索引与过滤

组过滤作为行过滤的推广，指的是如果对一个组的全体所在行进行统计的结果返回 True 则会被保留， False 则该组会被过滤，最后把所有未被过滤的组其对应的所在行拼接起来作为 DataFrame 返回。在 groupby 对象中，定义了 filter 方法进行组的筛选，其中自定义函数的输入参数为数据源构成的 DataFrame 本身，返回为布尔值。

## 跨列分组

对于分组进行跨行操作，首先，这显然不是过滤操作，因此 filter 不符合要求；其次，返回的均值是标量而不是序列，因此 transform 不符合要求；最后，似乎使用 agg 函数能够处理，但是之前强调过聚合函数是逐列处理的，而不能够 多列数据同时处理 。由此，引出了 apply 函数来解决这一问题。

apply 的自定义函数传入参数与 filter 完全一致，可返回多种类型：

* 标量：结果得到的是 Series ，索引与 agg 的结果一致
* Series 情况：得到的是 DataFrame ，行索引与标量情况一致，列索引为 Series 的索引
* DataFrame 情况：得到的是 DataFrame ，行索引最内层在每个组原先的索引上，再加一层返回的 DataFrame 行索引，同时分组结果 DataFrame 的列索引和返回的 DataFrame 列索引一致。

