---
title: Specification
description: Proposed specifications for the Disc ID standard
---

# Disc ID Specification

!!! example "Documentation Status: Draft"
	The documentation below is currently in a draft form. No formal version has been published. As such, it is not recommended to produce any disc tags using this specification or build any software based on it.

The following specifications are proposed as a standard for describing the origin details of a disc golf disc to allow for easier interoperability of digital systems across the industry.

## Data Format
The [NFC Forum's Data Exchange Format (NDEF)](https://learn.gototags.com/nfc/ndef){ target=_blank } specifies a common data format for NFC Forum-compliant devices and NFC Forum-compliant tags. The current proposal is to use this standard to define one or two NDEF Records to be added to the tags, the entirety of the records together is considered a NDEF Message.

When a NFC tag reader connects with a tag, the whole NDEF Message is passed from the tag to the reader and can then be processed based on detals in the Record(s) header and payload.

Given the potential cost savings when minimizing the memory required on the tag, the following proposal provides guidance on two different NDEF Record Layouts (short and long) depending on the required memory.

!!! note "Implementation support for Record layouts and counts"
	Implementations of the Disc ID standard should support both the reading and writing of Long and Short Record Layouts to allow for maximum data effiency in different scenarios.

	Additionally, with the URL record below being optional, they should also support reading and writing a NDEF Message with a single NDEF Record (just the disc details in Record 2) or both the NDEF Records outlined below.

## Record 1: NFC Forum Well-Known Type - URI
*Optional, but recommended if memory on tag allows*

This record contains a URL which should point to an internet page with details about what Disc ID is, a link to download apps that implement the standard so the NDEF Record with the disc data can be accessed, and other details, perhaps disc-specific.

Although this record is optional, by including this as the first of the NDEF Records, mobile devices with background NFC scanning will automatically pick it up as the primary action and trigger a popup or something similar without the need to open a NFC scanning app ([example details for iOS](https://developer.apple.com/documentation/corenfc/adding_support_for_background_tag_reading){ target=_blank }). This may be a valuable feature for helping discover the Disc ID standard by those who aren't already familiar.

### Record Notes

- This must be the first Record to enable the background scanning capabilities and thus must have the Message Being (MB) flag bit set to `1`
- Because the other Record is required, this must have the Message End (ME) flag bit set to `0`
- The length of the URL in this Record should be minimized so it can utilize the [Short Record Layout](ndef.md#ndef-short-record-layout) option

See [NDEF Reference](ndef.md) for further details on the NDEF flags and fields outlined below.

### NDEF Flags and TNF byte

Example:

| Bit 7   | Bit 6   | Bit 5   | Bit 4   | Bit 3   | Bits 2-0  |
|---------|---------|---------|---------|---------|-----------|
|  MB     | ME      | CF      | SR      | IL      | TNF       |
| `1`     | `0`     | `0`     | `1`     | `0`     | `001`     |

- TNF bits correspond to NFC Forum Well-Known Types (hex `0x01`)
- If payload is over 255 bytes, set SR to `0` and follow the [NDEF Long Record Layout](ndef.md#ndef-long-record-layout)

### NDEF Fields

| Name           | Value                                                       |
|----------------|-------------------------------------------------------------|
| Type Length    | `1`                                                         |
| Payload Length | length of URL payload in bytes                     |
| Type           | `U`                                                         |
| Payload        | URL with [URI identifer code](ndef.md#uri-identifier-codes) |

- Type corresponds with NFC Forum Well-Known Type URI, `urn:nfc:wkt:U`
- Note that because Payload IDs are not being used, the ID Length and ID fields are not included

## Record 2: NFC Forum External Type with disc data
*Required*

This record will contain the data related to the disc.

!!! discussion "Encoding disc data within the payload of a NDEF Record"
	More discussion on how the disc data is to be stored is being discussed can be found in this thread: https://github.com/orgs/Disc-ID/discussions/2

### Record Notes

- If this is the only record on the tag, both the Message Begin (MB) and Message End (ME) flag bits must be set to `1`
- Ideally another [Short Record Layout](ndef.md#ndef-short-record-layout) would be used here

See [NDEF Reference](ndef.md) for further details on the NDEF flags and fields outlined below.

### NDEF Flags and TNF byte
Example:

| Bit 7   | Bit 6   | Bit 5   | Bit 4   | Bit 3   | Bits 2-0  |
|---------|---------|---------|---------|---------|-----------|
|  MB     | ME      | CF      | SR      | IL      | TNF       |
| `0`     | `1`     | `0`     | `1`     | `0`     | `100`     |

- TNF bits correspond to NFC Forum External Types (hex `0x04`)
- If no URL Record is included so this is the only record in the NDEF Message, then MB flag must be set to `1`
- If payload is over 255 bytes, set SR to `0` and follow the [NDEF Long Record Layout](ndef.md#ndef-long-record-layout)


### NDEF Fields

| Name           | Value                      |
|----------------|----------------------------|
| Type Length    | `15`                       |
| Payload Length | length of payload in bytes |
| Type           | `discid.org:disc`          |
| Payload        | TBD                        |

- Type is a custom value derived from the domain name of the Disc ID site and identified `disc` to signify object type
- See [Encoding disc data within the payload of a NDEF Record Discussion thread]() for further details on potential payload encoding
- Note that because Payload IDs are not being used, the ID Length and ID fields are not included

### Disc Data Fields
The following details are being proposed as fields to include about a disc in the Payload of the required NDEF record. The description of the fields is noted next to each field name below along with the format under consideration.

??? info "Notable missing fields"
	The following fields were considered for inclusion in the first draft of the specification but ultimately not added. The reasons for not including them are noted below for reference:

	- Disc type: this was a list of common types of discs to help provide a category for easily grouping them such as putters, midranges, fairway drivers, control drivers and distance drivers. This was not included as it is a bit of a subjective decision and can easily be deduced from other details about the disc, especially flight numbers.

#### Fields Summary
This summary table contains some size and other details for the fields

| Field Name                            | Presence | Type     | Length Type | Min Size  | Range/Format/Notes      | Alt Size  |
|---------------------------------------|----------|----------|-------------|-----------|-------------------------|-----------|
| [Version](#version)                   | Required | Integer  | Fixed       | 8 bits    | 0-255                   | 24 bits   |
| [Disc ID](#disc-id)                   | Required | String   | Fixed       | 64 bits   | ASCII?                  | 64 bits   |
| [Signature](#signature)               | Required | String   | TBD         | TBD       | TBD                     | TBD       |
| [Manufacture Date](#manufacture-date) | Required | Integer  | Fixed       | 32 bits   | up to `42941231`        | 64 bits   |
| [Manufacturer](#manufacturer)         | Required | String   | Fixed       | 24 bits   | 46,656 values           | 24 bits   |
| [Model Name](#model-name)             | Required | String   | Variable    | Variable  | Likely 36 bytes or less | Variable  |
| [Quality](#quality)                   | Required | Integer  | Fixed       | 4 bits    | 0-15                    | 8 bits    |
| [Plastic](#plastic)                   | Required | String   | Variable    | Variable  | Likely 24 bytes or less | Variable  |
| [Weight](#weight)                     | Required | Integer  | Fixed       | 8 bits    | 0-255                   | 24 bits   |
| [Run](#run)                           | Required | Integer  | Fixed       | 24 bits   | 0-16,777,216            | 64 bits   |
| [Flight](#flight)                     | Required | Integers | Fixed       | 18 bits   | See [Flight](#flight)   | 48 bits   |
| [Color](#color)                       | Required | String   | Variable    | Variable  | Likely 16 bytes or less | Variable  |
| **Totals**                            |          |          |             | 182+ bits |                         | 320+ bits |

- Alt Size is the size if using 1 byte characters instead of optimizing around integers

#### Version
Version of the Disc ID specification the data in this tag adheres to.

*Format:* 3 bit integer, 0-255 range

#### Disc ID
Read-only unique ID for the tag (not written by tag manufacturer, added by whoever writes the data noted here to the tag).

*Format:* 64-bits, 8 ASCII characters

#### Signature
A [digital signature](https://en.wikipedia.org/wiki/Digital_signature) produced by the entity writing to the tag which uses a standard set of the Disc Data Field as the input message to generate the signature. By preventing this signature from being accessed outside of physically scanning the tag, it can be used during online transactions to provide a higher level of validation of the disc being bought/sold/traded.

*Format:* TBD

#### Manufacture Date
The date the disc was manufactured.

*Format:* 32 bit integer for an ISO 8601 format of date only without dashes is being considered, e.g. `20231104` or `20230401`

#### Manufacturer
The manufacturer of the disc.

*Format:* 24 bits, 3 ASCII characters mapped to the full Manufacturer name. See [Manufacturers data map](data-maps.md#manufacturers).

#### Model Name
The model of the disc. If [PDGA Approved](https://www.pdga.com/technical-standards/equipment-certification/discs){ target=_blank }, the model name here should be kept similar to the name submitted for PDGA Approval.

*Format:* Variable length string of ASCII characters

#### Quality
The quality of the manufactured disc as defined by the manufacturer. Used to denote retail quality vs. imperfect discs such as misprints and seconds.

*Format:* 4 bit integer, see [Quality data map](data-maps.md#quality).

#### Plastic
The name of the plastic used in the disc as defined by the manufacturer.

*Format:* Variable string of ASCII characters

#### Weight
The measured weight of the disc by the manufacturer in grams.

*Format:* 8 bit integer, 0-255 range

#### Run
The name of the specific manufacturing run the disc was produced during, as defined by the manufacturer.

*Format:* Variable string of ASCII characters

#### Flight
The flight numbers based on the [Flight Ratings System](https://www.innovadiscs.com/home/disc-golf-faq/flight-ratings-system/){ target=_blank } popularized by Innova Discs, including Speed (1-14+), Glide (1 to 7+), Turn (-5 to 1+) and Fade (0-5+).

*Format*: 18 bits split into one integer for each characteristic/indicator as noted below:

| Characteristic | Size   | Range                      |
|----------------|--------|----------------------------|
| Speed          | 4 bits | 0 to 15                    |
| Glide          | 4 bits | 0 to 15                    |
| Turn indicator | 1 bit  | 0 = positive, 1 = negative |
| Turn           | 3 bits | -7 to 7                    |
| Fade           | 4 bits | 0 to 15                    |

#### Color
The name of the color plastic used to manufacture the disc, as defined by the manufacturer.

*Format:* Variable string of ASCII characters

!!! info "Inclusion of the Color field"
	Color is being considered for the specification due to the different flight characteristics found between different colors of the same mold/plastic/run and how much value this can provide to players and collectors. If this is included in the payload the signature is based on, it can be used in validating the accuracy of the details in online transactions.

---


## NFC Tag Requirements
Any tag setup to contain NDEF records with enough memory for the payload should be acceptable, however it is recommended to stay within tags following the ISO 14443 or ISO 15693 standards.


## Security considerations

### Cloning Tags
Data on NFC tags can be cloned to a new tag, including any unique ID added by the manufacturer or others. This is more of an issue with tags that stick onto a disc, since when a tag is embedded, you would need to make a clone of that tag onto another disc that has a blank, unlocked embedded tag and where the disc characteristics are similar enough to avoid detection (color, weight, plastic, etc.). Since creating such similar discs is economically intensive, the concerns of cloning with embedded tags is low.