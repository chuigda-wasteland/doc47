## DOC47 - The documentation repository for Pr47

------

### What is Pr47
Project-47 (Pr47, 47工程) is a series of attemptations trying to create a modern, efficient and convenient scripting engine for Rust program. The created script language is also called Pr47. The language Pr47 intends to have the following features:
- Simple and handy grammar
- Semi-static type system
- Function overloading
- Generic containers
- Garbage collection
- Exception handling
- More powerful function binding
  - Automatically copy for `Copy` types
  - Support `&T` and `&mut T`
  - <del>Support `T: 'a`, instead of just `T: 'static`</del> Not possible, otherwise soundness hole.
- Type fusion
  - `Err` variant of Rust `Result<T, E>` will be automatically translated into Pr47 exception when performing FFI call
  - `None` variant of Rust `Option<T>` will be automatically translated into `null` value

The file `PR47_BY_EXAMPLE.p47` provides a overview for the Pr47 language. That example will get updated together with the documentation. If you are fresh to the language, that example is for you.

The documentation, however, is a more formal and strict standard for the language.

------

### What Pr47 is not, and why
- Totally statically typed programming language
  - For a statically typed language, you may just use Rust, not Pr47
  - But it is still possible to build world in a static way in Pr47
- A functional programming language
  - <del>Functional programming is crap</del>
  - Certain functional features will be added, if appropriate
  - Due to implementational reason, functional programs can be inefficient,
    and thus programming in full functional style is not encouraged.
- A easy language
  - Interacting with Rust references makes this language uneasy
  - We're trying to make this, though
- A light-weight language
  - Pr47 relies on its static checking to perform perfectly
  - Light-weightify options may be introduced

------

### Contribution & Donation
To contribute to the project, read the `CODE_OF_CONDUCT.txt`

I currently don't accept donations.
