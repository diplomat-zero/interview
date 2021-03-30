Q:
一张表，里面有ID自增主键，当insert了17条记录之后，删除了第15,16,17条记录，再把Mysql重启，再insert一条记录，这条记录的ID是18还是15?

A:
如果引擎是myisam 那么是18。因为myisam会将自增主键的最大id存储到数据文件里，重启mysql最大自增id依然存在。
如果引擎是innodb 那么是15。因为innodb会将自增主键的最大id存储到内存中，重启mysql会丢失。

Q:
Heap表是什么?

A:
HEAP表存在于内存中，用于临时高速存储。
BLOB或TEXT字段是不允许的
只能使用比较运算符=，<，>，=>，= <
HEAP表不支持AUTO_INCREMENT
索引不可为NULL

Q:
CHAR和VARCHAR的区别？

A:
以下是CHAR和VARCHAR的区别：CHAR和VARCHAR类型在存储和检索方面有所不同CHAR列长度固定为创建表时声明的长度，长度值范围是1到255当CHAR值被存储时，它们被用空格填充到特定长度，检索CHAR值时需删除尾随空格。

