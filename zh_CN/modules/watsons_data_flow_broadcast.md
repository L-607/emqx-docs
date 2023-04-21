# Agent Data Flow - Broadcast： 上传

## 场景

服务端产生文件，例如营销活动文件、脚本 BAT 文件，下发到门店中。预先将文件上传至 EMQX 作为文件缓存

## Job 控制

参数

| Name | Info |
| - | - |
| job_id | Job 唯一标识符 |
| task_id | Task 唯一标识符 |
| script_id | Script 唯一标识符 |
| request_id | 传输文件的请求 ID，交互过程中唯一 |
| path | 文件源路径 |
| target_path | 目标路径 |
| groups | 广播地址，即门店 group id |

当服务端 Agent 到达 Job 执行时间（根据 Job 信息中的 execution_time 字段，crontab 类型），开始向 EMQX 发起执行广播请求。

## 发起 Broadcast

通过 MQTT 报文
Topic

```text
$file_sniffer/v1/broadcast/${clientid}
```

</br>
QoS 1
</br>
Payload

```json
{
    "request_id": "da0036a7-4bbc-4009-b7be-79bc35f67c05",
    "path": "/any/path/any/file",
    "target_path": "/any/path/any/file",
    "job_id": 100,
    "task_id": 20,
    "script_id": 20,
    "groups": [1,2,3]
}
```

## 响应 Broadcast

Topic

```text
$file_sniffer/v1/broadcast/${clientid}
```

</br>
QoS 1
</br>
Payload

发起请求之后，服务端根据当前 Job 的 MaxCurrentSession 限制（即最大并行量），返回给客户端

| Name | Value | Info |
| - | - | - |
| ack | ok | 可以执行 |
| ack | WAIT | 已到达最大执行限制，等待 |
| ack | ERROR | 服务器出现异常，或者 Agent 端没有相关权限 |
| timeout | Integer() | 当到达最大限制时，等待时长 |
| topic | String() | 文件传输使用的 Topic，由服务端分配，保证文件通道唯一 |

```json
{
    "ack" : "ok | WAIT | ERROR",
    "topic": "$file/${trans topic suffix}"
}
```

## 文件传输 - 上传

使用 Broadcast 响应中的 Topic

Topic

```text
$file/${trans topic suffix}
```

QoS 1
</br>
Payload
使用 nftp 文件传输协议（1.0 版本），协议细节参考 nftp 章节

```text
file content encode by nftp
```
