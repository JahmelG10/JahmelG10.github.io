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
- 1 to 2-bytes Message-specific data
- Padding (`0x00`) up to byte 62
- 2-byte suffix (`0x59`, `0x42`)

---

## Message ID

The Message ID table defines the unique identifiers for system members and their associated addresses. Each member is assigned a specific ID and address for communication within the system.

| Member        | System            | ID  | Address |
|---------------|-------------------|-----|---------|
| Cade Clonts   | Wifi              | 1   | 0x01    |
| Jahmel        | Human Interface   | 2   | 0x02    |
| Dan           | Fan Control       | 3   | 0x03    |
| Broadcast     | All               | 88  | 0x58    |

### Status

The Status table defines the status codes used in the system to indicate the state of a message or operation.

| Status | Code  |
|--------|-------|
| Normal | 0x00  |
| Error  | 0x01  |

## Message Types

The Message Types table categorizes the types of messages and their associated status or code ranges.

| Category         | Status/Code | Address |
|------------------|-------------|----|
| Temp Data        | 0 to 255  | 0x10 |
| Fan Control      | 0 to 3    | 0x20 |

---

### Temperature Sensor (Message Type 1)

The Temperature Sensor table defines the structure of messages for temperature data. Each byte in the message is mapped to a specific variable, with details about its type, range, and example values.

| Byte | Variable Name | Variable Type | Min Value | Max Value | Example Value |
|---|------------------|--------------|-----------|-----------|--------------|
| 1 | prefix_1        | uint8_t      | 0x41      | 0x41      | 0x41         |
| 2 | prefix_2        | uint8_t      | 0x5a      | 0x5a      | 0x5a         |
| 3 | source_id       | uint8_t      | 1         | 3         | 0x03         |
| 4 | destination_id  | uint8_t      | 1         | 3 & 88    | 0x58         |
| 5 | message_type    | uint8_t      | 0x10      | 0x10      | 0x10         |
| 6 | temp_id         | uint8_t      | 0         | 255       | 0x01         |
| 7 | status          | uint8_t      | 0         | 1         | 0x01         |
| 8 | temp_data_integer | uint8_t    | 0         | 255       | 25           |
| 9 | temp_data_fraction | uint8_t   | 0         | 99        | 50           |
| 10-62 | Unused       | uint8_t     | 0x00       | 0x00     | 0x00         |
| 63 | suffix_1        | uint8_t      | 0x59      | 0x59      | 0x59         |
| 64 | suffix_2        | uint8_t      | 0x42      | 0x42      | 0x42         |


### Fan Control (Message Type 2)

The Fan Control table defines the structure of messages for controlling fan speed. Each byte in the message is mapped to a specific variable, with details about its type, range, and example values.

| Byte  | Variable Name   | Variable Type | Min Value | Max Value | Example Value |
|-------|-----------------|--------------|-----------|-----------|--------------|
| 1     | prefix_1        | uint8_t      | 0x41      | 0x41      | 0x41         |
| 2     | prefix_2        | uint8_t      | 0x5a      | 0x5a      | 0x5a         |
| 3     | source_id       | uint8_t      | 1         | 3         | 0x01         |
| 4     | destination_id  | uint8_t      | 1         | 3 & 88    | 0x03         |
| 5     | message_type    | uint8_t      | 0x20      | 0x20      | 0x20         |
| 6     | fan_id          | uint8_t      | 0         | 1         | 0x01         |
| 7     | status          | uint8_t      | 0         | 1         | 0x01         |
| 8     | fan_speed_data  | uint8_t      | 0         | 3         | 0x02         |
| 9     | fan_speed_set   | uint8_t      | 0         | 3         | 0x01         |
| 10-62 | Unused          | uint8_t      | 0x00      | 0x00      | 0x00         |
| 63    | suffix_1        | uint8_t      | 0x59      | 0x59      | 0x59         |
| 64    | suffix_2        | uint8_t      | 0x42      | 0x42      | 0x42         |




### Message Type Matrix

- S = Sending Message
- R = Recieving Message

| Message Type               | Message ID | Cade<br>Role: MQTT<br>ID: 0x01                     | Dan<br>Role: Motor<br>ID: 0x03                      | Jahmel<br>Role: HMI<br>ID: 0x02                             |
|----------------------------|------------|---------------------------------------------------|----------------------------------------------------|-------------------------------------------------------------|
| sensor value               | 0x10       | S<br>(Temperature Value in °C)                   | R<br>(motor turns on to cool system)               | R<br>(Debug LEDs on/off within value ranges)                |
| Set Motor Speed            | 0x20       | S<br>(Publish 1, 2, or 3)                        | R<br>(Set 1 = Low, 2 = Medium, 3 = High)           | S<br>(toggle debug button press 1, 2, 3)                    |
| Motor Speed Status/Speed  | 0x20       | R<br>(Upload 1, 2, 3)                            | S<br>(Broadcast status/speed)                      | R<br>(Debug LED blinks to recognize message)                |

