## 1. &emsp; Terms and definitions &emsp; `[pr47.terms]`

1.  **Registration time**: (phrase) the Pr47 implementation import foreign types and foreign functions from Rust host environment.
2.  **Compile time**: (phrase) the Pr47 implementation checks the program with certain static checking rules, and optionally transform source program into some optimized representation.
3.  **Run time**: (phrase) the Pr47 implementation executes the program and yield results.
4.  **Well-formed**: program does not violate Pr47 rules.
5.  **Ill-formed**: program not well formed.
6.  **Reject**: (compile time behavior) the Pr47 implementation refuses to run an ill-formed program, since it violates one or more piece of static rules.
7.  **Undefined behavior**: (runtime hehavior) result of operation is not defined, and should not be relied on.
