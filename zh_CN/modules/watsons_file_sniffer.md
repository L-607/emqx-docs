# 文件嗅探协议

需求来源：

1. 文件传输协议的前置行为
2. Client & Server 互相检测文件状态

需求：

1. 识别文件 & 文件夹，文件路径探查
2. 读取隐藏文件
3. 静态获取（轮询） & 动态监控（推送）文件状态
4. 无外部 SDK 依赖，支持 MQTT 协议，并表明文件嗅探协议版本号

## 设计

### 文件嗅探交互方式

主动探查：问询者向目标发送消息，格式为

#### 请求

Topic

`$file_sniffer/v1/dir/${clientid}`

```json
{
    "request_id": "4246becb-a937-42de-ad6c-5395f1923f7f",
    "path": "/any/path"
}
```

请求参数
| Name | Info |
| - | - |
| ClientID | topic参数，标明查询双方中， 客户端的 clientid ，如果是服务端向设备端查询，也填写被查询的clientid |
| path | 需要查询的路径，可以是文件夹也可以是文件路径 |

#### 响应

Topic

`$file_sniffer/v1/dir/${clientid}`

当查询的路径是文件夹，需要返回该文件夹下的所有文件和次级文件夹信息，次级文件夹不展开

```json
{
    "request_id": "4246becb-a937-42de-ad6c-5395f1923f7f",
    "path": "/any/path",
    "type": "folder",
    "result": "OK",
    "folder_include": [
        {
            "name": "test.log",
            "type": "file"
        },
        {
            "name": "MyFolder",
            "type": "folder"
        }
    ]
}
```

当查询的路径是文件，仅返回文件信息

```json
{
    "request_id": "4246becb-a937-42de-ad6c-5395f1923f7f",
    "path": "/any/path/test.log",
    "type": "file",
    "result": "OK"
}
```

对于无权查看的文件，或者不存在的文件路径，则返回

```json
{
    "request_id": "4246becb-a937-42de-ad6c-5395f1923f7f",
    "path": "/any/path/not_allow.log",
    "result": "NOT_ALLOW"
}
```

```json
{
    "request_id": "4246becb-a937-42de-ad6c-5395f1923f7f",
    "path": "/any/path/not_exist.log",
    "result": "NOT_EXIST"
}
```

对于无法预估的文件错误，统一使用

```json
{
    "request_id": "4246becb-a937-42de-ad6c-5395f1923f7f",
    "path": "/any/path/error",
    "result": "ERROR"
}
```

### 文件传输请求（不限定文件传输协议）

传输前需要先使用文件嗅探协议确认文件状态，文件状态在确认后瞬间发生变化导致的文件传输失败不计入考量（业务规划时应该避免开启下载之后文件被删除或者权限变化）。

#### 下载

topic中使用的clientid统一为设备的clientid

发起
Topic

`$file_sniffer/v1/download/${clientid}`

```json
{
    "request_id": "da0036a7-4bbc-4009-b7be-79bc35f67c05",
    "path": "/any/path/any/file"
}
```

确认发起

Topic

`$file_sniffer/v1/download/${clientid}`

```json
{
    "request_id": "da0036a7-4bbc-4009-b7be-79bc35f67c05",
    "path": "/any/path/any/file",
    "ack": "ok",
    "topic": "$file/755d163c06adea767b4087b3c9b47aa9"
}
```

对于无权查看的文件，或者不存在的文件路径，则返回

```json
{
    "request_id": "da0036a7-4bbc-4009-b7be-79bc35f67c05",
    "path": "/any/path/any/file",
    "ack": "NOT_ALLOW"
}
```

```json
{
    "request_id": "da0036a7-4bbc-4009-b7be-79bc35f67c05",
    "path": "/any/path/any/file",
    "ack": "NOT_EXIST"
}
```

对于无法预估的文件错误，统一使用

```json
{
    "request_id": "da0036a7-4bbc-4009-b7be-79bc35f67c05",
    "path": "/any/path/any/file",
    "ack": "ERROR"
}
```

发起者收到响应之后，应当立即准备开始接收文件。
没有收到响应，或者ack的内容不是ok，则认为传输发起失败，认为是对端的异常

</br>

【此协议是针对于 nftp 协议的补充，解决了文件传输发起的问题】

#### 上传

发起
Topic

`$file_sniffer/v1/upload/${clientid}`

```json
{
    "request_id": "da0036a7-4bbc-4009-b7be-79bc35f67c05",
    "path": "/any/path/any/file",
    "target_path": "/any/path/any/file",
    "job_id": 100,
    "task_id": 20,
    "script_id": 20,
    "servers": [3301, 3302]
}
```

确认发起，ack 字段作为结果返回值，ok 表示可以开始上传。

Topic

`$file_sniffer/v1/upload/${clientid}`

```json
{
    "request_id": "da0036a7-4bbc-4009-b7be-79bc35f67c05",
    "path": "/any/path/any/file",
    "target_path": "/any/path/any/file",
    "topic": "$file/755d163c06adea767b4087b3c9b47aa9",
    "job_id": 100,
    "task_id": 20,
    "script_id": 20,
    "servers": [3301, 3302],
    "ack": "ok"
}
```

ack 使用 WAIT 表示需要避开网络 IO 高峰，等待时长为 timeout 字段，单位毫秒。 等待时间达到 job 的执行结束时间则不再重试，认为job失败，上报错误

```json
{
    "request_id": "da0036a7-4bbc-4009-b7be-79bc35f67c05",
    "path": "/any/path/any/file",
    "target_path": "/any/path/any/file",
    "ack": "WAIT",
    "timeout": 60000,
    "job_id": 100,
    "task_id": 20,
    "script_id": 20
}
```

#### 文件推送: 一对多广播

##### 设备（ Server 类型）发起广播

Topic

`$file_sniffer/v1/broadcast/${clientid}`

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

确认发起，ack 字段作为结果返回值，ok 表示可以开始接收推送。

`$file_sniffer/v1/broadcast/${clientid}`

```json
{
    "request_id": "da0036a7-4bbc-4009-b7be-79bc35f67c05",
    "path": "/any/path/any/file",
    "target_path": "/any/path/any/file",
    "job_id": 100,
    "task_id": 20,
    "script_id": 20,
    "groups": [1,2,3],
    "topic": "$file/${clientid}",
    "ack": "ok"
}
```

网络异常等情况返回

```json
{
    "ack": "ERROR | BadReq | ..."
}
```

##### 设备（ client 类型）监听广播

1. 订阅 Topic

`$file_sniffer/v1/push/${clientid}`

2. 接收消息

```json
{
    "request_id": "da0036a7-4bbc-4009-b7be-79bc35f67c05",
    "path": "/any/path/any/file",
    "target_path": "/any/path/any/file",
    "topic": "$file/${clientid}",
    "job_id": 100,
    "task_id": 20,
    "script_id": 20
}
```

客户端可以接收广播文件时，响应

`$file_sniffer/v1/push/${clientid}`

```json
{
    "request_id": "da0036a7-4bbc-4009-b7be-79bc35f67c05",
    "path": "/any/path/any/file",
    "target_path": "/any/path/any/file",
    "topic": "$file/${clientid}",
    "job_id": 100,
    "task_id": 20,
    "script_id": 20,
    "ack": "ok"
}
```

网络异常等情况返回

```json
{
    "ack": "ERROR | BadReq | ..."
}
```

#### 文件推送: 多对一、多对多汇总

门店端向服务端汇总文件数据

借用文件上传的部分，使用参数

```json
{
    "servers": [3301,3302]
}
```
