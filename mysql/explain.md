```
id
查询编号，如果没有子查询或者联合查询的话，就只有一条，如果是联合查询的话，那么会出现一条id为null的记录，并且标志查询结果
```

```
select_type
关联类型，决定访问表的方式

SIMPLE
简单查询，代表没有子查询或者union。

PRIMARY
如果不是简单查询，那么最外层查询就会被标记成PRIMARY。

UNION
联合查询

DERIVED
用来标记出现在from里的子查询

SUBQUERY
不在from里的子查询。

DEPENDENT
代表关联子查询

UNCACHEABLE
代表不能缓存的子查询

MATERIALIZED
物化子查询是Mysql对子查询的优化，第一次执行子查询时会将结果保存到临时表，物化子查询只需要执行一次
```

```
table
表名
```

```
partitions
数据的分区信息
```

```
type
关联类型，决定通过什么方式找到每一行数据。以下按照速度由快到慢。

system>const>eq_ref>ref>fulltext>ref_or_null>index_merge>unique_subquery>index_subquery>range>index>ALL。

system&const
这通常是最快的查找方式，代表Mysql通过优化最终转换成常量查询，最常规的做法就是直接通过主键或者唯一索引查询。
而system是const的一个特例（只有一行数据的系统表），随便找一张系统表，就插入一条数据就可以看到system了。

eq_ref
通常通过主键索引或者唯一索引查询时会看到eq_ref，它最多只返回一条数据

ref
也是通过索引查找，但是和eq_ref不同，ref可能匹配到多条符合条件的数据，比如最左前缀匹配或者不是主键和唯一索引。

fulltext
使用FULLTEXT索引

ref_or_null
和ref类似，但是还要进行一次查询找到NULL的数据。

index_merge
索引合并

unique_subquery
按照官方文档所说，unique_subquery只是eq_ref的一个特例

index_subquery
和unique_subquery类似，只是针对的是非唯一索引。

range
看名字就知道，范围查询，其实就是带有限制条件的索引扫描

index
跟全表扫描类似，只是扫表是按照索引顺序进行。

ALL
全表扫描，没啥好说的。
```

```
possible_keys
可以使用哪些索引。
```

```
key
实际决定使用哪个索引
```

```
key_len
索引字段的可能最大长度，不是表中实际数据使用的长度
```

```
ref
表示key展示的索引实际使用的列或者常量。
```

```
rows
查询数据需要读取的行数，只是一个预估的数值，但是能很直观的看出SQL的优劣了。
```

```
filtered
5.1版本之后新增字段，表示针对符合查询条件的记录数的百分比估算，用rows和filtered相乘可以计算出关联表的行数。
```

```
Extra
解析查询的附加额外信息

Using index
使用覆盖索引。

Using index condition
使用索引下推，索引下推简单来说就是加上了条件筛选，减少了回表的操作

Using temporary
排序使用了临时表。

Using filesort
使用外部索引文件排序，但是不能从这里看出是内存还是磁盘排序，我们只能知道更消耗性能。

Using where
where过滤，没啥好说的。

Zero limit
除非你写个LIMIT 0。

Using sort_union(), Using union(), sing intersect()
使用了索引合并，参看上文。
```