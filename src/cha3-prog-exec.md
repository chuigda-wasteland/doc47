## 3. &emsp; Program execution &emsp; `[pr47.exec]`

<sup>1</sup> &emsp; Pr47 is a semi-static programming language, due to which it combines static or compile time checks with dynamic or runtime checks. A Pr47 program is firstly compiled with certain static rules, and then executed with dynamic rules applied.

### 3.1 &emsp; Initialization &emsp; `[pr47.exec.init]`

<sup>1</sup> &emsp; A Pr47 implementation may optionally have one or more initialization stages, which may initialize certain internal data and programs. Initialization, if present, should act like a normal Rust function or method.

### 3.2 &emsp; Pr47 foreign item registration &emsp; `[pr47.exec.reg]`

<sup>1</sup> &emsp; After the Pr47 implementation gets initialized, foreign types and functions will be registered, so that they can be used in further program.

<sup>2</sup> &emsp; Foreign types are registered first. Registering a foreign type is mostly about retrieving the type check informations of that type via `std::any::TypeId`, and then associate that information with a Pr47 identifier.

<sup>3</sup> &emsp; A foreign function can be registered only after all its dependent foreign types get registered. Registing a Rust function mostly involves retrieving the function signature with assistance of `std::any::TypeId`, and then associate that information with a Pr47 identifier.

### 3.4 &emsp; Compilation &emsp; `[pr47.exec.comp]`

<sup>1</sup> &emsp; After registing foreign types and functions, the Pr47 implementation then read in the Pr47 scripts, enforce the static checking rules, and optionally transform source codes into some optimized form. In a typical Pr47 implementation, the following steps may be taken in order.

<sup>2</sup> &emsp; *Lexical analyzer* or *scanner* preprocesses the source code, removing any comment and redundant spaces, and produce a series of tokens.

<sup>3</sup> &emsp; *Syntactical analyzer* or parser* parses the incoming token stream according to CFG definitions, optionally constructs a concrete syntax tree (CST) and passes it to next compiling stage.

<sup>4</sup> &emsp; If supported, *compiler action applier* then applies *early compiler actions*, operates on the produced CST, performs several syntactical transformations and passes the updated CST to next compiling stage.

<sup>5</sup> &emsp; *Semantic analyzer* analyzes the produced CST (if applicable), enforces static semantic rules, and optionally produces an abstract syntax tree (AST).

<sup>6</sup> &emsp; If supported, *compiler action applier* then applies *late compiler actions*, operates on the produced AST, performs several semantical transformations and passes the updated AST to next stage.

<sup>7</sup> &emsp; An optional *code generator* transforms the final AST (if applicable) to some intermediate form.

### 3.5 &emsp; Function export &emsp; `[pr47.exec.export]`

<sup>1</sup> &emsp; After compilation, the Pr47 implementation should be able to export functions to host environment.

### 3.6 &emsp; Program execution &emsp; `[pr47.exec.run]`

<sup1>1</sup> &emsp; It is possible to launch a single Pr47 function via the exported function interface. It is also possible to treat the whole script as an executable, and start execution from function `main`, `entry` or `application_start`. Only one of `main`, `entry` and `application_start` may be declared to global scope, and must satisfy the following signature:

```go
func func_name() int
```

&emsp; or:

```go
func func_name(vector<string>) int
```