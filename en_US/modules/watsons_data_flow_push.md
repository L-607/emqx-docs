# Agent Data Flow - Push: push

## Scenes

The server generates files, such as marketing campaign files and script BAT files, and sends them to stores.

EMQX pushes the uploaded cache to the store.

## Job Control

The push behavior is not controlled by the store, but only by the job of the initiator (Server). The store should accept the file immediately after receiving the push instruction

## store monitoring

Topic

```text
$file_sniffer/v1/push/${clientid}
```

Qos 1
</br>
The file push command will be sent to the Agent through the message of this topic, and the business information of the pushed file will be sent to the Agent

## Initiate Push

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

## Response to Push

After the Agent receives the Push message, it immediately subscribes to the topic specified in the message

```text
$file/${PUSH topic suffix}
```

After the subscription is completed, respond to the server

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

## File Transfer - Download

Use the Topic in the Push message

Topic

```text
$file/${PUSH topic suffix}
```

QoS 1
</br>
Payload
Use nftp file transfer protocol (version 1.0), protocol details refer to nftp chapter

```text
file content encode by nftp
```