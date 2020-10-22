## 4. &emsp; Types &emsp; `[pr47.type]`

<sup>1</sup> &emsp; Since Pr47 is semi-statically typed language, entities may be either statically type checked or dynamically type checked. A Pr47 implementation should use compile time information as much as possible to optimize program execution and provide better diagnostics.

### 4.1 &emsp; Type classifications &emsp; `[pr47.type.class]`

<sup>1</sup> &emsp; There are two classes of types in Pr47: value types and reference types. Objects of value types comply copy semantics when assignment takes place, while objects of reference types comply clone (or shallow copy) semantics when assignment takes place. Foreign types registered from host environment are considered reference types.

### 4.2 &emsp; Builtin values types &emsp; `[pr47.type.value]`

<sup>1</sup> &emsp; **Integer** type is denoted by keyword `int` and serves to represent integral numbers. Integer type should have the same representation with Rust `i64`.

<sup>2</sup> &emsp; **Float type** is denoted by keyword `float` and serves to represent IEEE754 floating point numbers. Float type should have the same representation with Rust `f64`.

<sup>3</sup> &emsp; **Byte** type is denoted by keyword `byte` and serves to represent a single byte. Byte type should have the same representation with Rust `u8`.

<sup>4</sup> &emsp; **Char** type is denoted by keyword `char` and serves to represent a unicode character. Char type should have the same representation with Rust `char`.

<sup>5</sup> &emsp; **Boolean** type is denoted by keyword `bool` and serves to represent a binary `true` or `false`. Boolean type should have the same representation with Rust `bool`.

### 4.3 &emsp; Builtin reference types &emsp; `[pr47.type.ref]`

> TODO
>
> <sup>1</sup> &emsp; **string** type
>
> <sup>2</sup> &emsp; **vector** type
>
> <sup>3</sup> &emsp; **object** type
>
> <sup>4</sup> &emsp; **any** type

### 4.4 &emsp; Foreign types &emsp; `[pr47.type.foreign]`

> TODO

### 4.5 &emsp; Type fusing &emsp; `[pr47.type.fusion]`

> TODO