## 6. &emsp; Variables &emsp; `[pr47.var]`

<sup>1</sup> &emsp; A variable is a name bound to an object. A variable is introduced with a a variable declaration or function parameter declaration.

### 6.1 &emsp; Variable declaration &emsp; `[pr47.var.decl]`

> grammer of variable declaration
>
> ```bnf
> var-decl ::= "var" identifier var-decl-type var-opt-init
>
> var-decl-type ::=
>       type
>     | "deduced"
>     | ""
>
> var-opt-init ::=
>       "=" expr
>     | ""
> ```

<sup>1</sup> &emsp; A variable declaration introduces a variable to its scope. If a variable declaration occurs in a block, then then the variable is introduced to that block scope; otherwise to the global scope.

<sup>2</sup> &emsp; A typed variable declaration introduces a variable of specific type to scope. The introduced variable is called *typed variable*. A typed variable can only be assigned with object of that type. See exmple.

```go
var a int = 42; // a is of int type
a = 5.56; // ill-formed, type mismatch
var b int = 'д'; // ill-formed, type mismatch
```

<sup>3</sup> &emsp; An untyped variable declaration introduces a variable of uncertain type to scope. The introduced variable is called *untyped variable*. An untyped variable can be assigned with object of any type. Concrete type of the object denoted by the variable may change as new object gets assigned to the variable. See example.

```go
var a = 54; // as is of int type now
a = 'c'; // a is of char type now
a = "Здравствуйте" // a is of string type now
```

<sup>4</sup> &emsp; A variable can be declared with `deduced` type. Variables with deduced type are considered typed variables, whose type is automatically deduced from its initializer. Initializer evaluates to value `null` is ill formed.

```go
var a deduced = 5; // a deduced to be int
var b deduced = "привет"; // b deduced to be string
var c deduced = null; // ill-formed
```
