## &emsp; 10. Attributes &emsp; `[pr47.attr]`

<sup>1</sup> &emsp; An attribute, by itself, does not have any semantics. Attributes are read by compiler actions who're able to transform the source program at syntax or semantic layer.

> grammar of global attributes
> 
> ```plaintext
> global-attrs ::= 
>        global-attrs global-attr
>      | ""
>
> global-attr ::= "#![" attr-list "]"
> ```

<sup>2</sup> &emsp; Global attributes can be added to the commence of a Pr47 source file.

> grammar of attributed item
> 
> ```plaintext
> attr-decl ::=
>       attr decl
>     | decl
>
> attr-stmt ::=
>       attr stmt
>     | stmt
>
> attr ::= "#[" attr-list "]"
> ```

<sup>3</sup> &emsp; Each declaration or statement in Pr47 may be prefixed with an attribute declarator.

> grammar of attribute
>
> ```plaintext
> attr-list ::= 
>       attr-list "," attr-body
>     | attr-body
>     | ""
> 
> attr-body ::= 
>       single-id-attr
>     | single-value-attr
>     | kv-pair-attr
>
> single-id-attr ::= identifier
> kv-pair-attr   ::= identifier "=" attr-body
> call-like-attr ::= identifier "("  attr-list ")"
> ```

<sup>4</sup> &emsp; An attribute may be a single identifier attribute, a key-value like attribute or a function call like attribute.

### &emsp; 10.1 Compiler actions &emsp; `[pr47.attr.act]`

<sup>1</sup> &emsp; A compiler action is a Rust object consists of a name, an attribute *recognizer* and a series of transformation. A compiler action may be either an *early compiler action* that acts on syntactical layer, or a *late compiler action* that acts on semantical layer. Concrete representation and grammar of compiler actionares implementation defined.

<sup>2</sup> &emsp; Pr47 implementation matches the recognizer of compiler action and each attribute in *top level attribute list* in the following way:
 - For single identifier attribute, the compiler action and attribute match if the identifier and recognizer match
 - For key-value like attribute, the compiler action and attribute match if the key part of that attribute and recognizer match
 - For function call like attribute, the compiler action and attribute match if the *function name part* of that attribute and recognizer match.

&emsp; See example.

```go
#[force_static,    // attr1, may match with compiler action "force_static"
  repr="C",        // attr2, may match with compiler action "repr"
  proof(postulate) // attr3, may match with compiler action "proof"
]
func foo() {}
```

<sup>3</sup> &emsp; Once a compiler action matches with an attribute, the attribute arguments (if present) together with the attributed item (the whole translation unit for global attributes) are then sent to the transformation code. See example.

```go
// Here, the attribut list [result, T, E], together with the function
// itself "func bar() {}" are sent to compiler action "error_chain"
#[error_chain(result, T, E)]
func bar() {}
```