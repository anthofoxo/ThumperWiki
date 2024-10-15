# Mesh Format
Thumper's mesh files are a stripped down version of DirectX .x files. Meshes contain a raw memory dump of vertices and indices along with a few unknowns.

We know enough about the format to export thumper meshes and replace existing ones. We're unsure exactly how the hashes are computed from paths to mesh files.

In Thumper a mesh vertex contains a position, normal vector, texture coordinates, and colors. The colors seem to always be rgba of 0.

The index values are of type `unsigned short`, `3` indices make up a triangle.

The vertex structure matches the type below:
```cpp
struct f32vec3 {
  f32 x, y, z;
};

struct f32vec2 {
  f32 x, y;
};

struct u8vec4 {
  u8 b, g, r, a;
};

struct Vertex {
  f32vec3 position;
  f32vec3 normal;
  f32vec2 texcoord;
  u8vec4 color;
};

struct Triangle {
   u16 indices[3];
};
```

## Format
<div class="warning">
This table is using the newer general types.
</div>

| Type     | Meaning                                                |
| -------- | ------------------------------------------------------ |
| u32      | Header, meshes have a header value of 6                |
| u32      | *Unknown*, typically `1`[^unknown_1]                   |
| u32      | Vertex count.                                          |
| variable | The vertices. Size = `vertexCount * sizeof(Vertex)`    |
| u32      | Face count.[^note_1]                                   |
| variable | Faces. [^note_2] Size = `faceCount * sizeof(Triangle)` |
| u16      | *Unknown*, typically `1`[^unknown_2]                   |

## Mesh Conversions
With custom software we can take this data and export it into a usable format or take a mesh and replace it for our own custom meshes. [Aurora](https://github.com/anthofoxo/ThumperAurora) has native support to do this for you.

## UV Coordinate Space
While meshes use 2D texture coodinates, they all seem to lie on a flat line at `y = 0`. This means Thumper likely doesn't do any traditial texture mapping and texture coodinated in your mesh will need to be tuned accordinly.

## Footnotes
[^unknown_1]: This unknown value is typically `1`, possibly could be a format type or a count of sorts.

[^note_1]: Faces are assumed to be triangles and they are in all cases we've seen. This is not confirmed and should be tested further.

[^note_2]: If these are triangles then the size calculation is correct, otherwise this needs revised.

[^unknown_2]: This value seems to match up with an index but doesn't fit into the size described by the face count. This usually has a value of `1`.