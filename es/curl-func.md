```
查看索引
curl localhost:9200/_cat/indices?v

删除索引
curl -X DELETE 'http://localhost:9200/prometheus'

索引起别名
curl -XPUT localhost:9200/索引/_alias/别名

查看索引结构
curl localhost:9200/prometheus/_mapping?pretty

查看全部数据
curl 'localhost:9200/prometheus/_search' -d '{"query": {"match_all": {}}}' -H 'Content-Type:application/json'
```