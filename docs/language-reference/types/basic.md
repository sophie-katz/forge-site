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

# Basic types

## Boolean

There is one boolean type: `bool`. Boolean values can have [two values](../literals/boolean.md): `true` and `false`.

## Integer

The most common integer type is `int`, which is a signed integer that is automatically sized to prevent overflow.

They are 32 bits wide by default, but if any arithemetic operation is made against a value that is 64-bits wide, the result will be 64-bits wide even though it is still of the `int` type.

There is also an unsigned equivalent, `uint`.

### Explicit width

There are several integer types with explicit widths:

| Type | Signed? | Bit width |
| ---- | ------- | --------- |
| `i8` | Yes | 8 |
| `i16` | Yes | 16 |
| `i32` | Yes | 32 |
| `i64` | Yes | 64 |
| `isize` | Yes | System-dependent[^1] |
| `u8` | No | 8 |
| `u16` | No | 16 |
| `u32` | No | 32 |
| `u64` | No | 64 |
| `usize` | No | System-dependent[^1] |

These are less idiomatic, but are useful especially for system programming or optimization.

### Rationale

These types are inspired by Rust's integer types, which are very clear and readable.

The automatic-width integer type is chosen because in most cases we only care about arithmetic correctness and not bit magic. This is the most common use case for integers, so it should be the default.

## Float

All floats have explicit widths. The most idiomatic way to deal with floats is to use `float` which is aliased to `f64`, but this is declared in the standard library and is not a compiler construct.

| Type | Bit width |
| ---- | --------- |
| `f32` | 32 |
| `f64` | 64 |

### Rationale

These types are inspired by Rust's float types, which are very clear and readable.

## Special types

- `void` - used to denote when a function does not return a value.
- `never` - used to denote when a function's return type is unreachable because of program termination.
- `null` - used to represent null values.

### Rationale

These types are inspired by TypeScript, which has a similar set of special types which are very effective and readable.

[^1]: `isize` and `usize` are system dependent and take the size of pointers on the system for which the code is being compiled. On 32-bit systems these will be 32 bits, and on 64-bit systems these will be 64 bits.
