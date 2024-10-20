# Magic Numbers
A magic number is a 32-bit hash value produced by applying a hash function on a string. Hash tables are maintained in the game executable storing the hash values for string literals like game file paths, object types and parameter names. This is probably done to avoid expensive string comparisons and allow a more compact way of packing the binary game files.

## Hash Function
We have two versions of this hash function shown below, we should come up with a version implementing the for loop. The hash function is based on `FNV-1a`.

The implementations below may or may not match Thumper's function signature for their hash function. More decomp work needs done to discover this.

### TiddlyHost's Implementation
```cpp
uint32_t hash32(std::string s) {
  uint32_t h = 0x811c9dc5;
  for (std::string::size_type i = 0; i < s.length(); i++)
    h = (h ^ s[i]) * 0x1000193;
  h *= 0x2001;
  h = h ^ (h >> 0x7);
  h *= 0x9;
  h = h ^ (h >> 0x11);
  h *= 0x21;
  return h;
}
```

### Auora's Implementation
```cpp
uint32_t hash32(unsigned char const* array, unsigned int size) {
  uint32_t h = 0x811c9dc5;
  
  while (size > 0) {
    size--;
    h = (h ^ *array) * 0x1000193;
    array++;
  }
  
  h *= 0x2001;
  h = (h ^ (h >> 0x7)) * 0x9;
  h = (h ^ (h >> 0x11)) * 0x21;
  return h;
}
```

## List of Magic Numbers
Here is a list of different magic numbers used in Thumper game files.
* [Hashed File Names](hashed_file_names.md)
* [Types of .objlib Files](objlib_gen_structure.md#types-of-objlib-files)
* [Object Types](object_types.md)
* [Object/Parameter Selectors](object_param_selectors.md)