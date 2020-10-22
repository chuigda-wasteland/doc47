## 3. &emsp; Program execution &emsp; `[pr47.exec]`

<sup>1</sup> &emsp; Pr47 is a semi-static programming language, due to which it combines static or compile time checks with dynamic or runtime checks. A Pr47 program is firstly compiled with certain static rules, and then executed with dynamic rules applied.

### 3.1 &emsp; Initialization &emsp; `[pr47.exec.init]`

<sup>1</sup> &emsp; A Pr47 implementation may optionally have one or more initialization stages, which may initialize certain internal data and programs. Initialization, if present, should act like a normal Rust function or method.

### 3.2 &emsp; Pr47 foreign type registration &emsp; `[pr47.exec.reg.type]`

<sup>1</sup> &emsp; A Pr47 implementation should provide an interface for registing foreign types, so that foreign functions and scripts can use them. Registing a Rust type mostly involves remembering the `std::any::TypeId` of that type, and associate it with an identifier in a specific scope.

<sup>2</sup> &emsp; The implementation must be able to register any `T: 'static`; The implementation may also optionally implement registration for `T: 'a`, where `'a` is the lifetime of Pr47 environment.

<sup>3</sup> &emsp; Implementation should allow user to omit the identifier and scope for that registered type. When user choose to omit type name and scope, the implementation should use `std::any::type_name` to obtain an descriptional name for that type, and register that type to global scope.

<sup>4</sup> &emsp; Despite in the implementation part, registing a foreign type to `std` module or its submodule is ill-formed, and should be rejected at registration time.

#### 3.3 &emsp; Pr47 foreign function registration &emsp; `[pr47.exec.reg.func]`

<sup>1</sup> &emsp; A Pr47 implementation should provide an interface for registing foreign functions, so that scripts can use them. Registing a Rust function mostly involves remembering the function signature with assistance of `std::any::TypeId`, optionally creating a wrapper for that function and associate it with an identifier in a specific scope.

<sup>2</sup> &emsp; An implementation must be able to register any `Fn` whose parameter types and return type satisfies `T: static`. An implementation may also optionally implement registration for `Fn` whose parameter types and return type satisfies `T: 'a`, where `'a` is the lifetime of Pr47 environment.

<sup>3</sup> &emsp; By default, a Pr47 implementation should transfer the ownership of argument to Rust host environment when calling a foreign function, take the ownership of return value from Rust host environment when the function returns.

<sup>4</sup> &emsp; For parameters satisfy `T: Copy`, a Pr47 implementation should make a copy of the argument.

<sup>5</sup> &emsp; For parameters with reference type `&T`, a Pr47 implementation should share the argument immutably between the Pr47 environment and Rust host. For parameters with mutable reference type `&mut T`, the implementation should share the argument mutably between the Pr47 environment and Rust host. Foreign functions require mutable share are considered unsafe by Pr47.

<sup>6</sup> &emsp; For parameters with type that satisfies *type fusion* rules, see `[pr47.type.fusion]`. 

<sup>7</sup> &emsp; Before performing any operations above, `&std::option::Option<T>` should be converted to `std::option::Option<&T>` using `std::option::Option::as_ref`, and `&mut std::option::Option<T>` should be converted to `std::option::Option<&mut T>` using `std::option::Option::as_mut`.

### 3.4 &emsp; Compliation &emsp; `[pr47.exec.comp]`


