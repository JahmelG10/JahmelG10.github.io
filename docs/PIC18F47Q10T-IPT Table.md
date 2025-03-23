---
title: API
---
# HMI Subsystem API — Jahmel

This document defines the message structures used by the Human-Machine Interface (HMI) subsystem in our system architecture. It outlines both incoming and outgoing messages, conforming to the team-wide 64-byte protocol.

Each message includes:
- 2-byte prefix (`0x41`, `0x5a`)
- 1-byte source ID
- 1-byte destination ID
- 1-byte message type
- Message-specific data
- Padding (`0x00`) up to byte 62
- 2-byte suffix (`0x59`, `0x42`)

---

## Subsystem Address Table

| Subsystem     | ID | Address |
|---------------|----|---------|
| WiFi (Cade)   | 1  | `0x01`  |
| HMI (Jahmel)  | 2  | `0x02`  |
| Temp Sensor   | 3  | `0x03`  |
| Fan Controller| 4  | `0x04`  |
| Broadcast     | 88 | `0x58`  |


---
## Messages Received by HMI

---

### Temperature Reading (Message Type: `0x10`)
The HMI receives temperature data from the Temperature Sensor.

| Byte      | Variable Name       | Variable Type | Min Value | Max Value | Example Value |
|-----------|----------------------|----------------|------------|------------|----------------|
| 1         | prefix_1             | `uint8_t`      | 0x41       | 0x41       | 0x41           |
| 2         | prefix_2             | `uint8_t`      | 0x5a       | 0x5a       | 0x5a           |
| 3         | source_id            | `uint8_t`      | 3          | 3          | 0x03           |
| 4         | destination_id       | `uint8_t`      | 2          | 2          | 0x02           |
| 5         | message_type         | `uint8_t`      | 0x10       | 0x10       | 0x10           |
| 6         | temp_id              | `uint8_t`      | 1          | 255        | 0x01           |
| 7         | status               | `uint8_t`      | 0          | 1          | 0x00           |
| 8         | temp_data_integer    | `int8_t`       | -40        | 155        | 23             |
| 9         | temp_data_fraction   | `uint8_t`      | 0          | 99         | 50             |
| 10–62     | unused               | `uint8_t`      | 0x00       | 0x00       | 0x00           |
| 63        | suffix_1             | `uint8_t`      | 0x59       | 0x59       | 0x59           |
| 64        | suffix_2             | `uint8_t`      | 0x42       | 0x42       | 0x42           |

---

### Fan System Status (Message Type: `0x30`)
The HMI receives status updates from the Fan Controller.

| Byte      | Variable Name      | Variable Type | Min Value | Max Value | Example Value |
|-----------|---------------------|----------------|------------|------------|----------------|
| 1         | prefix_1            | `uint8_t`      | 0x41       | 0x41       | 0x41           |
| 2         | prefix_2            | `uint8_t`      | 0x5a       | 0x5a       | 0x5a           |
| 3         | source_id           | `uint8_t`      | 4          | 4          | 0x04           |
| 4         | destination_id      | `uint8_t`      | 2          | 2          | 0x02           |
| 5         | message_type        | `uint8_t`      | 0x30       | 0x30       | 0x30           |
| 6         | fan_id              | `uint8_t`      | 1          | 255        | 0x02           |
| 7         | status              | `uint8_t`      | 0          | 1          | 0x00           |
| 8         | fan_status_code     | `uint8_t`      | 0x00       | 0x01       | 0x00           |
| 9–62      | unused              | `uint8_t`      | 0x00       | 0x00       | 0x00           |
| 63        | suffix_1            | `uint8_t`      | 0x59       | 0x59       | 0x59           |
| 64        | suffix_2            | `uint8_t`      | 0x42       | 0x42       | 0x42           |

---

## Messages Sent by HMI

---

### Set Fan Speed (Message Type: `0x20`)
The HMI sends a command to the Fan Controller to adjust motor speed.

| Byte      | Variable Name      | Variable Type | Min Value | Max Value | Example Value |
|-----------|---------------------|----------------|------------|------------|----------------|
| 1         | prefix_1            | `uint8_t`      | 0x41       | 0x41       | 0x41           |
| 2         | prefix_2            | `uint8_t`      | 0x5a       | 0x5a       | 0x5a           |
| 3         | source_id           | `uint8_t`      | 2          | 2          | 0x02           |
| 4         | destination_id      | `uint8_t`      | 4          | 4          | 0x04           |
| 5         | message_type        | `uint8_t`      | 0x20       | 0x20       | 0x20           |
| 6         | fan_id              | `uint8_t`      | 1          | 255        | 0x02           |
| 7         | status              | `uint8_t`      | 0          | 1          | 0x01           |
| 8         | fan_speed_set       | `uint8_t`      | 0          | 125        | 85             |
| 9–62      | unused              | `uint8_t`      | 0x00       | 0x00       | 0x00           |
| 63        | suffix_1            | `uint8_t`      | 0x59       | 0x59       | 0x59           |
| 64        | suffix_2            | `uint8_t`      | 0x42       | 0x42       | 0x42           |

---

### Send Event Log to WiFi (Message Type: `0x31`)
The HMI logs user/system actions to the WiFi Module for storage.

| Byte      | Variable Name     | Variable Type | Min Value | Max Value | Example Value |
|-----------|--------------------|----------------|------------|------------|----------------|
| 1         | prefix_1           | `uint8_t`      | 0x41       | 0x41       | 0x41           |
| 2         | prefix_2           | `uint8_t`      | 0x5a       | 0x5a       | 0x5a           |
| 3         | source_id          | `uint8_t`      | 2          | 2          | 0x02           |
| 4         | destination_id     | `uint8_t`      | 1          | 1          | 0x01           |
| 5         | message_type       | `uint8_t`      | 0x31       | 0x31       | 0x31           |
| 6         | event_type         | `uint8_t`      | 0          | 10         | 1 (fan change) |
| 7         | event_value        | `uint8_t`      | 0          | 255        | 85             |
| 8–62      | unused             | `uint8_t`      | 0x00       | 0x00       | 0x00           |
| 63        | suffix_1           | `uint8_t`      | 0x59       | 0x59       | 0x59           |
| 64        | suffix_2           | `uint8_t`      | 0x42       | 0x42       | 0x42           |

---




## Notes

- All messages follow a 64-byte format with fixed prefix/suffix values.
- Message types are unique to each action.
- HMI must acknowledge valid messages and discard malformed or irrelevant ones.
- Confirm use of message type `0x31` with Cade for WiFi storage.

