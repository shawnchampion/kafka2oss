
## 应用简介
本应用支持将 kafka 某个 topic 中的消息定时导入到 oss 对应 bucket 中。入参：
```json
{
    "consumer_service_name":"kafka_to_oss_demo",
    "consumer_function_name":"consumer_function_name",
    "kafka_instance_id":"alikafka_post-cn-qra2lc4fr00y",
    "topic_name":"Kafka2OSS",
    "consumer_group_id":"Kafka2OSS-Consumer-group",
    "bucket_name":"kafka2oss-dest",
    "kafka_endpoint": ["alikafka-post-cn-qra2lc4fr00y-1-vpc.alikafka.aliyuncs.com:9092","alikafka-post-cn-qra2lc4fr00y-2-vpc.alikafka.aliyuncs.com:9092","alikafka-post-cn-qra2lc4fr00y-3-vpc.alikafka.aliyuncs.com:9092"]
}
```
说明：
consumer_service_name：调用的 consumer 服务名称
consumer_function_name：调用的 consumer 函数名称
kafka_instance_id：消费的实例 id
topic_name：消费的实例 topic 名称
consumer_group_id：消费组名称
bucket_name：结果存储 bucket 名称
kafka_endpoint：kafka 地址

## 使用步骤

1. 在 kafka 控制台创建实例、topic 及消费组，填入上述的 kafka_instance_id、consumer_group_id 及 topic_name 中；
2. 在 ram 控制台创建一个 ram 角色，并赋予如下权限策略（也可使用示例中的 fc default role）：
```json
{
    "Version": "1",
    "Statement": [
        {
            "Action": [
                "fc:InvokeFunction",
                "log:*",
                "oss:*"
            ],
            "Resource": "*",
            "Effect": "Allow"
        }
    ]
}
```
3. 更新最新版 S 工具；s build --use-docker
4. git clone 本项目。更改 s.yaml 中触发器触发参数为上述实际参数，在项目目录中执行如下命令： `s deploy -t s.yaml`
