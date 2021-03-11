## 4. &emsp; Types &emsp; `[pr47.type]`

<sup>1</sup> &emsp; Since Pr47 is semi-statically typed language, entities may be either statically type checked or dynamically type checked. A Pr47 implementation should use compile time information as much as possible to optimize program execution and provide better diagnostics.

### 4.1 &emsp; Type classifications &emsp; `[pr47.type.class]`

<sup>1</sup> &emsp; There are two classes of types in Pr47: value types and reference types. Objects of value types comply copy semantics when assignment takes place, while objects of reference types comply clone (or shallow copy) semantics when assignment takes place. Foreign types registered from host environment are considered reference types.

### 4.2 &emsp; Builtin values types &emsp; `[pr47.type.value]`

<sup>1</sup> &emsp; **Integer** type is denoted by keyword `int` and serves to represent integral numbers. Integer type should have the same representation with Rust `i64`.

<sup>2</sup> &emsp; **Float type** is denoted by keyword `float` and serves to represent IEEE754 floating point numbers. Float type should have the same representation with Rust `f64`.

<sup>3</sup> &emsp; **Byte** type is denoted by keyword `byte` and serves to represent a single byte. Byte type should have the same representation with Rust `u8`.

<sup>4</sup> &emsp; **Character** type is denoted by keyword `char` and serves to represent a unicode character. Char type should have the same representation with Rust `char`.

<sup>5</sup> &emsp; **Boolean** type is denoted by keyword `bool` and serves to represent a binary `true` or `false`. Boolean type should have the same representation with Rust `bool`.

### 4.3 &emsp; Builtin reference types &emsp; `[pr47.type.ref]`

<sup>1</sup> &emsp; **String** type is denoted by keyword `string` and serves to represent any UTF-8 text. String type should have the same representation with Rust `std::string::String` by default.

<sup>2</sup> &emsp; **Vector** or **dynamic array** type is denoted by keyword `vector` and serves to represent a variable length array. `vector` is a generic container. See grammar and example.

> grammar of vector type
> 
> ```plaintext
>     vector-type ::= "vector" "<" type ">"
> ```

```go
    var v vector<int> = new_vec();
    v.push(1);      // now v = [1]
    v.insert(0, 2); // now v = [2, 1]
    v.push(2.5);    // ill-formed, v is an vector of int
```

<sup>3</sup> &emsp; The vector type should have a corresponding Rust representation, so that it can be used by Pr47 type fusion.

> <sup>4</sup> &emsp; **object** type
>
> <sup>5</sup> &emsp; **any** type

<sup>6</sup> &emsp; There's no reference to value-typed objects in Pr47.

### 4.4 &emsp; Nullable types &emsp; `[pr47.type.nullable]`

<sup>1</sup> &emsp; All types and variables are by default not nullable, and thus cannot store the `null` value.

<sup>2</sup> &emsp; For each non-nullable type `T`, there's a nullable counterpart `?T`, which is capable of storing `null` value.

### 4.5 &emsp; Foreign types &emsp; `[pr47.type.foreign]`

> TODO

### 4.6 &emsp; Type fusion &emsp; `[pr47.type.fusion]`

> TODO