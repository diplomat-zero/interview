# 索引的类型
| 索引类型 | 语句                                                                      |
|------|-------------------------------------------------------------------------|
| 普通索引 | alter table `table_name` add index index_name (`column`)           |
| 唯一索引 | alter table `table_name` add unique (`column`)                      |
| 联合索引 | alter table `table_name` add index index_name(`column1`,`column2`) |
| 主键索引 | alter table `table_name` add primary key(`column`)                  |
| 全文索引 | alter table `table_name` add fulltext (`column`)                    |
