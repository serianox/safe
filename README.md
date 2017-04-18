# Safe
### Notation
Numbers in base 2, 8 and 16 are prefixed with `0b`, `0o` and `0x` respectively.
### Endianess
All data is stored using big-endian.
## Data Encoding
### Types
This specification uses the following types to encode data:
- `uint1`
  an 8 bits unsigned number
- `uint2`
  an 16 bits unsigned number
- `uint4`
  an 32 bits unsigned number
- `uint8`
  an 64 bits unsigned number
- `uint16`
  an 128 bits unsigned number
- `vuint`
  a variable-length unsigned number
### Variable Unsigned Integer
_Variable Unsigned Integer_ or `vuint` is a compact encoding for unsigned numbers.

A `vuint` is composed of a power of 2 number of bytes, where the first byte holds the number of bytes composing the `vuint`. The first byte leading bits set to 1 count is the $log_2$ of the length in byte of the `vuint`. The remaining bits in the `vuint` are the base 2 encoding of the unsigned integer. A `vuint` always use the most compact encoding.

For instance, the number 127 is encoded in base 2 as `0b01111111`. The corresponding `vuint` encoding is `0x7f`.

Another example, the number 16383 is encoded in base 2 as `0b11111111111111`. It will require two bytes to encode it. The corresponding `vuint` encoding is `0xbfff`

Finally, the number 16384 is encoded in base 2 as `0b100000000000000`. It will require 4 bytes to encode it. The corresponding `vuint` encoding is `0xc0004000`.
### Structures
## Safe Structures
### Archive Header
```
archive_header
    magic : uint4
    major_version : uint1
    minor_versintion : uint1
```
- `magic`
   the magic value `0x53414645`
- `major_version`
   The major version of this specification used to encode the file.
- `minor_version`
   The minor version of this specification used to encode the file.
### File Header
```
file_header
    header_size : vuint
    header_checksum : 
    compressed_size : vuint
    uncompressed_size : vuint
    name_length : vuint
    name : uint1[name_length]
    data_checksum : 
    data : uint1[compressed_size]
```