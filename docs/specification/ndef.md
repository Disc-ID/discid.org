---
title: NDEF Reference
description: General NDEF reference material related to the Disc ID Specification
---


# NFC Data Exchange Format (NDEF) Reference

## NDEF Flags and Fields 

### Flags and TNF
These are stored within the first byte of the Record:

| Abbr | Name             | Details |
|------|------------------|---------|
| MB   | Message Begin    | If 1, this is the first Record in the NDEF message; there can only be one MB Record in a NDEF Message. |
| ME   | Message End      | If 1, this is the last Record in the NDEF Message; there can only be one ME Record in a NDEF Message. |
| CF   | Chunk Flag       | If 1, this record and next Record have chunk relationship; if 0, not chunk relationship. |
| SR   | Short Record     | If 1, the payload length included in this Record is between 0-255 octets (bytes). |
| IL   | ID Length        | If 1, this record includes Payload ID Length and Payload ID; if 0, it does not include these. |
| TNF  | Type Name Format | consists of 3 bits to cover 7 types; for the Disc ID Specification type 1 (`001`) and type 4 (`100`) are used |

**Lengths**

| Name           | Details | Used in Spec |
|----------------|---------|--------------|
| Type Length    | An unsigned 8-bit integer that specifies the length in octets of the Type field below | Yes |
| Payload Length | An unsigned integer that specifies the length in octets of the Payload field below, the size of which is determined by the SR flag: SR flag set = a single octet representing an 8-bit unsigned integer; SR flag not set = four octets representing a 32-bit unsigned integer. Transmission order of the octets is MSB-first. | Yes |
| ID Length      | An unsigned 8-bit integer that specifies the length in octets of the ID field below | No |

**Fields**

| Name    | Details | Used in Spec |
|---------|---------|--------------|
| Type    | An identifier describing the type of the payload | Yes |
| Payload | The data payload that conforms to the payload Type indicated | Yes |
| ID      | A unique ID for the payload | No |

## NDEF Record Layouts

### Short Record
This record layout saves memory space when the payload length is 255 octets (bytes) or shorter.

This is recommended for use whenever possible, but definitely when including the [Record 1: NFC Forum Well-Known Type - URI](disc-id.md#record-1-nfc-forum-well-known-type-uri) due to the limited size of a URL.

![NDEF Short Record Layout](/images/NDEF_Short_Record_Layout.png){ style="min-width: 100px; max-height: 400px;"}

### Long Record
This record layout is used when the payload length is over 255 octets (bytes).

![NDEF Record Layout](/images/NDEF_Record_Layout.png){ style="min-width: 100px; max-height: 500px;"}

## URI Identifier Codes
The following URI Identifier Codes can be used to replace the URI Header in the Payload of a Well-Known Type URI Record, such as in [Record 1: NFC Forum Well-Known Type - URI](/specification/disc-id.md#record-1-nfc-forum-well-known-type-uri)

| URI Identifier Code (UIC) | Content        |
|---------------------------|----------------|
| `0x00`                    | N/A            |
| `0x01`                    | `http://www.`  |
| `0x02`                    | `https://www.` |
| `0x03`                    | `http://`      |
| `0x04`                    | `https://`     |

## Links

[NFC Data Exchange Format (NDEF) Technical Specification 1.0](https://github.com/haldean/ndef/blob/master/docs/NFCForum-TS-NDEF_1.0.pdf)

[NFC Record Type Definition (RTD) Technical Specification 1.0](https://github.com/haldean/ndef/blob/master/docs/NFCForum-TS-RTD_1.0.pdf)

[URI Record Type Definition Technical Specification 1.0](https://github.com/haldean/ndef/blob/master/docs/NFCForum-TS-RTD_URI_1.0.pdf)