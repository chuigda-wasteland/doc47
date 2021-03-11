## 7. &emsp; Declarations &emsp; `[pr47.decl]`

<sup>1</sup> &emsp; A declaration may introduce a variable or function into a specific scope.

### 7.1 &emsp; Variable declaration &emsp; `[pr47.decl.var]`

> grammer of variable declaration
>
> ```plaintext
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
var a = 54; // a is of int type now
a = 'c'; // a is of char type now
a = "Здравствуйте" // a is of string type now
```

<sup>4</sup> &emsp; A variable can be declared with `deduced` type. Variables with deduced type are considered typed variables, whose type is automatically deduced from its initializer. Initializer evaluates to value `null` is ill formed.

<sup>5</sup> &emsp; Type deduction always produces non-nullable types.

```go
var a deduced = 5; // a deduced to be int
var b deduced = "привет"; // b deduced to be string
var c deduced = null; // ill-formed
```

### 7.2 &emsp; Function declaration &emsp; `[pr47.decl.func]`

> grammar of function declaration
> 
> ```plaintext
> function-decl ::= "func" identifier "(" param-list ")" opt-type opt-func-body
> 
> opt-func-body ::= 
>       ";"
>     | compound-stmt
> 
> opt-type ::=
>       type
>     | ""
> ```

<sup>1</sup> &emsp; A function declaration may have an optional function body, a compound statement. A function declaration with a body is called a *function definition*. A function declaration without a body may serve an attribute provider.

### 7.2.1 &emsp; Function parameters &emsp; `[pr47.decl.func.parm]`

> grammar of function parameter
>
> ```plaintext
> param-list ::= 
>       param-list "," param
>     | param
>     | ""
>
> param ::= identifier opt-type
> ```

<sup>1</sup> &emsp; A function may optionally take a series of parameters. A function parameter may be explicitly marked with a type, such parameters are called *typed parameters*. Parameters that are not a typed parameters are called *untyped parameters*.
