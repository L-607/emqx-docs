# API docs
### 接口文档

#### 分页说明

- list：当前页数据
- total: 当前查询条件下的数据总数，(total/pageSize) + 1 = 总页数
- pageSize： 一页数据量
- pageNo: 页码

---

title: emqx-sdes v1.0.0
language_tabs:

  - shell: Shell
  - http: HTTP
  - javascript: JavaScript
  - ruby: Ruby
  - python: Python
  - php: PHP
  - java: Java
  - go: Go
    toc_footers: []
    includes: []
    search: true
    code_clipboard: true
    highlight_theme: darkula
    headingLevel: 2
    generator: "@tarslib/widdershins v4.0.17"

---

# emqx-sdes

> v1.0.0

Base URLs:

# JobLogApi

## GET 按客户端详细信息获取作业日志

GET /v1/logs/clients/jobs

### 请求参数

| 名称     | 位置  | 类型   | 必选 | 说明                 |
| -------- | ----- | ------ | ---- | -------------------- |
| status   | query | string | 是   | SUCCESS, FAILED, ALL |
| startAt  | query | Long   | 否   | 起使时间             |
| pageSize | query | string | 是   | none                 |
| pageNo   | query | string | 是   | none                 |

> 返回示例

> 成功

```json
{
  "total": 0,
  "list": [
    {
      "status": "",
      "startTime": 0,
      "endTime": 0,
      "nowTime": 0,
      "reportId": "",
      "jobId": 0,
      "jobName": "",
      "jobDesc": ""
    }
  ]
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

*[Class{@code Object} is the root of the class hierarchy.
Every class has{@code Object} as a superclass. All objects,
including arrays, implement the methods of this class.]*

| 名称 | 类型 | 必选 | 约束 | 中文名 | 说明 |
| ---- | ---- | ---- | ---- | ------ | ---- |

## GET getJobLogsByClient

GET /v1/logs/clients

### 请求参数

| 名称     | 位置  | 类型   | 必选 | 说明                 |
| -------- | ----- | ------ | ---- | -------------------- |
| status   | query | string | 是   | SUCCESS, FAILED, ALL |
| clientId | query | string | 是   | none                 |
| startAt  | query | Long   | 否   | 起使时间             |
| pageSize | query | string | 是   | none                 |
| pageNo   | query | string | 是   | none                 |

> 返回示例

> 成功

```json
{
  "total": 0,
  "list": [
    {
      "status": "",
      "mqttClientId": "",
      "clientId": 0,
      "ipAddress": "",
      "username": "",
      "role": "ENMU('SERVER', 'STORE')"
    }
  ]
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

*cn.xiaohuodui.common.http.Page<cn.xiaohuodui.vo.JobLogsByClientVo>*

| 名称 | 类型 | 必选 | 约束 | 中文名 | 说明 |
| ---- | ---- | ---- | ---- | ------ | ---- |

## GET 按客户端详细信息任务获取作业日志

GET /v1/logs/clients/jobs/tasks

### 请求参数

| 名称     | 位置  | 类型   | 必选 | 说明     |
| -------- | ----- | ------ | ---- | -------- |
| clientId | query | string | 是   | none     |
| jobId    | query | string | 是   | none     |
| reportId | query | string | 是   | none     |
| startAt  | query | Long   | 否   | 起使时间 |
| pageSize | query | string | 是   | none     |
| pageNo   | query | string | 是   | none     |

> 返回示例

> 成功

```json
{
  "total": 0,
  "list": [
    {
      "status": "",
      "startTime": 0,
      "endTime": 0,
      "nowTime": 0,
      "taskId": 0,
      "taskName": "",
      "taskDesc": "",
      "order": 0,
      "priority": 0,
      "disableValidation": false
    }
  ]
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

*[Class{@code Object} is the root of the class hierarchy.
Every class has{@code Object} as a superclass. All objects,
including arrays, implement the methods of this class.]*

| 名称 | 类型 | 必选 | 约束 | 中文名 | 说明 |
| ---- | ---- | ---- | ---- | ------ | ---- |

## GET 通过客户端详细信息任务脚本获取作业日志

GET /v1/logs/clients/jobs/tasks/scripts

### 请求参数

| 名称     | 位置  | 类型   | 必选 | 说明     |
| -------- | ----- | ------ | ---- | -------- |
| clientId | query | string | 是   | none     |
| jobId    | query | string | 是   | none     |
| taskId   | query | string | 是   | none     |
| reportId | query | string | 是   | none     |
| startAt  | query | Long   | 否   | 起使时间 |
| pageSize | query | string | 是   | none     |
| pageNo   | query | string | 是   | none     |

> 返回示例

> 成功

```json
{
    "code": "SUCCESS",
    "data": {
      "total": 1,
      "list": [
        {
              "reportId": "{2DD358AC-BD9B-3D41-A83C-F9A63EEA5A72}",
              "filePath": "c:\\Users\\emqx\\Desktop\\test.txt",
              "type": "COPY_FILE",
              "messages": [
                {
                    "startTime": 1678421820914,
                    "endTime": 1678421939863,
                    "message": "START"
                },
                {
                    "startTime": 1678421820904,
                    "endTime": 1678421820913,
                    "message": "Successed"
                }
            ],
              "scriptId": 6,
              "targetFilePath": "c:\\Users\\emqx\\Desktop\\demo\\test.txt",
              "block": true,
              "id": 6,
              "createFilePath": true,
              "order": 0
        }
      ]
    }
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

*[Class{@code Object} is the root of the class hierarchy.
Every class has{@code Object} as a superclass. All objects,
including arrays, implement the methods of this class.]*

| 名称 | 类型 | 必选 | 约束 | 中文名 | 说明 |
| ---- | ---- | ---- | ---- | ------ | ---- |

## GET getJobsByStatus

GET /v1/logs/jobs

### 请求参数

| 名称     | 位置  | 类型   | 必选 | 说明                 |
| -------- | ----- | ------ | ---- | -------------------- |
| status   | query | string | 是   | SUCCESS, FAILED, ALL |
| startAt  | query | Long   | 否   | 起使时间             |
| pageSize | query | string | 是   | none                 |
| pageNo   | query | string | 是   | none                 |

> 返回示例

> 成功

```json
{
  "total": 0,
  "list": [
    {
      "status": "",
      "startTime": 0,
      "endTime": 0,
      "jobId": 0,
      "jobName": "",
      "jobDesc": "",
      "LastEditedAt": "",
      "priority": 0,
      "executionTime": "",
      "duration": 0
    }
  ]
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

*cn.xiaohuodui.common.http.Page<cn.xiaohuodui.vo.JobLogsVo>*

| 名称 | 类型 | 必选 | 约束 | 中文名 | 说明 |
| ---- | ---- | ---- | ---- | ------ | ---- |

## GET getJobClientsByJob

GET /v1/logs/jobs/clients

### 请求参数

| 名称     | 位置  | 类型   | 必选 | 说明                 |
| -------- | ----- | ------ | ---- | -------------------- |
| status   | query | string | 是   | SUCCESS, FAILED, ALL |
| jobId    | query | string | 是   | none                 |
| startAt  | query | Long   | 否   | 起使时间             |
| pageSize | query | string | 是   | none                 |
| pageNo   | query | string | 是   | none                 |

> 返回示例

> 成功

```json
{
  "total": 0,
  "list": [
    {
      "status": "",
      "mqttClientId": "",
      "clientId": 0,
      "username": "",
      "ipAddress": "",
      "reportId": ""
    }
  ]
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

*cn.xiaohuodui.common.http.Page<cn.xiaohuodui.vo.JobLogClientByJobVo>*

| 名称 | 类型 | 必选 | 约束 | 中文名 | 说明 |
| ---- | ---- | ---- | ---- | ------ | ---- |

## GET getJobTasksByJobClient

GET /v1/logs/jobs/clients/tasks

### 请求参数

| 名称     | 位置  | 类型   | 必选 | 说明     |
| -------- | ----- | ------ | ---- | -------- |
| clientId | query | string | 是   | none     |
| jobId    | query | string | 是   | none     |
| reportId | query | string | 是   | none     |
| startAt  | query | Long   | 否   | 起使时间 |
| pageSize | query | string | 是   | none     |
| pageNo   | query | string | 是   | none     |

> 返回示例

> 成功

```json
{
  "total": 0,
  "list": [
    {
      "status": "",
      "startTime": 0,
      "endTime": 0,
      "nowTime": 0,
      "taskId": 0,
      "taskName": "",
      "taskDesc": "",
      "order": 0,
      "priority": 0,
      "disableValidation": false
    }
  ]
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

*[Class{@code Object} is the root of the class hierarchy.
Every class has{@code Object} as a superclass. All objects,
including arrays, implement the methods of this class.]*

| 名称 | 类型 | 必选 | 约束 | 中文名 | 说明 |
| ---- | ---- | ---- | ---- | ------ | ---- |

## GET getScriptLogByJobClient

GET /v1/logs/jobs/clients/tasks/scripts

### 请求参数

| 名称     | 位置  | 类型   | 必选 | 说明     |
| -------- | ----- | ------ | ---- | -------- |
| clientId | query | string | 是   | none     |
| jobId    | query | string | 是   | none     |
| taskId   | query | string | 是   | none     |
| reportId | query | string | 是   | none     |
| startAt  | query | Long   | 否   | 起使时间 |
| pageSize | query | string | 是   | none     |
| pageNo   | query | string | 是   | none     |

> 返回示例

> 成功

```json
{
    "code": "SUCCESS",
    "data": {
      "total": 1,
      "list": [
        {
              "reportId": "{2DD358AC-BD9B-3D41-A83C-F9A63EEA5A72}",
              "filePath": "c:\\Users\\emqx\\Desktop\\test.txt",
              "type": "COPY_FILE",
              "messages": [
                {
                    "startTime": 1678421820914,
                    "endTime": 1678421939863,
                    "message": "START"
                },
                {
                    "startTime": 1678421820904,
                    "endTime": 1678421820913,
                    "message": "Successed"
                }
            ],
              "scriptId": 6,
              "targetFilePath": "c:\\Users\\emqx\\Desktop\\demo\\test.txt",
              "block": true,
              "id": 6,
              "createFilePath": true,
              "order": 0
        }
      ]
    }
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

*[Class{@code Object} is the root of the class hierarchy.
Every class has{@code Object} as a superclass. All objects,
including arrays, implement the methods of this class.]*

| 名称 | 类型 | 必选 | 约束 | 中文名 | 说明 |
| ---- | ---- | ---- | ---- | ------ | ---- |

# dashboard

## GET 日志统计

GET /v1/dashboard/logs/count

> 返回示例

> 200 Response

```json
{
  "clients": 0,
  "jobs": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称      | 类型   | 必选 | 约束 | 中文名 | 说明 |
| --------- | ------ | ---- | ---- | ------ | ---- |
| » clients | number | true | none |        | none |
| » jobs    | number | true | none |        | none |

## GET task logs

GET /v1/logs/tasks

### 请求参数

| 名称     | 位置  | 类型   | 必选 | 说明 |
| -------- | ----- | ------ | ---- | ---- |
| clientId | query | string | 是   | none |
| jobId    | query | string | 是   | none |

> 返回示例

> 200 Response

```json
{
  "list": [
  {
    "status": "string",
    "startTime": 0,
    "endTime": 0,
    "taskId": 0,
    "taskName": "string",
    "reportId": "string",
    "order": 0,
    "priority": 0,
    "disableValidation": true
  }
  ],
  "total": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称                 | 类型     | 必选 | 约束 | 中文名 | 说明 |
| -------------------- | -------- | ---- | ---- | ------ | ---- |
| » list               | [object] | true | none |        | none |
| »» status            | string   | true | none |        | none |
| »» startTime         | number   | true | none |        | none |
| »» endTime           | number   | true | none |        | none |
| »» taskId            | number   | true | none |        | none |
| »» taskName          | string   | true | none |        | none |
| »» reportId          | string   | true | none |        | none |
| »» order             | integer  | true | none |        | none |
| »» priority          | integer  | true | none |        | none |
| »» disableValidation | boolean  | true | none |        | none |
| » total              | number   | true | none |        | none |

## GET script logs

GET /v1/logs/scripts

### 请求参数

| 名称     | 位置  | 类型   | 必选 | 说明 |
| -------- | ----- | ------ | ---- | ---- |
| clientId | query | string | 是   | none |
| jobId    | query | string | 是   | none |
| taskId   | query | string | 是   | none |

> 返回示例

> 200 Response

```json
{
  "total": 0,
  "list": [
    {
      "transferOperation": null,
      "filePath": "string",
      "type": "string",
      "message": "string",
      "ignoreHiddenFile": true,
      "recvFileScriptId": 0,
      "scriptId": 0,
      "targetFilePath": "string",
      "maxRetryTime": 0,
      "isItem": true,
      "startTime": 0,
      "endTime": 0,
      "createFilePath": true,
      "order": 0,
      "status": "string"
    }
  ]
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称                 | 类型     | 必选 | 约束 | 中文名 | 说明                                                         |
| -------------------- | -------- | ---- | ---- | ------ | ------------------------------------------------------------ |
| » total              | integer  | true | none |        | none                                                         |
| » list               | [object] | true | none |        | none                                                         |
| »» transferOperation | null     | true | none |        | none                                                         |
| »» filePath          | string   | true | none |        | none                                                         |
| »» type              | string   | true | none |        | enum('SEND_FILE', 'RECV_FILE', 'COPY_FILE', 'DELETE_FILE', 'EXECUTE_FILE', 'WAIT_FLAG_FILE', 'GET_FILE_STATUS', 'IF', 'BROADCAST', 'UPLOAD_TO_SERVER') |
| »» message           | string   | true | none |        | none                                                         |
| »» ignoreHiddenFile  | boolean  | true | none |        | none                                                         |
| »» recvFileScriptId  | integer  | true | none |        | none                                                         |
| »» scriptId          | integer  | true | none |        | none                                                         |
| »» targetFilePath    | string   | true | none |        | none                                                         |
| »» maxRetryTime      | integer  | true | none |        | none                                                         |
| »» isItem            | boolean  | true | none |        | none                                                         |
| »» startTime         | integer  | true | none |        | none                                                         |
| »» endTime           | integer  | true | none |        | none                                                         |
| »» createFilePath    | boolean  | true | none |        | none                                                         |
| »» order             | integer  | true | none |        | none                                                         |
| »» status            | string   | true | none |        | none                                                         |

## GET client logs overview

GET /v1/logs/clients/overview

> 返回示例

> 200 Response

```json
{
  "list": [
    {
      "status": "string",
      "mqttClientId": "string",
      "clientId": 0,
      "username": "string",
      "ipAddress": "string"
    }
  ],
  "total": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称            | 类型     | 必选  | 约束 | 中文名 | 说明                                     |
| --------------- | -------- | ----- | ---- | ------ | ---------------------------------------- |
| » list          | [object] | true  | none |        | none                                     |
| »» status       | string   | false | none |        | enum('SUCCESS', 'FAILED', 'NOT_EXECUTE') |
| »» mqttClientId | string   | false | none |        | none                                     |
| »» clientId     | integer  | false | none |        | none                                     |
| »» username     | string   | false | none |        | none                                     |
| »» ipAddress    | string   | false | none |        | none                                     |
| » total         | integer  | true  | none |        | none                                     |


## GET job logs

GET /v1/logs/jobs

### 请求参数

| 名称   | 位置  | 类型   | 必选 | 说明 |
| ------ | ----- | ------ | ---- | ---- |
| status | query | number | 是   | none |

> 返回示例

> 200 Response

```json
{
  "list": [
  {
    "status": "string",
    "startTime": 0,
    "endTime": 0,
    "jobId": 0,
    "jobName": "string",
    "jobDesc": "string"
  }
  ],
  "total": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称         | 类型     | 必选  | 约束 | 中文名 | 说明                      |
| ------------ | -------- | ----- | ---- | ------ | ------------------------- |
| » list       | [object] | true  | none |        | none                      |
| »» status    | string   | false | none |        | enum('SUCCESS', 'FAILED') |
| »» startTime | integer  | false | none |        | none                      |
| »» endTime   | integer  | false | none |        | none                      |
| »» jobId     | integer  | false | none |        | none                      |
| »» jobName   | string   | false | none |        | none                      |
| »» jobDesc   | string   | false | none |        | none                      |
| » total      | integer  | true  | none |        | none                      |

## GET client logs

GET /v1/logs/clients

### 请求参数

| 名称     | 位置  | 类型   | 必选 | 说明                      |
| -------- | ----- | ------ | ---- | ------------------------- |
| status   | query | string | 是   | enum('SUCCESS', 'FAILED') |
| clientId | query | string | 否   | none                      |
| jobId    | query | string | 否   | none                      |

> 返回示例

> 200 Response

```json
{
  "list": [
  {
    "status": "string",
    "startTime": 0,
    "endTime": 0,
    "jobId": 0,
    "jobName": "string",
    "jobDesc": "string",
    "mqttClientId": "string",
    "clientId": 0,
    "username": "string"
  }
  ],
  "total": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称            | 类型     | 必选  | 约束 | 中文名 | 说明                      |
| --------------- | -------- | ----- | ---- | ------ | ------------------------- |
| » list          | [object] | true  | none |        | none                      |
| »» status       | string   | false | none |        | enum('SUCCESS', 'FAILED') |
| »» startTime    | integer  | false | none |        | none                      |
| »» endTime      | integer  | false | none |        | none                      |
| »» jobId        | integer  | false | none |        | none                      |
| »» jobName      | string   | false | none |        | none                      |
| »» jobDesc      | string   | false | none |        | none                      |
| »» mqttClientId | string   | false | none |        | none                      |
| »» clientId     | integer  | false | none |        | none                      |
| »» username     | string   | false | none |        | none                      |
| » total         | integer  | true  | none |        | none                      |

# 数据模型


## GET 聚合报告

GET /v1/dashboard/reports

> 返回示例

> 200 Response

```json
{
  "clients": 0,
  "Groups": 0,
  "jobs": 0,
  "tasks": 0,
  "clientsOnline": 0,
  "clientsOffline": 0,
  "clientsDisabled": 0,
  "jobFailed": 0,
  "jobSuccess": 0,
  "jobNotExecuted": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称              | 类型    | 必选 | 约束 | 中文名 | 说明 |
| ----------------- | ------- | ---- | ---- | ------ | ---- |
| » clients         | integer | true | none |        | none |
| » Groups          | integer | true | none |        | none |
| » jobs            | integer | true | none |        | none |
| » tasks           | integer | true | none |        | none |
| » clientsOnline   | integer | true | none |        | none |
| » clientsOffline  | integer | true | none |        | none |
| » clientsDisabled | integer | true | none |        | none |
| » jobFailed       | integer | true | none |        | none |
| » jobSuccess      | integer | true | none |        | none |
| » jobNotExecuted  | integer | true | none |        | none |

# 数据模型


## GET Basic Info

GET /v1/dashboard/info

> 返回示例

> 200 Response

```json
{
  "clients": 0,
  "tasks": 0,
  "jobs": 0,
  "groups": 0,
  "tasksHistory": 0,
  "alerts": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称           | 类型    | 必选 | 约束 | 中文名 | 说明 |
| -------------- | ------- | ---- | ---- | ------ | ---- |
| » clients      | integer | true | none |        | none |
| » tasks        | integer | true | none |        | none |
| » jobs         | integer | true | none |        | none |
| » groups       | integer | true | none |        | none |
| » tasksHistory | integer | true | none |        | none |
| » alerts       | integer | true | none |        | none |

## GET Online Clients Chart

GET /v1/dashboard/onlineClients

### 请求参数

| 名称      | 位置  | 类型    | 必选 | 说明 |
| --------- | ----- | ------- | ---- | ---- |
| startTime | query | number  | 否   | none |
| endTime   | query | number  | 否   | none |
| interval  | query | integer | 否   | none |

> 返回示例

> 200 Response

```json
[
  {
    "clientCount": 0,
    "time": 0
  }
]
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称          | 类型    | 必选 | 约束 | 中文名 | 说明 |
| ------------- | ------- | ---- | ---- | ------ | ---- |
| » clientCount | integer | true | none |        | none |
| » time        | number  | true | none |        | none |

# config

## GET Job List

GET /v1/jobs

### 请求参数

| 名称                    | 位置  | 类型    | 必选 | 说明 |
| ----------------------- | ----- | ------- | ---- | ---- |
| jobName                 | query | string  | 否   | none |
| pageNo                  | query | integer | 否   | none |
| pageSize                | query | integer | 否   | none |
| jobNameContain          | query | string  | 否   | none |
| enabled                 | query | string  | 否   | none |
| lastEditedAtGte         | query | number  | 否   | none |
| lastEditedAtLte         | query | number  | 否   | none |
| lastRunAtGte            | query | number  | 否   | none |
| lastRunAtLte            | query | number  | 否   | none |
| assignmentsChangedAtGte | query | number  | 否   | none |
| assignmentsChangedAtLte | query | number  | 否   | none |
| createAtGte             | query | number  | 否   | none |
| createAtLte             | query | number  | 否   | none |

> 返回示例

> 200 Response

```json
{
  "list": [
    {
      "jobId": 0,
      "jobName": "string",
      "tasks": 0,
      "description": "string",
      "enabled": true,
      "maxRetryTimes": 0,
      "priority": 0,
      "cycleType": 0,
      "executionTime": null,
      "created": 0,
      "lastEditedAt": 0,
      "lastRun": null,
      "assignmentsChanged": null,
      "retryWait": 0
    }
  ],
  "total": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称                  | 类型         | 必选 | 约束 | 中文名 | 说明 |
| --------------------- | ------------ | ---- | ---- | ------ | ---- |
| » list                | [object]     | true | none |        | none |
| »» jobId              | integer      | true | none |        | none |
| »» jobName            | string       | true | none |        | none |
| »» tasks              | integer      | true | none |        | none |
| »» description        | string       | true | none |        | none |
| »» enabled            | boolean      | true | none |        | none |
| »» maxRetryTimes      | integer      | true | none |        | none |
| »» priority           | integer¦null | true | none |        | none |
| »» cycleType          | integer      | true | none |        | none |
| »» executionTime      | null         | true | none |        | none |
| »» created            | integer      | true | none |        | none |
| »» lastEditedAt       | integer¦null | true | none |        | none |
| »» lastRun            | null         | true | none |        | none |
| »» assignmentsChanged | null         | true | none |        | none |
| »» retryWait          | integer      | true | none |        | none |
| » total               | number       | true | none |        | none |

## POST Create Job

POST /v1/jobs

> Body 请求参数

```json
{
  "jobName": "string",
  "description": "string",
  "enabled": true,
  "maxRetries": 0,
  "priority": 0,
  "cycleType": 0,
  "executionTime": "string",
  "retryWait": 0,
  "lastRunAt": 0,
  "assignmentsChangedAt": 0
}
```

### 请求参数

| 名称                   | 位置 | 类型    | 必选 | 说明 |
| ---------------------- | ---- | ------- | ---- | ---- |
| body                   | body | object  | 否   | none |
| » jobName              | body | string  | 是   | none |
| » description          | body | string  | 是   | none |
| » enabled              | body | boolean | 是   | none |
| » maxRetries           | body | integer | 是   | none |
| » priority             | body | integer | 是   | none |
| » cycleType            | body | integer | 是   | none |
| » executionTime        | body | string  | 是   | none |
| » retryWait            | body | integer | 是   | none |
| » lastRunAt            | body | number  | 是   | none |
| » assignmentsChangedAt | body | number  | 是   | none |

> 返回示例

> 200 Response

```json
{
  "jobId": 0,
  "jobName": "string",
  "description": "string",
  "enable": true,
  "maxRetries": 0,
  "retryWait": 0,
  "tasks": 0,
  "enabled": true,
  "maxRetryTimes": 0,
  "priority": 0,
  "cycleType": 0,
  "executionTime": "string",
  "createdAt": 0,
  "lastEditedAt": 0,
  "lastRunAt": 0,
  "assignmentsChanged": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称                 | 类型    | 必选 | 约束 | 中文名 | 说明 |
| -------------------- | ------- | ---- | ---- | ------ | ---- |
| » jobId              | integer | true | none |        | none |
| » jobName            | string  | true | none |        | none |
| » description        | string  | true | none |        | none |
| » enable             | boolean | true | none |        | none |
| » maxRetries         | integer | true | none |        | none |
| » retryWait          | integer | true | none |        | none |
| » tasks              | integer | true | none |        | none |
| » enabled            | boolean | true | none |        | none |
| » maxRetryTimes      | integer | true | none |        | none |
| » priority           | integer | true | none |        | none |
| » cycleType          | integer | true | none |        | none |
| » executionTime      | string  | true | none |        | none |
| » createdAt          | integer | true | none |        | none |
| » lastEditedAt       | integer | true | none |        | none |
| » lastRunAt          | integer | true | none |        | none |
| » assignmentsChanged | integer | true | none |        | none |

## PUT update job

PUT /v1/jobs

> Body 请求参数

```json
{
  "jobId": 0,
  "jobName": "string",
  "description": "string",
  "enabled": true,
  "maxRetries": 0,
  "priority": 0,
  "cycleType": 0,
  "executionTime": "string",
  "retryWait": 0,
  "lastRunAt": 0,
  "assignmentsChangedAt": 0
}
```

### 请求参数

| 名称                   | 位置 | 类型    | 必选 | 说明 |
| ---------------------- | ---- | ------- | ---- | ---- |
| body                   | body | object  | 否   | none |
| » jobId                | body | number  | 是   | none |
| » jobName              | body | string  | 是   | none |
| » description          | body | string  | 是   | none |
| » enabled              | body | boolean | 是   | none |
| » maxRetries           | body | integer | 是   | none |
| » priority             | body | integer | 是   | none |
| » cycleType            | body | integer | 是   | none |
| » executionTime        | body | string  | 是   | none |
| » retryWait            | body | integer | 是   | none |
| » lastRunAt            | body | number  | 是   | none |
| » assignmentsChangedAt | body | number  | 是   | none |

> 返回示例

> 200 Response

```json
{
  "desc": "string"
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称   | 类型   | 必选 | 约束 | 中文名 | 说明 |
| ------ | ------ | ---- | ---- | ------ | ---- |
| » desc | string | true | none |        | none |

## GET Task List

GET /v1/tasks

### 请求参数

| 名称                    | 位置  | 类型    | 必选 | 说明 |
| ----------------------- | ----- | ------- | ---- | ---- |
| taskName                | query | string  | 否   | none |
| pageNo                  | query | integer | 否   | none |
| pageSize                | query | integer | 否   | none |
| taskNameContain         | query | string  | 否   | none |
| enabled                 | query | string  | 否   | none |
| lastEditedAtGte         | query | number  | 否   | none |
| lastEditedAtLte         | query | number  | 否   | none |
| lastRunAtGte            | query | number  | 否   | none |
| lastRunAtLte            | query | number  | 否   | none |
| assignmentsChangedAtGte | query | number  | 否   | none |
| assignmentsChangedAtLte | query | number  | 否   | none |
| createAtGte             | query | number  | 否   | none |
| createAtLte             | query | number  | 否   | none |

> 返回示例

> 200 Response

```json
{
  "list": [
    {
      "taskName": "string",
      "priority": 0,
      "lastEditedAt": 0,
      "taskId": 0,
      "enabled": true,
      "disableValidation": null,
      "lastRunAt": null,
      "assignmentsChangedAt": null,
      "description": "string",
      "createdAt": 0
    }
  ],
  "total": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称                    | 类型         | 必选 | 约束 | 中文名 | 说明 |
| ----------------------- | ------------ | ---- | ---- | ------ | ---- |
| » list                  | [object]     | true | none |        | none |
| »» taskName             | string¦null  | true | none |        | none |
| »» priority             | integer      | true | none |        | none |
| »» lastEditedAt         | integer¦null | true | none |        | none |
| »» taskId               | integer      | true | none |        | none |
| »» enabled              | boolean      | true | none |        | none |
| »» disableValidation    | null         | true | none |        | none |
| »» lastRunAt            | null         | true | none |        | none |
| »» assignmentsChangedAt | null         | true | none |        | none |
| »» description          | string       | true | none |        | none |
| »» createdAt            | integer      | true | none |        | none |
| » total                 | integer      | true | none |        | none |

## POST Create Task

POST /v1/tasks

> Body 请求参数

```json
{
  "taskName": "string",
  "priority": 0,
  "disableValidation": true,
  "lastRunAt": 0,
  "assignmentsChangedAt": 0,
  "enabled": true,
  "description": "string"
}
```

### 请求参数

| 名称                   | 位置 | 类型    | 必选 | 说明 |
| ---------------------- | ---- | ------- | ---- | ---- |
| body                   | body | object  | 否   | none |
| » taskName             | body | string  | 是   | none |
| » priority             | body | integer | 是   | none |
| » disableValidation    | body | boolean | 是   | none |
| » lastRunAt            | body | number  | 是   | none |
| » assignmentsChangedAt | body | number  | 是   | none |
| » enabled              | body | boolean | 是   | none |
| » description          | body | string  | 是   | none |

> 返回示例

> 200 Response

```json
{
  "taskId": 0,
  "name": "string",
  "priority": 0,
  "disableValidation": true,
  "lastRunAt": 0,
  "assignmentsChangedAt": 0,
  "enabled": true,
  "description": "string"
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称                   | 类型    | 必选 | 约束 | 中文名 | 说明 |
| ---------------------- | ------- | ---- | ---- | ------ | ---- |
| » taskId               | number  | true | none |        | none |
| » name                 | string  | true | none |        | none |
| » priority             | integer | true | none |        | none |
| » disableValidation    | boolean | true | none |        | none |
| » lastRunAt            | number  | true | none |        | none |
| » assignmentsChangedAt | number  | true | none |        | none |
| » enabled              | boolean | true | none |        | none |
| » description          | string  | true | none |        | none |

## PUT update Task

PUT /v1/tasks

> Body 请求参数

```json
{
  "taskId": 0,
  "name": "string",
  "priority": 0,
  "disableValidation": true,
  "lastRunAt": 0,
  "assignmentsChangedAt": 0,
  "enabled": true,
  "description": "string"
}
```

### 请求参数

| 名称                   | 位置 | 类型    | 必选 | 说明 |
| ---------------------- | ---- | ------- | ---- | ---- |
| body                   | body | object  | 否   | none |
| » taskId               | body | number  | 是   | none |
| » name                 | body | string  | 是   | none |
| » priority             | body | integer | 是   | none |
| » disableValidation    | body | boolean | 是   | none |
| » lastRunAt            | body | number  | 是   | none |
| » assignmentsChangedAt | body | number  | 是   | none |
| » enabled              | body | boolean | 是   | none |
| » description          | body | string  | 是   | none |

> 返回示例

> 200 Response

```json
{
  "desc": null
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称   | 类型 | 必选 | 约束 | 中文名 | 说明 |
| ------ | ---- | ---- | ---- | ------ | ---- |
| » desc | null | true | none |        | none |

## GET Job Detail

GET /v1/jobs/{jobId}/details

### 请求参数

| 名称  | 位置 | 类型   | 必选 | 说明 |
| ----- | ---- | ------ | ---- | ---- |
| jobId | path | number | 是   | none |

> 返回示例

> 200 Response

```json
{
  "general": {
    "jobName": "string",
    "description": "string",
    "createdAt": 0,
    "lastEditedAt": 0,
    "lastRunAt": 0,
    "enabled": true,
    "assignmentsChanged": 0
  },
  "executionOpt": {
    "priority": 0,
    "maxRetries": 0,
    "cycleType": 0,
    "retryWait": 0,
    "duration": 0,
    "executionTime": "string"
  }
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称                  | 类型    | 必选 | 约束 | 中文名 | 说明 |
| --------------------- | ------- | ---- | ---- | ------ | ---- |
| » general             | object  | true | none |        | none |
| »» jobName            | string  | true | none |        | none |
| »» description        | string  | true | none |        | none |
| »» createdAt          | number  | true | none |        | none |
| »» lastEditedAt       | number  | true | none |        | none |
| »» lastRunAt          | number  | true | none |        | none |
| »» enabled            | boolean | true | none |        | none |
| »» assignmentsChanged | number  | true | none |        | none |
| » executionOpt        | object  | true | none |        | none |
| »» priority           | integer | true | none |        | none |
| »» maxRetries         | integer | true | none |        | none |
| »» cycleType          | integer | true | none |        | none |
| »» retryWait          | number  | true | none |        | none |

## GET Job Groups

GET /v1/jobs/{jobId}/groups

### 请求参数

| 名称      | 位置  | 类型    | 必选 | 说明 |
| --------- | ----- | ------- | ---- | ---- |
| jobId     | path  | number  | 是   | none |
| groupName | query | string  | 否   | none |
| pageNo    | query | integer | 否   | none |
| pageSize  | query | integer | 否   | none |

> 返回示例

> 200 Response

```json
{
  "list": [
    {
      "groupId": 0,
      "groupName": "string",
      "type": 0,
      "lastEditedAt": 0,
      "enabled": true,
      "queryProperty": "string",
      "queryOperation": "string",
      "queryValue": "string",
      "assignmentsChangedAt": 0,
      "membershipChangedAt": 0,
      "lastRefreshedAt": 0,
      "description": "string",
      "createdAt": 0
    }
  ],
  "total": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称                    | 类型     | 必选  | 约束 | 中文名 | 说明 |
| ----------------------- | -------- | ----- | ---- | ------ | ---- |
| » list                  | [object] | true  | none |        | none |
| »» groupId              | integer  | true  | none |        | none |
| »» groupName            | string   | true  | none |        | none |
| »» type                 | integer  | true  | none |        | none |
| »» lastEditedAt         | integer  | true  | none |        | none |
| »» enabled              | boolean  | false | none |        | none |
| »» queryProperty        | string   | false | none |        | none |
| »» queryOperation       | string   | false | none |        | none |
| »» queryValue           | string   | false | none |        | none |
| »» assignmentsChangedAt | integer  | false | none |        | none |
| »» membershipChangedAt  | integer  | false | none |        | none |
| »» lastRefreshedAt      | integer  | false | none |        | none |
| »» description          | string   | false | none |        | none |
| »» createdAt            | integer  | false | none |        | none |
| » total                 | number   | true  | none |        | none |

## PUT bind job group

PUT /v1/jobs/{jobId}/groups

> Body 请求参数

```json
[
  0
]
```

### 请求参数

| 名称  | 位置 | 类型          | 必选 | 说明 |
| ----- | ---- | ------------- | ---- | ---- |
| jobId | path | number        | 是   | none |
| body  | body | array[number] | 否   | none |

> 返回示例

> 200 Response

```json
null
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | null     |

## GET Job Clients

GET /v1/jobs/{jobId}/clients

### 请求参数

| 名称                | 位置  | 类型          | 必选 | 说明 |
| ------------------- | ----- | ------------- | ---- | ---- |
| jobId               | path  | number        | 是   | none |
| pageNo              | query | integer       | 否   | none |
| pageSize            | query | integer       | 否   | none |
| clientId            | query | number        | 否   | none |
| username            | query | string        | 否   | none |
| usernameContain     | query | string        | 否   | none |
| mqttClientId        | query | array[string] | 否   | none |
| mqttClientIdContain | query | string        | 否   | none |
| status              | query | string        | 否   | none |
| enabled             | query | string        | 否   | none |
| connectedAtGte      | query | number        | 否   | none |
| connectedAtLte      | query | number        | 否   | none |
| disconnectedAtGte   | query | number        | 否   | none |
| disconnectedAtLte   | query | number        | 否   | none |
| createAtGte         | query | number        | 否   | none |

> 返回示例

> 200 Response

```json
{
  "total": 0,
  "list": [
    {
      "clientId": 0,
      "mqttClientId": "string",
      "username": null,
      "enable": true,
      "status": "string",
      "connectAt": null,
      "disconnectAt": 0,
      "createAt": 0
    }
  ]
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称            | 类型     | 必选  | 约束 | 中文名 | 说明 |
| --------------- | -------- | ----- | ---- | ------ | ---- |
| » total         | integer  | true  | none |        | none |
| » list          | [object] | true  | none |        | none |
| »» clientId     | integer  | false | none |        | none |
| »» mqttClientId | string   | false | none |        | none |
| »» username     | null     | false | none |        | none |
| »» enable       | boolean  | false | none |        | none |
| »» status       | string   | false | none |        | none |
| »» connectAt    | null     | false | none |        | none |
| »» disconnectAt | integer  | false | none |        | none |
| »» createAt     | integer  | false | none |        | none |

## PUT bind job clients

PUT /v1/jobs/{jobId}/clients

> Body 请求参数

```json
[
  0
]
```

### 请求参数

| 名称  | 位置 | 类型          | 必选 | 说明 |
| ----- | ---- | ------------- | ---- | ---- |
| jobId | path | number        | 是   | none |
| body  | body | array[number] | 否   | none |

> 返回示例

> 200 Response

```json
null
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | null     |

## GET Job Tasks

GET /v1/jobs/{jobId}/tasks

### 请求参数

| 名称                    | 位置  | 类型    | 必选 | 说明 |
| ----------------------- | ----- | ------- | ---- | ---- |
| jobId                   | path  | string  | 是   | none |
| taskName                | query | string  | 否   | none |
| pageNo                  | query | integer | 否   | none |
| pageSize                | query | integer | 否   | none |
| taskNameContain         | query | string  | 否   | none |
| enabled                 | query | string  | 否   | none |
| lastEditedAtGte         | query | number  | 否   | none |
| lastEditedAtLte         | query | number  | 否   | none |
| lastRunAtGte            | query | number  | 否   | none |
| lastRunAtLte            | query | number  | 否   | none |
| assignmentsChangedAtGte | query | number  | 否   | none |
| assignmentsChangedAtLte | query | number  | 否   | none |
| createAtGte             | query | number  | 否   | none |
| createAtLte             | query | number  | 否   | none |

> 返回示例

> 200 Response

```json
{
  "list": [
    {
      "taskName": "string",
      "priority": 0,
      "lastEditedAt": 0,
      "taskId": 0,
      "enabled": true,
      "disableValidation": null,
      "lastRunAt": null,
      "assignmentsChangedAt": null,
      "description": "string",
      "createdAt": 0
    }
  ],
  "total": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称                    | 类型         | 必选 | 约束 | 中文名 | 说明 |
| ----------------------- | ------------ | ---- | ---- | ------ | ---- |
| » list                  | [object]     | true | none |        | none |
| »» taskName             | string¦null  | true | none |        | none |
| »» priority             | integer      | true | none |        | none |
| »» lastEditedAt         | integer¦null | true | none |        | none |
| »» taskId               | integer      | true | none |        | none |
| »» enabled              | boolean      | true | none |        | none |
| »» disableValidation    | null         | true | none |        | none |
| »» lastRunAt            | null         | true | none |        | none |
| »» assignmentsChangedAt | null         | true | none |        | none |
| »» description          | string       | true | none |        | none |
| »» createdAt            | integer      | true | none |        | none |
| » total                 | integer      | true | none |        | none |

## PUT bind job task

PUT /v1/jobs/{jobId}/tasks

> Body 请求参数

```json
[
  0
]
```

### 请求参数

| 名称  | 位置 | 类型          | 必选 | 说明 |
| ----- | ---- | ------------- | ---- | ---- |
| jobId | path | number        | 是   | none |
| body  | body | array[number] | 否   | none |

> 返回示例

> 200 Response

```json
null
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | null     |

## GET Task Detail

GET /v1/tasks/{taskId}/details

### 请求参数

| 名称   | 位置 | 类型   | 必选 | 说明 |
| ------ | ---- | ------ | ---- | ---- |
| taskId | path | number | 是   | none |

> 返回示例

> 200 Response

```json
{
  "name": "string",
  "taskId": 0,
  "enabled": 0,
  "priority": 0,
  "disableValidation": true,
  "lastEditedAt": 0,
  "lastRunAt": 0,
  "assignmentsChangedAt": 0,
  "description": "string",
  "createdAt": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称                   | 类型    | 必选 | 约束 | 中文名 | 说明 |
| ---------------------- | ------- | ---- | ---- | ------ | ---- |
| » name                 | string  | true | none |        | none |
| » taskId               | number  | true | none |        | none |
| » enabled              | integer | true | none |        | none |
| » priority             | integer | true | none |        | none |
| » disableValidation    | boolean | true | none |        | none |
| » lastEditedAt         | number  | true | none |        | none |
| » lastRunAt            | number  | true | none |        | none |
| » assignmentsChangedAt | number  | true | none |        | none |
| » description          | string  | true | none |        | none |
| » createdAt            | number  | true | none |        | none |

## GET Task Script

GET /v1/tasks/{taskId}/scripts

### 请求参数

| 名称   | 位置 | 类型   | 必选 | 说明 |
| ------ | ---- | ------ | ---- | ---- |
| taskId | path | string | 是   | none |

> 返回示例

> 200 Response

```json
{
  "script": "string"
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称     | 类型   | 必选 | 约束 | 中文名 | 说明 |
| -------- | ------ | ---- | ---- | ------ | ---- |
| » script | string | true | none |        | none |

## POST save scripts

POST /v1/tasks/{taskId}/scripts

> Body 请求参数

```json
[
{
  "type": "string",
  "order": 0,
  "conditions": [
  {
    "type": "string",
    "order": 0,
    "filePath": "string"
  }
  ],
  "true": [
  {
    "type": "string",
    "order": 0,
    "maxRetryTime": 0,
    "filePath": "string",
    "targetFilePath": "string",
    "createFilePath": true,
    "ignoreHiddenFile": true,
    "transferOption": {}
  }
  ]
}
]
```

### 请求示例

```json
[
{
  "type": "IF",
  "order": 0,
  "conditions": [
  {
    "type": "GET_FILE_STATUS",
    "order": 0,
    "filePath": "/a/mock/path",
    "block": true
  }
  ],
  "true": [
  {
    "type": "SEND_FILE",
    "order": 0,
    "maxRetryTime": 0,
    "filePath": "/a/mock/path",
    "targetFilePath": "/a/mock/path",
    "createFilePath": true,
    "ignoreHiddenFile": true,
    "transferOption": {},
    "block": true,
    "retryTimes": 4,
    "retryInterval": 20,
    "overWrite": "ENUM('OVERWRITE', 'NOT_OVERWRITE', 'COMPARE_OVERWRITE')"
  }
  ],
  "false": [
  {
    "type": "EXECUTE_FILE",
    "order": 3,
    "filePath": "/a/mokc/path",
    "block": true
  }
  ]
}
]
```

### 请求参数

| 名称   | 位置 | 类型          | 必选 | 说明 |
| ------ | ---- | ------------- | ---- | ---- |
| taskId | path | number        | 是   | none |
| body   | body | array[object] | 否   | none |

> 返回示例

> 200 Response

```json
[
  {
    "scriptId": 0,
    "scriptType": "string"
  }
]
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称         | 类型   | 必选 | 约束 | 中文名 | 说明                                                         |
| ------------ | ------ | ---- | ---- | ------ | ------------------------------------------------------------ |
| » scriptId   | number | true | none |        | none                                                         |
| » scriptType | string | true | none |        | enum('SEND_FILE', 'RECV_FILE', 'COPY_FILE', 'DELETE_FILE', 'EXECUTE_FILE', 'WAIT_FLAG_FILE', 'GET_FILE_STATUS', 'IF', 'BROADCAST', 'UPLOAD_TO_SERVER'), 下同 |

## GET Task Jobs

GET /v1/tasks/{taskId}/jobs

### 请求参数

| 名称                    | 位置  | 类型    | 必选 | 说明 |
| ----------------------- | ----- | ------- | ---- | ---- |
| taskId                  | path  | string  | 是   | none |
| jobName                 | query | string  | 否   | none |
| pageNo                  | query | integer | 否   | none |
| pageSize                | query | integer | 否   | none |
| jobNameContain          | query | string  | 否   | none |
| enabled                 | query | string  | 否   | none |
| lastEditedAtGte         | query | number  | 否   | none |
| lastEditedAtLte         | query | number  | 否   | none |
| lastRunAtGte            | query | number  | 否   | none |
| lastRunAtLte            | query | number  | 否   | none |
| assignmentsChangedAtGte | query | number  | 否   | none |
| assignmentsChangedAtLte | query | number  | 否   | none |
| createAtGte             | query | number  | 否   | none |
| createAtLte             | query | number  | 否   | none |

> 返回示例

> 200 Response

```json
{
  "list": [
    {
      "jobId": 0,
      "jobName": "string",
      "targetClientGroup": 0,
      "tasks": 0,
      "jobScheduler": 0,
      "maxRetryTime": 0,
      "maxJobDuration": 0
    }
  ],
  "total": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称                 | 类型     | 必选 | 约束 | 中文名 | 说明 |
| -------------------- | -------- | ---- | ---- | ------ | ---- |
| » list               | [object] | true | none |        | none |
| »» jobId             | number   | true | none |        | none |
| »» jobName           | string   | true | none |        | none |
| »» targetClientGroup | number   | true | none |        | none |
| »» tasks             | integer  | true | none |        | none |
| »» jobScheduler      | number   | true | none |        | none |
| »» maxRetryTime      | integer  | true | none |        | none |
| »» maxJobDuration    | number   | true | none |        | none |
| » total              | integer  | true | none |        | none |

## PUT bind  task job

PUT /v1/tasks/{taskId}/jobs

> Body 请求参数

```json
[
  0
]
```

### 请求参数

| 名称   | 位置 | 类型          | 必选 | 说明 |
| ------ | ---- | ------------- | ---- | ---- |
| taskId | path | number        | 是   | none |
| body   | body | array[number] | 否   | none |

> 返回示例

> 200 Response

```json
null
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | null     |

## GET Group list

GET /v1/groups

### 请求参数

| 名称      | 位置  | 类型    | 必选 | 说明 |
| --------- | ----- | ------- | ---- | ---- |
| groupName | query | string  | 否   | none |
| pageSize  | query | integer | 否   | none |
| pageNo    | query | integer | 否   | none |

> 返回示例

> 200 Response

```json
{
  "total": 0,
  "list": [
    {
      "groupId": 0,
      "groupName": "string",
      "type": 0,
      "lastEditedAt": 0
    }
  ]
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称            | 类型     | 必选 | 约束 | 中文名 | 说明 |
| --------------- | -------- | ---- | ---- | ------ | ---- |
| » total         | number   | true | none |        | none |
| » list          | [object] | true | none |        | none |
| »» groupId      | number   | true | none |        | none |
| »» groupName    | string   | true | none |        | none |
| »» type         | integer  | true | none |        | none |
| »» lastEditedAt | number   | true | none |        | none |

## POST Create Group

POST /v1/groups

> Body 请求参数

```json
{
  "type": 0,
  "groupName": "string",
  "description": "string",
  "enabled": true,
  "queryProperty": "string",
  "queryOperation": "string",
  "queryValue": "string",
  "assignmentsChangedAt": 0,
  "membershipChangedAt": 0,
  "lastRefreshedAt": 0
}
```

### 请求参数

| 名称                   | 位置 | 类型    | 必选 | 说明 |
| ---------------------- | ---- | ------- | ---- | ---- |
| body                   | body | object  | 否   | none |
| » type                 | body | integer | 是   | none |
| » groupName            | body | string  | 是   | none |
| » description          | body | string  | 是   | none |
| » enabled              | body | boolean | 是   | none |
| » queryProperty        | body | string  | 是   | none |
| » queryOperation       | body | string  | 是   | none |
| » queryValue           | body | string  | 是   | none |
| » assignmentsChangedAt | body | number  | 是   | none |
| » membershipChangedAt  | body | number  | 是   | none |
| » lastRefreshedAt      | body | number  | 是   | none |

> 返回示例

> 200 Response

```json
{
  "type": 0,
  "groupName": "string",
  "description": "string",
  "groupId": 0,
  "enabled": true,
  "queryProperty": "string",
  "queryOperation": "string",
  "queryValue": "string",
  "assignmentsChangedAt": 0,
  "membershipChangedAt": 0,
  "lastRefreshedAt": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称                   | 类型    | 必选 | 约束 | 中文名 | 说明 |
| ---------------------- | ------- | ---- | ---- | ------ | ---- |
| » type                 | integer | true | none |        | none |
| » groupName            | string  | true | none |        | none |
| » description          | string  | true | none |        | none |
| » groupId              | number  | true | none |        | none |
| » enabled              | boolean | true | none |        | none |
| » queryProperty        | string  | true | none |        | none |
| » queryOperation       | string  | true | none |        | none |
| » queryValue           | string  | true | none |        | none |
| » assignmentsChangedAt | number  | true | none |        | none |
| » membershipChangedAt  | number  | true | none |        | none |
| » lastRefreshedAt      | number  | true | none |        | none |

## PUT update Group

PUT /v1/groups

> Body 请求参数

```json
{
  "groupId": 0,
  "type": 0,
  "groupName": "string",
  "description": "string",
  "enabled": true,
  "queryProperty": "string",
  "queryOperation": "string",
  "queryValue": "string",
  "assignmentsChangedAt": 0,
  "membershipChangedAt": 0,
  "lastRefreshedAt": 0
}
```

### 请求参数

| 名称                   | 位置 | 类型    | 必选 | 说明 |
| ---------------------- | ---- | ------- | ---- | ---- |
| body                   | body | object  | 否   | none |
| » groupId              | body | number  | 是   | none |
| » type                 | body | integer | 是   | none |
| » groupName            | body | string  | 是   | none |
| » description          | body | string  | 否   | none |
| » enabled              | body | boolean | 否   | none |
| » queryProperty        | body | string  | 否   | none |
| » queryOperation       | body | string  | 否   | none |
| » queryValue           | body | string  | 否   | none |
| » assignmentsChangedAt | body | number  | 否   | none |
| » membershipChangedAt  | body | number  | 否   | none |
| » lastRefreshedAt      | body | number  | 否   | none |

> 返回示例

> 200 Response

```json
{
  "desc": null
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称   | 类型 | 必选 | 约束 | 中文名 | 说明 |
| ------ | ---- | ---- | ---- | ------ | ---- |
| » desc | null | true | none |        | none |

## PUT Maintenence

PUT /v1/config/maintenance

将某一字段的记录与另一字段的记录进行关联操作。 例如将Client记录关联到Job记录上

> Body 请求参数

```json
{
  "optionType": 0,
  "optionIds": [
    0
  ],
  "targetType": 0,
  "targetId": 0,
  "opt": 0
}
```

### 请求参数

| 名称         | 位置 | 类型     | 必选 | 说明                          |
| ------------ | ---- | -------- | ---- | ----------------------------- |
| body         | body | object   | 否   | none                          |
| » optionType | body | number   | 是   | 0:job 1:task 2:group 3:client |
| » optionIds  | body | [number] | 是   | none                          |
| » targetType | body | integer  | 是   | none                          |
| » targetId   | body | number   | 是   | none                          |
| » opt        | body | integer  | 是   | 0:移除 1:添加                 |

> 返回示例

> 200 Response

```json
{
  "optionType": 0,
  "optionIds": [
    0
  ],
  "targetType": 0,
  "targetId": 0,
  "opt": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称         | 类型     | 必选 | 约束 | 中文名 | 说明                          |
| ------------ | -------- | ---- | ---- | ------ | ----------------------------- |
| » optionType | number   | true | none |        | 0:job 1:task 2:group 3:client |
| » optionIds  | [number] | true | none |        | none                          |
| » targetType | integer  | true | none |        | none                          |
| » targetId   | number   | true | none |        | none                          |
| » opt        | integer  | true | none |        | 0:移除 1:添加                 |

## PUT enable job

PUT /v1/jobs/{jobId}/enable

### 请求参数

| 名称  | 位置 | 类型   | 必选 | 说明 |
| ----- | ---- | ------ | ---- | ---- |
| jobId | path | number | 是   | none |

> 返回示例

> 成功

```json
"success"
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | string   |

## PUT disable dob

PUT /v1/jobs/{jobId}/disable

### 请求参数

| 名称  | 位置 | 类型   | 必选 | 说明 |
| ----- | ---- | ------ | ---- | ---- |
| jobId | path | number | 是   | none |

> 返回示例

> 成功

```json
"success"
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | string   |

## DELETE Delete task

DELETE /v1/tasks/{taskId}

### 请求参数

| 名称   | 位置 | 类型   | 必选 | 说明 |
| ------ | ---- | ------ | ---- | ---- |
| taskId | path | number | 是   | none |

> 返回示例

> 成功

```json
"success"
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | string   |

## DELETE Delete job

DELETE /v1/jobs/{jobId}

### 请求参数

| 名称  | 位置 | 类型   | 必选 | 说明 |
| ----- | ---- | ------ | ---- | ---- |
| jobId | path | number | 是   | none |

> 返回示例

> 成功

```json
"success"
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | string   |

## DELETE Delete group

DELETE /v1/groups/{groupId}

### 请求参数

| 名称    | 位置 | 类型   | 必选 | 说明 |
| ------- | ---- | ------ | ---- | ---- |
| groupId | path | number | 是   | none |

> 返回示例

> 成功

```json
"success"
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | string   |

## PUT bind group client

PUT /v1/groups/{groupId}/clients

> Body 请求参数

```json
[
  0
]
```

### 请求参数

| 名称    | 位置 | 类型          | 必选 | 说明 |
| ------- | ---- | ------------- | ---- | ---- |
| groupId | path | number        | 是   | none |
| body    | body | array[number] | 否   | none |

> 返回示例

> 200 Response

```json
null
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | null     |

## GET get gruop clients

GET /v1/groups/{groupId}/clients


### 请求参数

| 名称     | 位置  | 类型    | 必选 | 说明 |
| -------- | ----- | ------- | ---- | ---- |
| groupId  | path  | number  | 是   | none |
| pageSize | query | integer | 否   | none |
| pageNo   | query | integer | 否   | none |

> 返回示例

> 200 Response

```json
{
  "total": 0,
  "list": [
    {
      "clientId": 0,
      "username": "string",
      "enable": true,
      "status": "string",
      "createAt": 0,
      "role": "ENMU('SERVER', 'STORE')"
    }
  ]
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | null     |

## GET Run Job

GET /v1/jobs/{jobId}/run

### 请求参数

| 名称  | 位置 | 类型   | 必选 | 说明 |
| ----- | ---- | ------ | ---- | ---- |
| jobId | path | number | 是   | none |

> 返回示例

> 成功

```json
"success"
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | string   |

## PUT remove job group

PUT /v1/jobs/{jobId}/groups/remove

> Body 请求参数

```json
[
  0
]
```

### 请求参数

| 名称  | 位置 | 类型          | 必选 | 说明 |
| ----- | ---- | ------------- | ---- | ---- |
| jobId | path | number        | 是   | none |
| body  | body | array[number] | 否   | none |

> 返回示例

> 200 Response

```json
null
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | null     |

## PUT remove job task

PUT /v1/jobs/{jobId}/tasks/remove

> Body 请求参数

```json
[
  0
]
```

### 请求参数

| 名称  | 位置 | 类型          | 必选 | 说明 |
| ----- | ---- | ------------- | ---- | ---- |
| jobId | path | number        | 是   | none |
| body  | body | array[number] | 否   | none |

> 返回示例

> 200 Response

```json
null
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | null     |

## PUT remove job clients Copy

PUT /v1/jobs/{jobId}/clients/remove

> Body 请求参数

```json
[
  0
]
```

### 请求参数

| 名称  | 位置 | 类型          | 必选 | 说明 |
| ----- | ---- | ------------- | ---- | ---- |
| jobId | path | number        | 是   | none |
| body  | body | array[number] | 否   | none |

> 返回示例

> 200 Response

```json
null
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | null     |

## GET jobs group count

GET /v1/jobs/{jobId}/groups/count

### 请求参数

| 名称  | 位置 | 类型   | 必选 | 说明 |
| ----- | ---- | ------ | ---- | ---- |
| jobId | path | number | 是   | none |

> 返回示例

> 200 Response

```json
{
  "count": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称    | 类型   | 必选 | 约束 | 中文名 | 说明 |
| ------- | ------ | ---- | ---- | ------ | ---- |
| » count | number | true | none |        | none |

## GET jobs tasks count

GET /v1/jobs/{jobId}/tasks/count

### 请求参数

| 名称  | 位置 | 类型   | 必选 | 说明 |
| ----- | ---- | ------ | ---- | ---- |
| jobId | path | number | 是   | none |

> 返回示例

> 200 Response

```json
{
  "count": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称    | 类型   | 必选 | 约束 | 中文名 | 说明 |
| ------- | ------ | ---- | ---- | ------ | ---- |
| » count | number | true | none |        | none |

## GET jobs clients count

GET /v1/jobs/{jobId}/clients/count

### 请求参数

| 名称  | 位置 | 类型   | 必选 | 说明 |
| ----- | ---- | ------ | ---- | ---- |
| jobId | path | number | 是   | none |

> 返回示例

> 200 Response

```json
{
  "count": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称    | 类型   | 必选 | 约束 | 中文名 | 说明 |
| ------- | ------ | ---- | ---- | ------ | ---- |
| » count | number | true | none |        | none |

## GET task jobs count

GET /v1/tasks/{taskId}/jobs/count

### 请求参数

| 名称   | 位置 | 类型   | 必选 | 说明 |
| ------ | ---- | ------ | ---- | ---- |
| taskId | path | number | 是   | none |

> 返回示例

> 200 Response

```json
{
  "count": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称    | 类型   | 必选 | 约束 | 中文名 | 说明 |
| ------- | ------ | ---- | ---- | ------ | ---- |
| » count | number | true | none |        | none |

## PUT bind client jobs

PUT /v1/clients/{clientsId}/jobs

> Body 请求参数

```json
[
  0
]
```

### 请求参数

| 名称      | 位置 | 类型          | 必选 | 说明 |
| --------- | ---- | ------------- | ---- | ---- |
| clientsId | path | number        | 是   | none |
| body      | body | array[number] | 否   | none |

> 返回示例

> 200 Response

```json
null
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | null     |

## PUT remove client jobs

PUT /v1/clients/{clientsId}/jobs/remove

> Body 请求参数

```json
[
  0
]
```

### 请求参数

| 名称      | 位置 | 类型          | 必选 | 说明 |
| --------- | ---- | ------------- | ---- | ---- |
| clientsId | path | number        | 是   | none |
| body      | body | array[number] | 否   | none |

> 返回示例

> 200 Response

```json
null
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | null     |

## PUT remove task job

PUT /v1/tasks/{taskId}/jobs/remove

> Body 请求参数

```json
[
  0
]
```

### 请求参数

| 名称   | 位置 | 类型          | 必选 | 说明 |
| ------ | ---- | ------------- | ---- | ---- |
| taskId | path | number        | 是   | none |
| body   | body | array[number] | 否   | none |

> 返回示例

> 200 Response

```json
null
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | null     |

## GET jobs count info

GET /v1/jobs/{jobId}/countInfo

### 请求参数

| 名称  | 位置 | 类型   | 必选 | 说明 |
| ----- | ---- | ------ | ---- | ---- |
| jobId | path | number | 是   | none |

> 返回示例

> 200 Response

```json
{
  "groups": 0,
  "tasks": 0,
  "clients": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称      | 类型   | 必选 | 约束 | 中文名 | 说明 |
| --------- | ------ | ---- | ---- | ------ | ---- |
| » groups  | number | true | none |        | none |
| » tasks   | number | true | none |        | none |
| » clients | number | true | none |        | none |

## GET task clients

GET /v1/tasks/{taskId}/clients

### 请求参数

| 名称                | 位置  | 类型          | 必选 | 说明 |
| ------------------- | ----- | ------------- | ---- | ---- |
| taskId              | path  | number        | 是   | none |
| pageNo              | query | integer       | 否   | none |
| pageSize            | query | integer       | 否   | none |
| clientId            | query | number        | 否   | none |
| username            | query | string        | 否   | none |
| usernameContain     | query | string        | 否   | none |
| createAtLte         | query | array[string] | 否   | none |
| mqttClientId        | query | string        | 否   | none |
| mqttClientIdContain | query | string        | 否   | none |
| status              | query | string        | 否   | none |
| enabled             | query | string        | 否   | none |
| connectedAtGte      | query | number        | 否   | none |
| connectedAtLte      | query | number        | 否   | none |
| disconnectedAtGte   | query | number        | 否   | none |
| disconnectedAtLte   | query | number        | 否   | none |
| createAtGte         | query | number        | 否   | none |

> 返回示例

> 200 Response

```json
{
  "total": 0,
  "list": [
    {
      "clientId": 0,
      "username": "string",
      "enable": true,
      "status": "string",
      "createAt": 0
    }
  ]
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称        | 类型     | 必选 | 约束 | 中文名 | 说明 |
| ----------- | -------- | ---- | ---- | ------ | ---- |
| » total     | number   | true | none |        | none |
| » list      | [object] | true | none |        | none |
| »» clientId | number   | true | none |        | none |
| »» username | string   | true | none |        | none |
| »» enable   | boolean  | true | none |        | none |
| »» status   | string   | true | none |        | none |
| »» createAt | number   | true | none |        | none |

## PUT bind client  group

PUT /v1/clients/{clientId}/groups

> Body 请求参数

```json
[
  0
]
```

### 请求参数

| 名称     | 位置 | 类型          | 必选 | 说明 |
| -------- | ---- | ------------- | ---- | ---- |
| clientId | path | number        | 是   | none |
| body     | body | array[number] | 否   | none |

> 返回示例

> 200 Response

```json
null
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | null     |

## PUT bind client group

PUT /v1/clients/{clientsId}/groups

> Body 请求参数

```json
[
  0
]
```

### 请求参数

| 名称      | 位置 | 类型          | 必选 | 说明 |
| --------- | ---- | ------------- | ---- | ---- |
| clientsId | path | number        | 是   | none |
| body      | body | array[number] | 否   | none |

> 返回示例

> 200 Response

```json
null
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | null     |

## GET task count info

GET /v1/tasks/{taskId}/countInfo

### 请求参数

| 名称   | 位置 | 类型   | 必选 | 说明 |
| ------ | ---- | ------ | ---- | ---- |
| taskId | path | number | 是   | none |

> 返回示例

> 200 Response

```json
{}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

## GET job allI info

GET /v1/jobs/allInfo

### 请求参数

| 名称                    | 位置  | 类型    | 必选 | 说明 |
| ----------------------- | ----- | ------- | ---- | ---- |
| jobName                 | query | string  | 否   | none |
| pageNo                  | query | integer | 否   | none |
| pageSize                | query | integer | 否   | none |
| jobNameContain          | query | string  | 否   | none |
| enabled                 | query | string  | 否   | none |
| lastEditedAtGte         | query | number  | 否   | none |
| lastEditedAtLte         | query | number  | 否   | none |
| lastRunAtGte            | query | number  | 否   | none |
| lastRunAtLte            | query | number  | 否   | none |
| assignmentsChangedAtGte | query | number  | 否   | none |
| assignmentsChangedAtLte | query | number  | 否   | none |
| createAtGte             | query | number  | 否   | none |
| createAtLte             | query | number  | 否   | none |

> 返回示例

> 200 Response

```json
{
  "list": [
    {
      "jobId": 0,
      "jobName": "string",
      "tasks": 0,
      "groups": 0,
      "clients": 0,
      "maxRetryTime": 0
    }
  ],
  "total": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称            | 类型     | 必选 | 约束 | 中文名 | 说明 |
| --------------- | -------- | ---- | ---- | ------ | ---- |
| » list          | [object] | true | none |        | none |
| »» jobId        | number   | true | none |        | none |
| »» jobName      | string   | true | none |        | none |
| »» tasks        | integer  | true | none |        | none |
| »» groups       | integer  | true | none |        | none |
| »» clients      | integer  | true | none |        | none |
| »» maxRetryTime | integer  | true | none |        | none |
| » total         | number   | true | none |        | none |

## GET Task List all info

GET /v1/tasks/allInfo

### 请求参数

| 名称                    | 位置  | 类型    | 必选 | 说明 |
| ----------------------- | ----- | ------- | ---- | ---- |
| taskName                | query | string  | 否   | none |
| pageNo                  | query | integer | 否   | none |
| pageSize                | query | integer | 否   | none |
| taskNameContain         | query | string  | 否   | none |
| enabled                 | query | string  | 否   | none |
| lastEditedAtGte         | query | number  | 否   | none |
| lastEditedAtLte         | query | number  | 否   | none |
| lastRunAtGte            | query | number  | 否   | none |
| lastRunAtLte            | query | number  | 否   | none |
| assignmentsChangedAtGte | query | number  | 否   | none |
| assignmentsChangedAtLte | query | number  | 否   | none |
| createAtGte             | query | number  | 否   | none |
| createAtLte             | query | number  | 否   | none |

> 返回示例

> 200 Response

```json
{
  "total": 0,
  "list": [
    {
      "taskId": 0,
      "taskName": "string",
      "enable": true,
      "priority": 0,
      "description": "string",
      "lastEditedAt": 0,
      "lastTimeRun": 0,
      "jobs": 0,
      "clients": 0,
      "scripts": 0
    }
  ]
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称            | 类型     | 必选 | 约束 | 中文名 | 说明 |
| --------------- | -------- | ---- | ---- | ------ | ---- |
| » total         | number   | true | none |        | none |
| » list          | [object] | true | none |        | none |
| »» taskId       | number   | true | none |        | none |
| »» taskName     | string   | true | none |        | none |
| »» enable       | boolean  | true | none |        | none |
| »» priority     | integer  | true | none |        | none |
| »» description  | string   | true | none |        | none |
| »» lastEditedAt | number   | true | none |        | none |
| »» lastTimeRun  | number   | true | none |        | none |
| »» jobs         | integer  | true | none |        | none |
| »» clients      | integer  | true | none |        | none |
| »» scripts      | integer  | true | none |        | none |

## PUT enable task

PUT /v1/tasks/{taskId}/enable

### 请求参数

| 名称   | 位置 | 类型   | 必选 | 说明 |
| ------ | ---- | ------ | ---- | ---- |
| taskId | path | number | 是   | none |

> 返回示例

> 成功

```json
"success"
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | string   |

## PUT disable task

PUT /v1/tasks/{taskId}/disable

### 请求参数

| 名称   | 位置 | 类型   | 必选 | 说明 |
| ------ | ---- | ------ | ---- | ---- |
| taskId | path | number | 是   | none |

> 返回示例

> 成功

```json
"success"
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | string   |

## GET job 日程表

GET /v1/dashboard/scheduledJobs

### 请求参数

| 名称  | 位置  | 类型   | 必选 | 说明 |
| ----- | ----- | ------ | ---- | ---- |
| start | query | number | 是   | none |
| end   | query | number | 是   | none |
| now   | query | number | 是   | none |

> 返回示例

> 200 Response

```json
[
  {
    "jobId": 0,
    "startAt": 0,
    "endAt": 0,
    "result": "string",
    "clients": 0,
    "actualStartAt": 0,
    "actualEndAt": 0
  }
]
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称            | 类型   | 必选 | 约束 | 中文名 | 说明                                             |
| --------------- | ------ | ---- | ---- | ------ | ------------------------------------------------ |
| » jobId         | number | true | none |        | none                                             |
| » startAt       | number | true | none |        | none                                             |
| » endAt         | number | true | none |        | none                                             |
| » result        | string | true | none |        | enum("SUCCESS", "FAILED", "UPCOMING", "RUNNING") |
| » clients       | number | true | none |        | none                                             |
| » actualStartAt | number | true | none |        | none                                             |
| » actualEndAt   | number | true | none |        | none                                             |

# monitoring

## GET Client List

GET /v1/clients

### 请求参数

| 名称                | 位置  | 类型          | 必选 | 说明 |
| ------------------- | ----- | ------------- | ---- | ---- |
| pageNo              | query | integer       | 否   | none |
| pageSize            | query | integer       | 否   | none |
| clientId            | query | number        | 否   | none |
| username            | query | string        | 否   | none |
| usernameContain     | query | string        | 否   | none |
| createAtLte         | query | array[string] | 否   | none |
| mqttClientId        | query | string        | 否   | none |
| mqttClientIdContain | query | string        | 否   | none |
| status              | query | string        | 否   | none |
| enabled             | query | string        | 否   | none |
| connectedAtGte      | query | number        | 否   | none |
| connectedAtLte      | query | number        | 否   | none |
| disconnectedAtGte   | query | number        | 否   | none |
| disconnectedAtLte   | query | number        | 否   | none |
| createAtGte         | query | number        | 否   | none |

> 返回示例

> 200 Response

```json
{
  "total": 0,
  "list": [
    {
      "clientId": 0,
      "username": "string",
      "enable": true,
      "status": "string",
      "createAt": 0,
      "role": "ENMU('SERVER', 'STORE')"
    }
  ]
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称        | 类型     | 必选 | 约束 | 中文名 | 说明                    |
| ----------- | -------- | ---- | ---- | ------ | ----------------------- |
| » total     | number   | true | none |        | none                    |
| » list      | [object] | true | none |        | none                    |
| »» clientId | number   | true | none |        | none                    |
| »» username | string   | true | none |        | none                    |
| »» enable   | boolean  | true | none |        | none                    |
| »» status   | string   | true | none |        | none                    |
| »» role     | string   | true | none |        | ENMU('SERVER', 'STORE') |
| »» createAt | number   | true | none |        | none                    |

## POST create clients

POST /v1/clients

> Body 请求参数

```json
{
  "mqttClientId": "string",
  "username": "string",
  "enable": true,
  "status": "string",
  "connnectedAt": 0,
  "disconnnetedAt": 0,
  "ip": "string",
  "role": "ENMU('SERVER', 'STORE')"
}
```

### 请求参数

| 名称             | 位置 | 类型    | 必选 | 说明                    |
| ---------------- | ---- | ------- | ---- | ----------------------- |
| body             | body | object  | 否   | none                    |
| » mqttClientId   | body | string  | 是   | none                    |
| » ip             | body | string  | 是   | none                    |
| » username       | body | string  | 是   | none                    |
| » enable         | body | boolean | 否   | none                    |
| » status         | body | string  | 否   | none                    |
| » connnectedAt   | body | number  | 否   | none                    |
| » disconnnetedAt | body | number  | 否   | none                    |
| » role           | body | string  | 否   | ENMU('SERVER', 'STORE') |

> 返回示例

> 200 Response

```json
{
  "mqttClientId": "string",
  "username": "string",
  "enable": true,
  "status": "string",
  "connnectedAt": 0,
  "disconnnetedAt": 0,
  "ip": "string",
  "role": "ENMU('SERVER', 'STORE')"
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称             | 位置 | 类型    | 必选 | 说明                    |
| ---------------- | ---- | ------- | ---- | ----------------------- |
| » clientId       | body | number  | 是   | none                    |
| » mqttClientId   | body | string  | 是   | none                    |
| » username       | body | string  | 是   | none                    |
| » enable         | body | boolean | 是   | none                    |
| » status         | body | string  | 是   | none                    |
| » connnectedAt   | body | number  | 是   | none                    |
| » disconnnetedAt | body | number  | 是   | none                    |
| » ip             | body | string  | 是   | none                    |
| » role           | body | string  | 是   | ENMU('SERVER', 'STORE') |

## PUT update clients

PUT /v1/clients

> Body 请求参数

```json
{
  "clientId": 0,
  "mqttClientId": "string",
  "username": "string",
  "enable": true,
  "status": "string",
  "connnectedAt": 0,
  "disconnnetedAt": 0
}
```

### 请求参数

| 名称             | 位置 | 类型    | 必选 | 说明 |
| ---------------- | ---- | ------- | ---- | ---- |
| body             | body | object  | 否   | none |
| » clientId       | body | number  | 是   | none |
| » mqttClientId   | body | string  | 否   | none |
| » username       | body | string  | 否   | none |
| » enable         | body | boolean | 否   | none |
| » status         | body | string  | 否   | none |
| » connnectedAt   | body | number  | 否   | none |
| » disconnnetedAt | body | number  | 否   | none |

> 返回示例

> 200 Response

```json
{
  "desc": null
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称   | 类型 | 必选 | 约束 | 中文名 | 说明 |
| ------ | ---- | ---- | ---- | ------ | ---- |
| » desc | null | true | none |        | none |

## GET Client Attributes

GET /v1/clients/{clientId}/attributes

### 请求参数

| 名称     | 位置  | 类型    | 必选 | 说明 |
| -------- | ----- | ------- | ---- | ---- |
| clientId | path  | string  | 是   | none |
| pageSize | query | integer | 否   | none |
| pageNo   | query | integer | 否   | none |

> 返回示例

> 200 Response

```json
{
  "list": [
    {
      "type": 0,
      "attributeId": 0,
      "attributeName": "string",
      "attributeValue": "string",
      "display": true,
      "readOnly": true
    }
  ],
  "total": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称              | 类型     | 必选 | 约束 | 中文名 | 说明 |
| ----------------- | -------- | ---- | ---- | ------ | ---- |
| » list            | [object] | true | none |        | none |
| »» type           | integer  | true | none |        | none |
| »» attributeId    | number   | true | none |        | none |
| »» attributeName  | string   | true | none |        | none |
| »» attributeValue | string   | true | none |        | none |
| »» display        | boolean  | true | none |        | none |
| »» readOnly       | boolean  | true | none |        | none |
| » total           | number   | true | none |        | none |

## GET Client Groups

GET /v1/clients/{clientId}/groups

### 请求参数

| 名称     | 位置  | 类型    | 必选 | 说明 |
| -------- | ----- | ------- | ---- | ---- |
| clientId | path  | number  | 是   | none |
| pageSize | query | integer | 否   | none |
| pageNo   | query | integer | 否   | none |

> 返回示例

> 200 Response

```json
{
  "list": {
    "groupId": 0,
    "type": 0,
    "lastEditedAt": 0
  },
  "total": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称            | 类型    | 必选 | 约束 | 中文名 | 说明 |
| --------------- | ------- | ---- | ---- | ------ | ---- |
| » list          | object  | true | none |        | none |
| »» groupId      | number  | true | none |        | none |
| »» type         | integer | true | none |        | none |
| »» lastEditedAt | number  | true | none |        | none |
| » total         | number  | true | none |        | none |

## GET Client Jobs

GET /v1/clients/{clientId}/jobs

### 请求参数

| 名称                    | 位置  | 类型    | 必选 | 说明 |
| ----------------------- | ----- | ------- | ---- | ---- |
| clientId                | path  | number  | 是   | none |
| jobName                 | query | string  | 否   | none |
| pageNo                  | query | integer | 否   | none |
| pageSize                | query | integer | 否   | none |
| jobNameContain          | query | string  | 否   | none |
| enabled                 | query | string  | 否   | none |
| lastEditedAtGte         | query | number  | 否   | none |
| lastEditedAtLte         | query | number  | 否   | none |
| lastRunAtGte            | query | number  | 否   | none |
| lastRunAtLte            | query | number  | 否   | none |
| assignmentsChangedAtGte | query | number  | 否   | none |
| assignmentsChangedAtLte | query | number  | 否   | none |
| createAtGte             | query | number  | 否   | none |
| createAtLte             | query | number  | 否   | none |

> 返回示例

> 200 Response

```json
{
  "list": {
    "jobId": 0,
    "jobName": "string",
    "targetClientGroup": 0,
    "tasks": 0,
    "jobScheduler": 0,
    "maxRetryTime": 0,
    "maxJobDuration": 0
  },
  "total": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称                 | 类型    | 必选 | 约束 | 中文名 | 说明 |
| -------------------- | ------- | ---- | ---- | ------ | ---- |
| » list               | object  | true | none |        | none |
| »» jobId             | number  | true | none |        | none |
| »» jobName           | string  | true | none |        | none |
| »» targetClientGroup | number  | true | none |        | none |
| »» tasks             | integer | true | none |        | none |
| »» jobScheduler      | number  | true | none |        | none |
| »» maxRetryTime      | integer | true | none |        | none |
| »» maxJobDuration    | number  | true | none |        | none |
| » total              | integer | true | none |        | none |

## DELETE Delete Client

DELETE /v1/clients/{clientId}

### 请求参数

| 名称     | 位置 | 类型   | 必选 | 说明 |
| -------- | ---- | ------ | ---- | ---- |
| clientId | path | number | 是   | none |

> 返回示例

> 200 Response

```json
{
  "clientId": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称       | 类型   | 必选 | 约束 | 中文名 | 说明 |
| ---------- | ------ | ---- | ---- | ------ | ---- |
| » clientId | number | true | none |        | none |

## GET Task history

GET /v1/tasks/histories

### 请求参数

| 名称         | 位置  | 类型    | 必选 | 说明 |
| ------------ | ----- | ------- | ---- | ---- |
| pageSize     | query | integer | 否   | none |
| pageNo       | query | integer | 否   | none |
| mqttClientId | query | string  | 否   | none |
| taskName     | query | string  | 否   | none |

> 返回示例

> 200 Response

```json
{
  "list": [
    {
      "mqttClientId": "string",
      "taskName": "string",
      "enabled": 0,
      "taskScript": "string",
      "priority": 0,
      "ts": 0,
      "result": "string"
    }
  ],
  "total": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称            | 类型     | 必选 | 约束 | 中文名 | 说明 |
| --------------- | -------- | ---- | ---- | ------ | ---- |
| » list          | [object] | true | none |        | none |
| »» mqttClientId | string   | true | none |        | none |
| »» taskName     | string   | true | none |        | none |
| »» enabled      | integer  | true | none |        | none |
| »» taskScript   | string   | true | none |        | none |
| »» priority     | integer  | true | none |        | none |
| »» ts           | number   | true | none |        | none |
| »» result       | string   | true | none |        | none |
| » total         | number   | true | none |        | none |

## GET client attributes count

GET /v1/clients/{clientId}/attributes/count

### 请求参数

| 名称     | 位置 | 类型   | 必选 | 说明 |
| -------- | ---- | ------ | ---- | ---- |
| clientId | path | number | 是   | none |

> 返回示例

> 200 Response

```json
{
  "count": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称    | 类型   | 必选 | 约束 | 中文名 | 说明 |
| ------- | ------ | ---- | ---- | ------ | ---- |
| » count | number | true | none |        | none |

## GET client groups count

GET /v1/clients/{clientId}/groups/count

### 请求参数

| 名称     | 位置 | 类型   | 必选 | 说明 |
| -------- | ---- | ------ | ---- | ---- |
| clientId | path | number | 是   | none |

> 返回示例

> 200 Response

```json
{
  "count": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称    | 类型   | 必选 | 约束 | 中文名 | 说明 |
| ------- | ------ | ---- | ---- | ------ | ---- |
| » count | number | true | none |        | none |

## GET client jobs count

GET /v1/clients/{clientId}/jobs/count

### 请求参数

| 名称     | 位置 | 类型   | 必选 | 说明 |
| -------- | ---- | ------ | ---- | ---- |
| clientId | path | number | 是   | none |

> 返回示例

> 200 Response

```json
{
  "count": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称    | 类型   | 必选 | 约束 | 中文名 | 说明 |
| ------- | ------ | ---- | ---- | ------ | ---- |
| » count | number | true | none |        | none |

## GET Client tasks

GET /v1/clients/{clientId}/tasks

### 请求参数

| 名称                    | 位置  | 类型    | 必选 | 说明 |
| ----------------------- | ----- | ------- | ---- | ---- |
| clientId                | path  | number  | 是   | none |
| taskName                | query | string  | 否   | none |
| pageNo                  | query | integer | 否   | none |
| pageSize                | query | integer | 否   | none |
| taskNameContain         | query | string  | 否   | none |
| enabled                 | query | string  | 否   | none |
| lastEditedAtGte         | query | number  | 否   | none |
| lastEditedAtLte         | query | number  | 否   | none |
| lastRunAtGte            | query | number  | 否   | none |
| lastRunAtLte            | query | string  | 否   | none |
| assignmentsChangedAtGte | query | number  | 否   | none |
| assignmentsChangedAtLte | query | number  | 否   | none |
| createAtGte             | query | number  | 否   | none |
| createAtLte             | query | number  | 否   | none |

> 返回示例

> 200 Response

```json
{
  "list": {
    "jobId": 0,
    "jobName": "string",
    "targetClientGroup": 0,
    "tasks": 0,
    "jobScheduler": 0,
    "maxRetryTime": 0,
    "maxJobDuration": 0
  },
  "total": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称                 | 类型    | 必选 | 约束 | 中文名 | 说明 |
| -------------------- | ------- | ---- | ---- | ------ | ---- |
| » list               | object  | true | none |        | none |
| »» jobId             | number  | true | none |        | none |
| »» jobName           | string  | true | none |        | none |
| »» targetClientGroup | number  | true | none |        | none |
| »» tasks             | integer | true | none |        | none |
| »» jobScheduler      | number  | true | none |        | none |
| »» maxRetryTime      | integer | true | none |        | none |
| »» maxJobDuration    | number  | true | none |        | none |
| » total              | integer | true | none |        | none |

## GET clients detail

GET /v1/clients/{clientId}/details

### 请求参数

| 名称     | 位置 | 类型   | 必选 | 说明 |
| -------- | ---- | ------ | ---- | ---- |
| clientId | path | number | 是   | none |

> 返回示例

> 200 Response

```json
{
  "clientId": 0,
  "username": "string",
  "enable": true,
  "status": "string",
  "connectedAt": 0,
  "disconnectedAt": 0,
  "createAt": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称             | 类型    | 必选 | 约束 | 中文名 | 说明 |
| ---------------- | ------- | ---- | ---- | ------ | ---- |
| » clientId       | number  | true | none |        | none |
| » username       | string  | true | none |        | none |
| » enable         | boolean | true | none |        | none |
| » status         | string  | true | none |        | none |
| » connectedAt    | number  | true | none |        | none |
| » disconnectedAt | number  | true | none |        | none |
| » createAt       | number  | true | none |        | none |

## GET client count info

GET /v1/clients/{clientId}/countInfo

### 请求参数

| 名称     | 位置 | 类型   | 必选 | 说明 |
| -------- | ---- | ------ | ---- | ---- |
| clientId | path | number | 是   | none |

> 返回示例

> 200 Response

```json
{
  "attributes": 0,
  "jobs": 0,
  "tasks": 0,
  "group": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称         | 类型   | 必选 | 约束 | 中文名 | 说明 |
| ------------ | ------ | ---- | ---- | ------ | ---- |
| » attributes | number | true | none |        | none |
| » jobs       | number | true | none |        | none |
| » tasks      | number | true | none |        | none |
| » group      | number | true | none |        | none |

## GET Client List all info

GET /v1/clients/allInfo

### 请求参数

| 名称                | 位置  | 类型          | 必选 | 说明 |
| ------------------- | ----- | ------------- | ---- | ---- |
| pageNo              | query | integer       | 否   | none |
| pageSize            | query | integer       | 否   | none |
| clientId            | query | number        | 否   | none |
| username            | query | string        | 否   | none |
| usernameContain     | query | string        | 否   | none |
| createAtLte         | query | array[string] | 否   | none |
| mqttClientId        | query | string        | 否   | none |
| mqttClientIdContain | query | string        | 否   | none |
| status              | query | string        | 否   | none |
| enabled             | query | string        | 否   | none |
| connectedAtGte      | query | number        | 否   | none |
| connectedAtLte      | query | number        | 否   | none |
| disconnectedAtGte   | query | number        | 否   | none |
| disconnectedAtLte   | query | number        | 否   | none |
| createAtGte         | query | number        | 否   | none |

> 返回示例

> 200 Response

```json
{
  "total": 0,
  "list": [
    {
      "clientId": 0,
      "username": "string",
      "enable": true,
      "status": "string",
      "role": "ENMU('SERVER', 'STORE')",
      "createAt": 0,
      "groups": 0,
      "jobs": 0,
      "tasks": 0
    }
  ]
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称        | 类型     | 必选 | 约束 | 中文名 | 说明                    |
| ----------- | -------- | ---- | ---- | ------ | ----------------------- |
| » total     | number   | true | none |        | none                    |
| » list      | [object] | true | none |        | none                    |
| »» clientId | number   | true | none |        | none                    |
| »» username | string   | true | none |        | none                    |
| »» enable   | boolean  | true | none |        | none                    |
| »» role     | string   | true | none |        | ENMU('SERVER', 'STORE') |
| »» status   | string   | true | none |        | none                    |
| »» createAt | number   | true | none |        | none                    |
| »» groups   | number   | true | none |        | none                    |
| »» jobs     | number   | true | none |        | none                    |
| »» tasks    | integer  | true | none |        | none                    |

## PUT enable client

PUT /v1/clients/{clientId}/enable

### 请求参数

| 名称     | 位置 | 类型   | 必选 | 说明 |
| -------- | ---- | ------ | ---- | ---- |
| clientId | path | number | 是   | none |

> 返回示例

> 200 Response

```json
{
  "desc": null
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称   | 类型 | 必选 | 约束 | 中文名 | 说明 |
| ------ | ---- | ---- | ---- | ------ | ---- |
| » desc | null | true | none |        | none |

## PUT disable client

PUT /v1/clients/{clientId}/disable

### 请求参数

| 名称     | 位置 | 类型   | 必选 | 说明 |
| -------- | ---- | ------ | ---- | ---- |
| clientId | path | number | 是   | none |

> 返回示例

> 200 Response

```json
{
  "desc": null
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称   | 类型 | 必选 | 约束 | 中文名 | 说明 |
| ------ | ---- | ---- | ---- | ------ | ---- |
| » desc | null | true | none |        | none |

# settings

## POST Add Client Attributes

POST /v1/clients/{clientId}/attributes

> Body 请求参数

```json
[
  {
    "clientId": 0,
    "attributeId": 0,
    "attributeValue": "string"
  }
]
```

### 请求参数

| 名称     | 位置 | 类型          | 必选 | 说明 |
| -------- | ---- | ------------- | ---- | ---- |
| clientId | path | number        | 是   | none |
| body     | body | array[object] | 否   | none |

> 返回示例

> 200 Response

```json
{
  "desc": null
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称   | 类型 | 必选 | 约束 | 中文名 | 说明 |
| ------ | ---- | ---- | ---- | ------ | ---- |
| » desc | null | true | none |        | none |

## POST General Settings

POST /v1/settings

> Body 请求参数

```json
{
  "managementServerTimeZone": "string",
  "communicationServerTimeZone": "string",
  "region": "string",
  "adminTimeOut": 0
}
```

### 请求参数

| 名称                          | 位置 | 类型   | 必选 | 说明 |
| ----------------------------- | ---- | ------ | ---- | ---- |
| body                          | body | object | 否   | none |
| » managementServerTimeZone    | body | string | 是   | none |
| » communicationServerTimeZone | body | string | 是   | none |
| » region                      | body | string | 是   | none |
| » adminTimeOut                | body | number | 是   | none |

> 返回示例

> 200 Response

```json
{
  "managementServerTimeZone": "string",
  "communicationServerTimeZone": "string",
  "region": "string",
  "adminTimeOut": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称                          | 类型   | 必选 | 约束 | 中文名 | 说明 |
| ----------------------------- | ------ | ---- | ---- | ------ | ---- |
| » managementServerTimeZone    | string | true | none |        | none |
| » communicationServerTimeZone | string | true | none |        | none |
| » region                      | string | true | none |        | none |
| » adminTimeOut                | number | true | none |        | none |

## GET General Settings

GET /v1/settings

> 返回示例

> 200 Response

```json
{
  "managementServerTimeZone": "string",
  "communicationServerTimeZone": "string",
  "region": "string",
  "adminTimeOut": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称                          | 类型   | 必选 | 约束 | 中文名 | 说明 |
| ----------------------------- | ------ | ---- | ---- | ------ | ---- |
| » managementServerTimeZone    | string | true | none |        | none |
| » communicationServerTimeZone | string | true | none |        | none |
| » region                      | string | true | none |        | none |
| » adminTimeOut                | number | true | none |        | none |

## GET Job Settings

GET /v1/jobs/settings

> 返回示例

> 200 Response

```json
{
  "enable": true,
  "maxRetried": 0,
  "retryWait": 0,
  "maxConcurrentSession": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称                   | 类型    | 必选 | 约束 | 中文名 | 说明 |
| ---------------------- | ------- | ---- | ---- | ------ | ---- |
| » enable               | boolean | true | none |        | none |
| » maxRetried           | integer | true | none |        | none |
| » retryWait            | integer | true | none |        | none |
| » maxConcurrentSession | integer | true | none |        | none |

## POST Job Settings

POST /v1/jobs/settings

> Body 请求参数

```json
{
  "enable": true,
  "maxRetried": 0,
  "retryWait": 0,
  "maxConcurrentSession": 0
}
```

### 请求参数

| 名称                   | 位置 | 类型    | 必选 | 说明 |
| ---------------------- | ---- | ------- | ---- | ---- |
| body                   | body | object  | 否   | none |
| » enable               | body | boolean | 是   | none |
| » maxRetried           | body | integer | 是   | none |
| » retryWait            | body | integer | 是   | none |
| » maxConcurrentSession | body | integer | 是   | none |

> 返回示例

> 200 Response

```json
{
  "enable": true,
  "maxRetried": 0,
  "retryWait": 0,
  "maxConcurrentSession": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称                   | 类型    | 必选 | 约束 | 中文名 | 说明 |
| ---------------------- | ------- | ---- | ---- | ------ | ---- |
| » enable               | boolean | true | none |        | none |
| » maxRetried           | integer | true | none |        | none |
| » retryWait            | integer | true | none |        | none |
| » maxConcurrentSession | integer | true | none |        | none |

## GET Task Settings

GET /v1/tasks/settings

> 返回示例

> 200 Response

```json
{
  "enable": true,
  "priority": 0,
  "disableValidation": true,
  "jobsSettingId": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称                | 类型    | 必选 | 约束 | 中文名 | 说明 |
| ------------------- | ------- | ---- | ---- | ------ | ---- |
| » enable            | boolean | true | none |        | none |
| » priority          | integer | true | none |        | none |
| » disableValidation | boolean | true | none |        | none |
| » jobsSettingId     | number  | true | none |        | none |

## POST Task Settings

POST /v1/tasks/settings

> Body 请求参数

```json
{
  "enable": true,
  "priority": 0,
  "disableValidation": true
}
```

### 请求参数

| 名称                | 位置 | 类型    | 必选 | 说明 |
| ------------------- | ---- | ------- | ---- | ---- |
| body                | body | object  | 否   | none |
| » enable            | body | boolean | 是   | none |
| » priority          | body | integer | 是   | none |
| » disableValidation | body | boolean | 是   | none |

> 返回示例

> 200 Response

```json
{
  "enable": true,
  "priority": 0,
  "disableValidation": true,
  "tasksSettingId": "string"
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称                | 类型    | 必选 | 约束 | 中文名 | 说明 |
| ------------------- | ------- | ---- | ---- | ------ | ---- |
| » enable            | boolean | true | none |        | none |
| » priority          | integer | true | none |        | none |
| » disableValidation | boolean | true | none |        | none |
| » tasksSettingId    | string  | true | none |        | none |

## GET Clients Settings

GET /v1/clients/settings

> 返回示例

> 200 Response

```json
{
  "clientSettingsId": 0,
  "autoEnableNewClient": true
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称                  | 类型    | 必选 | 约束 | 中文名 | 说明 |
| --------------------- | ------- | ---- | ---- | ------ | ---- |
| » clientSettingsId    | number  | true | none |        | none |
| » autoEnableNewClient | boolean | true | none |        | none |

## POST Client Settings

POST /v1/clients/settings

> Body 请求参数

```json
{
  "autoEnableNewClient": true
}
```

### 请求参数

| 名称                  | 位置 | 类型    | 必选 | 说明 |
| --------------------- | ---- | ------- | ---- | ---- |
| body                  | body | object  | 否   | none |
| » autoEnableNewClient | body | boolean | 是   | none |

> 返回示例

> 200 Response

```json
{
  "clientSettingsId": 0,
  "autoEnableNewClient": true
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称                  | 类型    | 必选 | 约束 | 中文名 | 说明 |
| --------------------- | ------- | ---- | ---- | ------ | ---- |
| » clientSettingsId    | number  | true | none |        | none |
| » autoEnableNewClient | boolean | true | none |        | none |

## GET Attributes List

GET /v1/settings/attributes

### 请求参数

| 名称     | 位置  | 类型   | 必选 | 说明 |
| -------- | ----- | ------ | ---- | ---- |
| pageSize | query | number | 否   | none |
| pageNo   | query | number | 否   | none |

> 返回示例

> 200 Response

```json
{
  "list": [
    {
      "attributeName": "string",
      "attributeId": 0,
      "type": "string",
      "defaultValue": "string",
      "display": true,
      "readOnly": true
    }
    ],
    "total": 0
  }
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称             | 类型     | 必选 | 约束 | 中文名 | 说明 |
| ---------------- | -------- | ---- | ---- | ------ | ---- |
| » list           | [object] | true | none |        | none |
| »» attributeName | string   | true | none |        | none |
| »» attributeId   | number   | true | none |        | none |
| »» type          | string   | true | none |        | none |
| »» defaultValue  | string   | true | none |        | none |
| »» display       | boolean  | true | none |        | none |
| »» readOnly      | boolean  | true | none |        | none |
| » total          | number   | true | none |        | none |

## POST Add attributes

POST /v1/settings/attributes

> Body 请求参数

```json
{
  "attributeName": "string",
  "type": 0,
  "defaultValue": "string",
  "display": true,
  "readOnly": true
}
```

### 请求参数

| 名称            | 位置 | 类型    | 必选 | 说明 |
| --------------- | ---- | ------- | ---- | ---- |
| body            | body | object  | 否   | none |
| » attributeName | body | string  | 是   | none |
| » type          | body | integer | 是   | none |
| » defaultValue  | body | string  | 是   | none |
| » display       | body | boolean | 是   | none |
| » readOnly      | body | boolean | 是   | none |

> 返回示例

> 200 Response

```json
{
  "attributeName": "string",
  "attributesId": 0,
  "type": 0,
  "defaultValue": "string",
  "display": 0,
  "readOnly": 0
}
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | Inline   |

### 返回数据结构

状态码 **200**

| 名称            | 类型    | 必选 | 约束 | 中文名 | 说明 |
| --------------- | ------- | ---- | ---- | ------ | ---- |
| » attributeName | string  | true | none |        | none |
| » attributesId  | number  | true | none |        | none |
| » type          | integer | true | none |        | none |
| » defaultValue  | string  | true | none |        | none |
| » display       | integer | true | none |        | none |
| » readOnly      | integer | true | none |        | none |

## DELETE Delete Attributes

DELETE /v1/settings/attributes/{attributeId}

### 请求参数

| 名称        | 位置 | 类型   | 必选 | 说明 |
| ----------- | ---- | ------ | ---- | ---- |
| attributeId | path | string | 是   | none |

> 返回示例

> 成功

```json
"success"
```

### 返回结果

| 状态码 | 状态码含义                                              | 说明 | 数据模型 |
| ------ | ------------------------------------------------------- | ---- | -------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | 成功 | string   |

# 数据模型

