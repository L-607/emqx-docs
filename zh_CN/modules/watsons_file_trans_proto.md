# 文件传输协议

## Type of Packet

| Type   | Value (Hex) | Description                                    | Direction          |
| ------ | ----------- | ---------------------------------------------- | ------------------ |
| HELLO  | 0x01        | Always the first packet of Transferring.       | Sender -> Receiver |
| ACK    | 0x02        | An acknowledge of HELLO packet.                | Receiver -> Sender |
| FILE   | 0x03        | The FILE packet contains the contents of file. | Sender -> Receiver |
| END    | 0x04        | The last packet contain contents of file.      | Sender -> Receiver |
| GIVEME | 0x05        | Ask a packet with certain ID.                  | Receiver -> Sender |

## Transform detail

```text
+--------+         +----------+
| Sender |         | Receiver |
+--------+         +----------+
     |                   |
     |     HELLO         |
     |------------------>|
     |                   |
     |     ACK           |
     |<------------------|
     |                   |
     |     FILE Block 1  |
     |------------------>|
     |     FILE Block 2  |
     |------------------>|
     |     FILE Block 3  |
     |------------------>|
     |     FILE Block n  |
     |------------------>|
     |                   |
     |     END           |
     |------------------>|
     |                   |
```

## Lost Some File Blocks

```text
+--------+         +----------+
| Sender |         | Receiver |
+--------+         +----------+
     |                   |
     |     GIVEME [2,3]  |
     |<------------------|
     |                   |
     |     FILE Block 2  |
     |------------------>|
     |     FILE Block 3  |
     |------------------>|
     |                   |
     |     END           |
     |------------------>|
     |                   |
```

### HELLO

The HELLO packet is the first packet of transferring for one file.

| **Name**        | **Length(Byte)** | **Description**          |
| --------------- | ---------------- | ------------------------ |
| Type            | 1                | HELLO                    |
| Length          | 4                | Total packet length      |
| Packet Id       | 1                | Packet Id                |
| Blocks          | 2                | File blocks total number |
| FileName Length | 2                | FileName Length          |
| FileName        | FileName Length  | FileName                 |
| File CRC        | 4                | Crc32                    |

### ACK

The ACK packet is a acknowledge of HELLO packet.

| **Name**  | **Length(Byte)** | **Description**     |
| --------- | ---------------- | ------------------- |
| Type      | 1                | ACK                 |
| Length    | 4                | Total packet length |
| Packet Id | 1                | Packet Id           |
| File Id   | 4                | File Id             |

### FILE

The FILE packet contains the contents of file. And a block contained in one Packet. The size of block is define in nftp.h ((256 * 1024) Default).

| **Name**       | **Length(Byte)** | **Description**            |
| -------------- | ---------------- | -------------------------- |
| Type           | 1                | FILE                       |
| Length         | 4                | Total packet length        |
| File Id        | 4                | File Id                    |
| Block Seq      | 2                | Block Seq, starting from 0 |
| Content Length | 2                | Content Length             |
| Content        | Content Length   | File block content         |

### END

The END Packet is the last packet contain contents of file. It means the ending of transferring for a file.

| **Name**       | **Length(Byte)** | **Description**            |
| -------------- | ---------------- | -------------------------- |
| Type           | 1                | END                        |
| Length         | 4                | Total packet length        |
| File id        | 4                | File id                    |
| Block Seq      | 2                | Block Seq, starting from 0 |
| Content Length | 2                | Content Length             |
| Content        | Content Length   | File block content         |

### GIVEME

| **Name**        | **Length(Byte)** | **Description**     |
| --------------- | ---------------- | ------------------- |
| Type            | 1                | GIVEME              |
| Length          | 4                | Total packet length |
| Packet Id       | 1                | Packet Id           |
| Need Block Seqs | 2                | [1,3,5,7,8]         |
