```
kafka 启动命令
nohup bin/kafka-server-start.sh config/server.properties &
```

```
kafka查看topic和消息内容命令
1、查询topic，进入kafka目录：
bin/kafka-topics.sh --list --zookeeper localhost:2181
 
2、查询topic内容：
bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic topicName --from-beginning

3.查看topic下partition数量：
bin/kafka-topics.sh --describe --zookeeper localhost:2181 --topic prometheusdata
```

```
查看group列表
bin/kafka-consumer-groups.sh --bootstrap-server localhost:9092 --list

查看group消费情况
bin/kafka-consumer-groups.sh --bootstrap-server localhost:9092 --group groupname --describe
```