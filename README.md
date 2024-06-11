# eo-captured-packets

JSON representations of Endless Online protocol packets.

## Capture method

Packets were captured using a [proxy](https://www.github.com/ethanmoffat/eopcap) designed to dump decoded packet data alongside a representation of the [EO protocol](https://www.github.com/cirras/eo-protocol). The client used was the last officially available version of Endless online v28. The server software used was the official GameServer software running on a Windows XP VM.

## How to use this repository

This repository is intended for use by authors of Endless Online library implementations based on the aforementioned [EO protocol](https://www.github.com/cirras/eo-protocol). As library implementations generally rely on generated code to create structures and packets, this data can be used to assert that the generated structures properly serialize/deserialize the binary packet data.

Consumers are recommended to add this repository as a submodule, and either generate test code based on the data contained within them, or parse them in tests at runtime and use reflection to assert the values in the listed properties.

Some translation of property types and names to library types and names is expected depending on the consuming language and library implementation.

## JSON structure

The JSON models contain the following four top-level properties:

1. Packet Family 
2. Packet Action
3. Expected binary data (decoded)
   - This data omits the protocol information, including length bytes, packet id, and sequence numbers.
4. Child properties in the protocol object.

    Each property object contains:
   1. The property's type. Type is omitted for array entries with primitive types.
   2. The property's name. Name is omitted for array entries.
   3. The property's value. Value is omitted for arrays with an element type other than 'byte'.
      - For byte arrays, the byte data is a base64-encoded string.
   4. A list of child items. Child items are included for arrays and structures.
      - Each child item represents either an array entry or a structure properties.
