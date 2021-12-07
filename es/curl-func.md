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

删除全部数据(不删除索引结构)
curl 'localhost:9200/prometheus/_delete_by_query' -d '{"query": {"match_all": {}}}' -H 'Content-Type:application/json'

索引新增字段
curl -X PUT localhost:9200/prometheus/_mapping -d '{"properties":{"status":{"type":"keyword"}}}' -H 'Content-Type:application/json'

es update_by_query
curl 'localhost:9200/prometheus/_update_by_query' -d '{"query": {"bool": {"must": [{"term":{"metric": "process_open_fds"}},{"term":{"time": "1632280868"}}]}},"script": {"inline": "ctx._source.status = params.status","params": {"status": "1"},"lang": "painless"}}' -H 'Content-Type:application/json'

es query
curl 'localhost:9200/capacity/_search' -d '{"query":{"bool":{"must":[{"term":{"metric":"process_open_fds"}},{"term":{"time":"1632280868"}}]}}}' -H 'Content-Type:application/json'
```

curl 'localhost:9200/capacity/_search' -d '{"query":{"bool":{"must":[{"range":{"time":{"gte":1638430200,"lte":1638435600}}}]}}}' -H 'Content-Type:application/json'
