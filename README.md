# QuadMeUp_Crossbow
Cheap DIY RC link based on LoRa 868MHz modules

# Protocol

| Byte | Description | Notes |
| ---- | ---- | ---- |
| 0    | Preamble | "Q" 0x51 |
| 1    | Frame type & Payload Length | bits 7-5 defines frame type, bits 4-0 payload length |
| 2    | Packet ID | |
| 4 - 36 | Payload | 32 bytes max |
| payload length + 3 | CRC | XOR of all previous bytes |

## Frame types

| Value | Description | Direction |
| ----  | ----        | ---- |
| 000   | RC channels data `RC_DATA` | TX -> RX |
| 001   | Receiver health and basic telemetry `RX_HEALTH` | RX -> TX |
| 010   | Request receiver configuration | TX -> RX |
| 011   | Receiver configuration | RX -> TX |
| 100   | Set receiver configuration | TX -> RX |

### `RC_DATA` frame format

Protocol allows to send 11 RC channels in total encoded as following

* channels 1 to 6 encoded using 10 bits each
* channels 7 to 11 encoded using 4 bits per channel

Total length of `RC_DATA` payload is 10 bytes

### `RX_HEALTH` frame format

| Byte | Description |
| ---- | ---- |
| 0    | RX RSSI |
| 1    | RX supply volatage, sent in 0,1V |
| 2    | RX analog input 1 sent in 0,1V |
| 3    | RX analog input 2 sent in 0,1V |
