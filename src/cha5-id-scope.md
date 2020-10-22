## 5. &emsp; Identifiers and scopes &emsp; `[pr47.scope]`

<sup>1</sup> &emsp; An identifier can denote an object; a function; a member of an object or a member of a foreign transparent structure. For each different entity that an identifer designates, the identifier is visible only wthin a region of program text called scope.

<sup>2</sup> &emsp; There are two kinds of scope in Pr47: global scope and block scope. Identifiers introduced into global scope are valid in any context of a Pr47 program, while identifiers introduced into a block scope are only valid in that block after the introduction point. An identifier should not be introduced to the same scope twice. See example.

```go
// v1 introduced to global scope, valid in global, functions f1 and f2
var v1 = 5;
var v2 = f1(v1); // valid

// f1 introduced to global scope, valid in global, functions f1 and f2
// parameter v3 introduced to function f1 scope, only valid in f1
func f1 (v3) {
	v4 = 6; // invalid, v4 not introduced yet.

	var v3 = 13; // invalid, v3 already introduced (as a parameter)
	// v4 introduced to function f1 scope, only valid in f1
	var v4 = 191;

	v1 = 19; // valid
	f2(); // valid

	{ // 'a
		// v5 introduced to 'a scope, valid in 'a
		var v5 = 5;
	}
	v5 = 66; // invalid
}

// f2 introduced to global scope, valid in global, functions f1 and f2
func f2 () {
	f1(); // valid
	v2 = 42; // valid
	v3 = 42; // invalid, v3 is local to f1
	v4 = 42; // invalid, v4 is local to f1
}

var f1 = 130; // invalid, f1 already introduced (as a function)
```

<sup>3</sup> &emsp; One identifier can be introduced to more than one block scopes. Same identifiers in different block scopes are isolated. See example.

```go
// block 'a
func f1 () {
	var v int = 5; // A variable v of type int introduced to 'a
}

// block 'b
func f2 () {
	var v string = "5"; // A variable v of type str introduced to 'b

	// block 'c
	{
		var v2 float = 1.9; // A variable v2 of type float introduced to 'c
	}

	// block 'd
	{
		var v2 int = 42; // A variable v2 of type float introduced to 'd
	}
```

<sup>4</sup> &emsp; One identifier can be introduced to two nested scopes. In this case identifiers introduced to the inner scope will shadow the identifier introduced to the outer scope. To use the global identifier explicitly, use global:name. See example.

```go
var v1 = 43;

// block 'a
func f1() {
	v1.print(); // access global v1
}

// block 'b
func f2() {
	var v1 = 14; // shadowing global v1
	v1.print();  // access local 'b v1
	// block 'c
	{
		var v1 = "19"; // shadowing 'b v1
		v1.print(); // access local 'c v1
	}
	global:v1.print(); // access global v1 using global: specifier
}
```
