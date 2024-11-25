<!--
Copyright 2024 Sophie Katz

This file is part of the Forge programming language.

Forge is free software: you can redistribute it and/or modify it under the terms of the GNU General
Public License as published by the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

Forge is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the
implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public
License for more details.

You should have received a copy of the GNU General Public License along with Forge. If not, see
<https://www.gnu.org/licenses/>.
-->

# Type modifiers

```
ref int
```

## Details

Forge uses type modifiers for:

- [References](#references)
- [Pointers](#pointers)
- [Optionals](#optionals)
- [Constants](#constants)

### References

```
ref int
```

References are a way to point to a value instead of passing it directly. The address of the value that they point to cannot be changed. They also cannot be null.

You cannot apply the `ref` modifier more than once.

!!! warning

    This section needs more details.

### Pointers

```
pointer int
```

Pointers can point to any address in memory. This address can be changed. They can be null.

!!! note

    Unlike in C/C++, typeless pointers are not allowed (for example, `pointer void` will cause an error). You must specify a type.

    If you want to have typeless access to an address in memory, use a `usize` value instead and cast as needed.

You may apply the `pointer` modifier more than once.

!!! warning

    This section needs more details.

### Optionals

```
opt int
```

Optionals can be null or contain a value. They are used to represent values that may or may not exist.

You may apply the `opt` modifier more than once, although this is not idiomatic.

!!! warning

    This section needs more details.

### Constants

```
const int
```

Constant values cannot be mutated.

You cannot apply the `const` modifier more than once.

!!! warning

    This section needs more details.

## Syntax

```ebnf
(* assume unmodified-type is declared elsewhere *)

type-modifier = "ref" | "pointer" | "opt" | "const";

modified-type = { type-modifier } unmodified-type;
```

## Rationale

These are all common type use cases, so having them built into the language makes the syntax easier and more readable.

References and pointers are usually represented with the symbols `&` and `*` in many languages (C/C++/Rust/etc), but they are represented with keywords here. This is because it is often more readable to have fewer symbols and these keywords are not often used.

## Examples

An unmodified type:

```
int
```

An optional type:

```
let x: opt int = null;

x = 5;
```

A constant type:

```
let x: const int = 5;

x = 6; // this will cause an error
```

A pointer type:

```
let x: int = 5;
let y: int = 6;

let p: pointer int = &x;

p = &y;

p = null;
```

A reference type:

```
let x: int = 5;
let y: int = 6;

let r: ref int = &x;

r = &y; // this will cause an error

r = null; // this will cause an error
```

!!! warning

    This section may become incorrect after adding in more details to other sections.
