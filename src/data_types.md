# Data Types

<div class="warning">
These data types are deprecated and will be replaced by [revised data types](#revised_types).
</div>

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

## Revised Types

## Basic Types
The byte order for basic types will always be assumed to be in [little-endian byte order](https://en.wikipedia.org/wiki/Endianness), unless mentioned otherwise.

### s8
A signed 8-bit integer.

### u8
An unsigned 8-bit integer.

### s16
A signed 16-bit integer.

### u16
An unsigned 16-bit integer.

### s32
A signed 32-bit integer.

### u32
An unsigned 32-bit integer.

### f32
A 32-bit [IEEE 754](https://en.wikipedia.org/wiki/IEEE_754) floating point value.

## Arrays and Structs
Arrays will be represented as `type[size]`, where type is the data type and size is how many of those types are in an array. Arrays are tightly packed.

Structures are composite types made of basic type and arrays. These will be tightly packed with no padding between fields.

### str
A simple string representation with a size and the bytes of the string. No null termination bytes are used.

| Type            | Meaning              |
| --------------- | -------------------- |
| `u32      size` | length of the string |
| `u8[size] data` | bytes of the string  |

### f32vec2
An array of 2 `f32`. Typically used to represent texture coordinates in meshes.

* The first offset is commonly aliased as `x`, `r` or `s`.
* The second offset is commonly aliased as `y`, `g` or `t`.

| Type          | Meaning                  |
| ------------- | ------------------------ |
| `f32[2] vals` | The values of the vector |

### f32vec3
An array of 3 `f32`. Typically used to represent positions and normal vectors.

* The first offset is commonly aliased as `x`, or `r`.
* The second offset is commonly aliased as `y`, `g`.
* The third offset is commonly aliased as `z`, `b`.

| Type          | Meaning                  |
| ------------- | ------------------------ |
| `f32[3] vals` | The values of the vector |

### u8vec4
An array of 4 `u8`. Typically used to represent colors.

* The first offset is commonly aliased as `x`, or `r`.
* The second offset is commonly aliased as `y`, `g`.
* The third offset is commonly aliased as `z`, `b`.
* The fourth offset is commonly aliased as `w`, `a`.

| Type         | Meaning                  |
| ------------ | ------------------------ |
| `u8[4] vals` | The values of the vector |