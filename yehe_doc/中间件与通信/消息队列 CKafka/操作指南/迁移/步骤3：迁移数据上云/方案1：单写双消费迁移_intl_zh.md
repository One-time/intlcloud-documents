## 操作场景

本文主要介绍使用单写双消费方案将自建 Kafka 集群的数据迁移到 CKafka 中的方法。

## 前提条件    

- 已 [购买云上 CKafka 实例](https://intl.cloud.tencent.com/document/product/597/41379)。
- 已 [迁移 Topic 上云](https://intl.cloud.tencent.com/document/product/597/41380)。

## 操作步骤

对于数据有序性要求不高的情况下，可以采用多个消费者并行消费的方式进行切换。

单写双消费的方式简单清晰便于操作且无数据积压，平滑过渡； 但是需要业务侧新增一套消费者。

其迁移步骤如下所示：
![](https://main.qcloudimg.com/raw/7b41c8c1f3740a9b5b6ad45f6b369cc0.png)

1. 旧的消费者保持不动，消费端新起消费者，配置新的集群的 bootstrap-server，消费新的 CKafka 集群。
    需要配置 `--bootstrap-server` 中的 IP 为 CKafka 实例的接入网络，在控制台的实例详情页面**接入方式**模块的网络列复制。
  ```bash
./kafka-console-consumer.sh --bootstrap-server xxx.xxx.xxx.xxx:9092 --from-beginning --new-consumer --topic topicName --consumer.config ../config/consumer.properties
  ```

2. 切换生产流，生产者将数据生产到 CKafka 实例。
   修改 broker-list 中的 IP 为 CKafka 实例的接入网络，topicName 为 CKafka 实例中的 Topic 名称：
```bash
 ./kafka-console-producer.sh --broker-list xxx.xxx.xxx.xxx:9092 --topic topicName
```

3. 原有消费者无需特殊配置，继续消费自建 Kafka 集群的数据。当原有自建集群的数据消费完成后，即迁移完毕。

>!上文给出的是测试命令，正式业务的运行只需要修改相应应用程序配置的 broker 地址，然后重启相应的应用即可。
