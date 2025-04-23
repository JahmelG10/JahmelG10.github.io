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

[wednesday_1.txt](https://github.com/user-attachments/files/19861195/wednesday_1.txt)#include "mcc_generated_files/system/system.h"
 <pre><code>
#define MSG_PREFIX_1     0x41
#define MSG_PREFIX_2     0x5A
#define MSG_SUFFIX_1     0x59
#define MSG_SUFFIX_2     0x42
#define MSG_TOTAL_LEN    64

#define ID_WIFI           0x01
#define ID_HMI            0x02
#define ID_FAN_CONTROL    0x03
#define ID_TEMP_SENSOR    0x03
#define ID_BROADCAST      0x58

#define MSG_TYPE_FAN_CTRL  0x20
#define MSG_TYPE_TEMP_DATA 0x10

static uint8_t msg_buffer[MSG_TOTAL_LEN];
static uint8_t msg_index = 0;
static bool msg_receiving = false;

volatile uint8_t fan_speed = 0;

void BlinkLED(uint8_t times)
{
    for (uint8_t i = 0; i < times; i++)
    {
        IO_RC5_SetHigh();
        __delay_ms(100);
        IO_RC5_SetLow();
        __delay_ms(100);
    }
}

void SendFanSpeedBroadcast(uint8_t speed)
{
    uint8_t msg[64] = {0};

    msg[0] = MSG_PREFIX_1;
    msg[1] = MSG_PREFIX_2;
    msg[2] = ID_HMI;
    msg[3] = ID_BROADCAST;
    msg[4] = MSG_TYPE_FAN_CTRL;
    msg[5] = 0x02;  // fan_id
    msg[6] = 0x01;  // status
    msg[7] = speed; // fan_speed_data
    msg[8] = speed; // fan_speed_set
    msg[62] = MSG_SUFFIX_1;
    msg[63] = MSG_SUFFIX_2;

    for (uint8_t i = 0; i < 64; i++)
    {
        while (!EUSART1_IsTxReady());
        EUSART1_Write(msg[i]);
    }
}

void CheckButtonAndBroadcast(void)
{
    static bool prev_state = true;
    bool current_state = IO_RC2_GetValue();

    if (prev_state == true && current_state == false)
    {
        fan_speed++;
        if (fan_speed > 3) fan_speed = 1;
        SendFanSpeedBroadcast(fan_speed);
    }

    prev_state = current_state;
}

void ForwardMessage(uint8_t* buffer)
{
    for (uint8_t i = 0; i < MSG_TOTAL_LEN; i++)
    {
        while (!EUSART1_IsTxReady());
        EUSART1_Write(buffer[i]);
    }
}

void HandleFullMessage(uint8_t* buffer)
{
    if (buffer[0] != MSG_PREFIX_1 || buffer[1] != MSG_PREFIX_2 ||
        buffer[62] != MSG_SUFFIX_1 || buffer[63] != MSG_SUFFIX_2)
        return;

    uint8_t src_id = buffer[2];
    uint8_t dest_id = buffer[3];
    uint8_t msg_type = buffer[4];

    if (src_id != ID_WIFI && src_id != ID_HMI &&
        src_id != ID_FAN_CONTROL && src_id != ID_BROADCAST &&
        src_id != ID_TEMP_SENSOR)
        return;

    // Forward messages not meant for HMI or broadcast
    if (dest_id != ID_HMI && dest_id != ID_BROADCAST)
    {
        ForwardMessage(buffer);
        return;
    }

    switch (src_id)
    {
        case ID_WIFI:        BlinkLED(1); break;
        case ID_HMI:         BlinkLED(2); break;
        case ID_FAN_CONTROL: BlinkLED(3); break;
        case ID_BROADCAST:   BlinkLED(4); break;
    }

    if (msg_type == MSG_TYPE_TEMP_DATA && src_id == ID_TEMP_SENSOR)
    {
        uint8_t status = buffer[6];
        uint8_t raw_temp = buffer[7];
        uint8_t temp_frac = buffer[8];

        if (status == 1)
        {
            int8_t corrected_temp = (int8_t)raw_temp - 40;
            float temperature = corrected_temp + (temp_frac / 100.0f);

            if (corrected_temp < 0)
                BlinkLED(2);
            else
                BlinkLED(1);
        }
    }
}

void UART_MessageParser(void)
{
    if (EUSART1_IsRxReady())
    {
        uint8_t byte = EUSART1_Read();

        if (!msg_receiving)
        {
            if (byte == MSG_PREFIX_1)
            {
                msg_buffer[0] = byte;
                msg_index = 1;
                msg_receiving = true;
            }
        }
        else
        {
            msg_buffer[msg_index++] = byte;

            if (msg_index == MSG_TOTAL_LEN)
            {
                HandleFullMessage(msg_buffer);
                msg_receiving = false;
                msg_index = 0;
            }
        }
    }
}

void main(void)
{
    SYSTEM_Initialize();
    INTERRUPT_GlobalInterruptEnable();
    INTERRUPT_PeripheralInterruptEnable();

    while (1)
    {
        UART_MessageParser();
        CheckButtonAndBroadcast();
    }
}
 </code></pre> 

