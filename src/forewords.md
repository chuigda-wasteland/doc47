## Introduction to the Pr47 programming language

<sup>1</sup> &emsp; **Pr47 (47工程, Project-47, Проекта-47)** is an extension language designed to support general procedural programming. Pr47 intends to be a powerful light-weight configuration language for Rust programs, while supporting seamless interaction with Rust environment.

<sup>2</sup> &emsp; Pr47 intends to be a strict language, any operation violating Pr47 rules should be rejected and error will be thrown to host environment, either at compile time or at run time. A Pr47 implementation may also implement an optional tolerant mode, within which some of erroneous operations are allowed, and other erroneous operations are skipped without interrupting program execution. However, operations resulting undefined behavior are never legal and shall be avoided with every effort.

<sup>3</sup> &emsp; This document is provided AS IS, WITHOUT ANY WARRANTY. If you find any bugs, typos or defects of this document, mail [ICEY(icey@icey.tech)](mailto://icey@icey.tech).
