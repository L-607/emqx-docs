# Agent Data Flow - Push： 推送

## 场景

服务端产生文件，例如营销活动文件、脚本 BAT 文件，下发到门店中。

EMQX 将上传的缓存推送至门店。

## Job 控制

推送行为不受门店控制，仅有发起者（Server）的 Job 控制。门店应当在收到推送指令后立即接受文件

## 门店监听

Topic

```text
$file_sniffer/v1/push/${clientid}
```

Qos 1
</br>
文件推送指令会通过此 topic 的消息下发至 Agent，并将推送文件的业务信息一并发给 Agent

## 发起 Push

Topic

```text
$file_sniffer/v1/push/${clientid}
```

QoS 1
</br>
Payload

```json
{
    "request_id": "da0036a7-4bbc-4009-b7be-79bc35f67c05",
    "path": "/any/path/any/file",
    "target_path": "/any/path/any/file",
    "topic": "$file/${PUSH topic suffix}",
    "job_id": 100,
    "task_id": 20,
    "script_id": 20
}
```

## 响应 Push

Agent 在收到 Push 报文后，立即订阅报文中指定的 topic

```text
$file/${PUSH topic suffix}
```

订阅完成后，向服务端响应

Topic

```text
$file_sniffer/v1/push/${clientid}
```

QoS 1
</br>
Payload

```json
{
    "ack" : "ok"
}
```

## 文件传输 - 下载

使用 Push 报文中的 Topic

Topic

```text
$file/${PUSH topic suffix}
```

QoS 1
</br>
Payload
使用 nftp 文件传输协议（1.0 版本），协议细节参考 nftp 章节

```text
file content encode by nftp
```
