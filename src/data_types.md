# Data Types

## Basic Data Types
### bool
A single byte respresenting a boolean (true/false) value. Allowed values are `0` (hex value: `0x00`) or `1` (hex value: `0x01`).

### int16
A sequence of 2 bytes in [little-endian byte order](https://en.wikipedia.org/wiki/Endianness) representing a signed 16-bit integer.
<div class="warning">Datatype will be renamed to i16</div>

### int32
A sequence of 4 bytes in [little-endian byte order](https://en.wikipedia.org/wiki/Endianness) representing a signed 32-bit integer.
<div class="warning">Datatype will be renamed to i32</div>

### float32
A sequence of 4 bytes in [little-endian byte order](https://en.wikipedia.org/wiki/Endianness) representing a 32-bit floating-point number in [IEEE 754 standard](https://en.wikipedia.org/wiki/IEEE_754).
<div class="warning">Datatype will be renamed to f32</div>

### string
A sequence of bytes representing a string in the following format:
* The first 4 bytes store the length, or the number of characters, of the string as [int32](#int32). Note that these 4 bytes do not count towards the length.
* The remaining bytes store the string.
<div class="warning">Datatype will be renamed to str</div>

## Composite Data Types
### vector3f
| Length | Data Type           | Meaning                                  |
| ------ | ------------------- | -------------------------------------    |
|      4 | [float32](#float32) | The \\(x\\) coordinate of the 3D vector. |
|      4 | [float32](#float32) | The \\(y\\) coordinate of the 3D vector. |
|      4 | [float32](#float32) | The \\(z\\) coordinate of the 3D vector. |
<div class="warning">Datatype will be renamed to f32vec3</div>

### vector4f
| Length | Data Type           | Meaning                                  |
| ------ | ------------------- | ---------------------------------------- |
|      4 | [float32](#float32) | The \\(x\\) coordinate of the 4D vector. |
|      4 | [float32](#float32) | The \\(y\\) coordinate of the 4D vector. |
|      4 | [float32](#float32) | The \\(z\\) coordinate of the 4D vector. |
|      4 | [float32](#float32) | The \\(w\\) coordinate of the 4D vector. |
<div class="warning">Datatype will be renamed to f32vec4</div>

## Data Point Types
### boolDataPoint
| Length   | Data Type           | Meaning                              |
|----------|---------------------|--------------------------------------|
|        4 | [float32](#float32) | At what time (in beats) this data point occurs. For [boolDataPoint](#boolDataPoint), the allowed values for time \\(t\\) are: \\(t \in \mathbb{Z} \vert 0 \leq t < total number of beats\\) |
|        1 | [bool](#bool)       | ON/OFF state. 0 = OFF; 1 = ON. |
| variable | [string](#string)   | What interpolation method is applied on this data point with its neighboring data points. See [Interpolation Trait](trait_values.md#interpolation) for a list of allowed values. For boolDataPoint, this is meaningless. |
| variable | [string](#string)   | What easing method is applied on this data point with its neighboring data points. See [Easing Trait](trait_values.md#easing) for a list of allowed values. For boolDataPoint, this is meaningless. |

### float32DataPoint
| Length | Data Type           | Meaning                              |
|--------|---------------------|--------------------------------------|
|      4 | [float32](#float32) | At what time (in beats) this data point occurs. For [float32DataPoint](#float32DataPoint), the allowed values for time depend on the context. |
|      4 | [float32](#float32) | The floating-point value this data point holds. The specific meaning of this value depends on the context. |
| variable | [string](#string) | What interpolation method is applied on this data point with its neighboring data points. See [Interpolation Trait](trait_values.md#interpolation) for a list of allowed values.  |
| variable | [string](#string) | What easing method is applied on this data point with its neighboring data points. See [Easing Trait](trait_values.md#easing) for a list of allowed values.  |