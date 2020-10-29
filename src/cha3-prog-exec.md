## 3. &emsp; Program execution &emsp; `[pr47.exec]`

<sup>1</sup> &emsp; Pr47 is a semi-static programming language, due to which it combines static or compile time checks with dynamic or runtime checks. A Pr47 program is firstly compiled with certain static rules, and then executed with dynamic rules applied.

### 3.1 &emsp; Initialization &emsp; `[pr47.exec.init]`

<sup>1</sup> &emsp; A Pr47 implementation may optionally have one or more initialization stages, which may initialize certain internal data and programs. Initialization, if present, should act like a normal Rust function or method.

### 3.2 &emsp; Pr47 foreign type registration &emsp; `[pr47.exec.reg.type]`

<sup>1</sup> &emsp; A Pr47 implementation should provide an interface for registing foreign types, so that foreign functions and scripts can use them. Registing a Rust type mostly involves remembering the `std::any::TypeId` of that type, and associate it with an identifier in a specific scope.

<sup>2</sup> &emsp; The implementation must be able to register any `T: 'static`; The implementation may also optionally implement registration for `T: 'a`, where `'a` is the lifetime of Pr47 environment, with certain restrictions and assumptions.

<sup>3</sup> &emsp; Implementation should allow user to omit the identifier and scope for that registered type. When user choose to omit type name and scope, the implementation should use `std::any::type_name` to obtain an descriptional name for that type, and register that type to global scope.

<sup>4</sup> &emsp; Despite in the implementation part, registing a foreign type to `std` module or its submodule is ill-formed, and should be rejected at registration time.

### 3.3 &emsp; Pr47 foreign function registration &emsp; `[pr47.exec.reg.func]`

<sup>1</sup> &emsp; A Pr47 implementation should provide an interface for registing foreign functions, so that scripts can use them. Registing a Rust function mostly involves remembering the function signature with assistance of `std::any::TypeId`, optionally creating a wrapper for that function and associate it with an identifier in a specific scope.

<sup>2</sup> &emsp; An implementation must be able to register any `Fn` whose parameter types and return type satisfies `T: static`. An implementation may also optionally implement registration for `Fn` whose parameter types and return type satisfies `T: 'a`, where `'a` is the lifetime of Pr47 environment, with certain restrictions and assumptions.

<sup>3</sup> &emsp; By default, a Pr47 implementation should transfer the ownership of argument to Rust host environment when calling a foreign function, take the ownership of return value from Rust host environment when the function returns.

<sup>4</sup> &emsp; For parameters satisfy `T: Copy`, a Pr47 implementation should make a copy of the argument.

<sup>5</sup> &emsp; For parameters with reference type `&T`, a Pr47 implementation should share the argument immutably between the Pr47 environment and Rust host. For parameters with mutable reference type `&mut T`, the implementation should share the argument mutably between the Pr47 environment and Rust host. Foreign functions require mutable share are considered unsafe by Pr47.

<sup>6</sup> &emsp; For parameters with type that satisfies *type fusion* rules, see `[pr47.type.fusion]`. 

<sup>7</sup> &emsp; When receiving return values from Rust function, `&std::option::Option<T>` should be converted to `std::option::Option<&T>` using `std::option::Option::as_ref`, and `&mut std::option::Option<T>` should be converted to `std::option::Option<&mut T>` using `std::option::Option::as_mut`.

### 3.4 &emsp; Compilation &emsp; `[pr47.exec.comp]`

<sup>1</sup> &emsp; After registing foreign types and functions, the Pr47 implementation should then read in the Pr47 scripts, enforce the static checking rules, and may optionally transform source codes into some optimized form. In a typical Pr47 implementation, the following steps may be taken in order.

#### 3.4.1 &emsp; Lexical analysis &emsp; `[pr47.exec.comp.lex]`

#### 3.4.2 &emsp; Parsing &emsp; `[pr47.exec.comp.parse]`

#### 3.4.3 &emsp; Early compiler action application &emsp; `[pr47.exec.comp.act1]`

#### 3.4.4 &emsp; Semantics analysis &emsp; `[pr47.exec.comp.sema]`

#### 3.4.5 &emsp; Late compiler action application &emsp; `[pr47.exec.comp.act2]`

#### 3.4.6 &emsp; Transformation or code generation &emsp; `[pr47.exec.comp.gen]`

### 3.5 &emsp; Function export &emsp; `[pr47.exec.export]`

<sup>1</sup> &emsp; After compilation, the Pr47 implementation should be able to export functions to host environment. Detailed requirements on such functionality are similar to requirements stated in `[pr47.exec.reg.func]`.

### 3.6 &emsp; Program execution &emsp; `[pr47.exec.run]`

<sup1>1</sup> &emsp; It is possible to launch a single Pr47 function via the exported function interface. It is also possible to treat the whole script as an executable, and start execution from function `main`, `entry` or `application_start`. Only one of `main`, `entry` and `application_start` may be declared to global scope, and must satisfy the following signature:

```go
func func_name() int
```

&emsp; or:

```go
func func_name(vector<string>) int
```