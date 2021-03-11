## 6. &emsp; Foreign function interface &emsp; `[pr47.ffi]`

<sup>1</sup> &emsp; A Pr47 program is able to use Rust types, call Rust functions or export functions to Rust via Pr47 foreign function interace (FFI).

### 6.1 &emsp; Binding Rust type `[pr47.ffi.type]`

<sup>1</sup> &emsp; An implementation must be able to register any Rust type `T: 'static` and bind that type to a Pr47 identifier. Bounded type can then be used in Pr47 program via that appointed identifier.

```rust
    // pseudo code, implementation does not have to be in this way
    // binding Rust type T to Pr47 identifier a.b.T
    pr47_instance.bind_type::<T>("a.b.T");
```

```go
    import a.b.T;

    func foo(t T) { /* ... */ }
    func bar() T { /* ... */ }
```

<sup>2</sup> &emsp; An implementation may optionally implement a registering mechanism for `T: 'a`. Restrictions and semantics are implementation defined, and suggested to be coherent with `T: 'static`.

<sup>3</sup> &emsp; Redefining any registered type is considered ill-formed. Registering a type twice is considered ill-formed. Registering types already handled in type fusion rulesis is considered ill-formed.

### 6.2 &emsp; Binding Rust function `[pr47.ffi.func]`

<sup>1</sup> &emsp; An implementation must be able to register any Rust function whose parameter types satisfy one of the following rules:

  - `T: 'static`
  - `&'a T` or `&'a mut T`, where `'a` outlives the lifetime of the Pr47 instance (if applicable), and `T: 'static`
  - `Option<T>`, where `T` satisfies one of the two rules above

&emsp; and return type satisfies one of the following rules:

  - `T: 'static`
  - `&'a T` or `&'a mut T`, where `'a` outlives the lifetime of the Pr47 instance (if applicable), and `T: 'static`
  - `Option<T>`, where `T` satisfies one of the two rules above
  - `&'a Option<T>` or `&'a mut Option<T>`, and `T: 'static`
  - `Result<T, E>`, where `T` satisfies one of the four rules above, and `E: 'static + std::error::Error`

<sup>2</sup> &emsp; The implementation should perform the following automatic operations for function arguments:

  - for parameter with `Option` type, convert `null` value to `None` variant, and convert non-`null` value to `Some` variant according to the following four rules
  - for parameter with `&'a T` type, share Pr47 object with Rust environment
  - for parameter with `&'a mut T` type, mutably share Pr47 object with Rust environment
  - otherwise, move the Pr47 object to Rust environment

<sup>3</sup> &emsp; The implementation should perform the following automatic operations for function return value, step by step:

  - for return value with `Result<T, E>` type, convert `Err` variant to a Pr47 exception, and convert `Ok` variant according to the following five rules
  - for return value with `&'a Option<T>` type, convert it to `Option<&'a T>`; and for `&'a mut Option<T>`, convert it to `Option<&'a mut T>`
  - for return value with `Option<T>` type, convert `None` variant to `null` value, and convert `Some` variant according to the following three rules
  - for return value with `&'a T` type, share that value with Rust environment
  - for return value with `&'a mut T` type, mutably share that value with Rust environment
  - otherwise, move that value to Pr47

### 6.3 &emsp; Exporting Pr47 function `[pr47.ffi.export]`
