# Agent Data Flow - Broadcast: Upload

## Scenes

The server generates files, such as marketing campaign files and script BAT files, and sends them to stores. Upload files to EMQX in advance as file cache

## Job Control

parameter

| Name | Info |
| - | - |
| job_id | Job unique identifier |
| task_id | Task unique identifier |
| script_id | Script unique identifier |
| request_id | Request ID for transferring files, unique during interaction |
| path | file source path |
| target_path | target path |
| groups | broadcast address, that is, store group id |

When the server agent reaches the job execution time (according to the execution_time field in the job information, crontab type), it starts to initiate an execution broadcast request to EMQX.

## Initiate Broadcast

via MQTT message
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

## Response Broadcast

Topic

```text
$file_sniffer/v1/broadcast/${clientid}
```

</br>
QoS 1
</br>
Payload

After initiating the request, the server returns to the client according to the MaxCurrentSession limit of the current job (that is, the maximum amount of parallelism).

| Name | Value | Info |
| - | - | - |
| ack | ok | executable |
| ack | WAIT | Maximum execution limit reached, waiting |
| ack | ERROR | The server is abnormal, or the Agent does not have relevant permissions |
| timeout | Integer() | How long to wait when the maximum limit is reached |
| topic | String() | Topic used for file transfer, allocated by the server to ensure unique file channel |

```json
{
     "ack" : "ok | WAIT | ERROR",
     "topic": "$file/${trans topic suffix}"
}
```

## File Transfer - Upload

Use the Topic in the Broadcast response

Topic

```text
$file/${trans topic suffix}
```

QoS 1
</br>
Payload
Use nftp file transfer protocol (version 1.0), protocol details refer to nftp chapter

```text
file content encode by nftp
```