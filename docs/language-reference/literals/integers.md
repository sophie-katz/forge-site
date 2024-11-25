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

# Integer literals

```
5
```

## Details

Forge supports integers literals with:

* Binary, octal, decimal, and hexadecimal digits
* Optional underscores for readability
* Optional suffixes for for explicit types

Integer literals always have type `int` unless specified otherwise and are 32-bit if the represented value fits within 32 bits without truncation. Otherwise, they are 64-bit.

## Rationale

These are all syntaxes that are widely expected in modern languages. They also take heavy inspiration from Rust, which has very clear and readable literals.

## Syntax

Integers can optionally be prefixed with any of:

- `0b` for binary
- `0o` for octal
- `0x` for hexadecimal

And they have a sequence of digits and separators following them. They can then optionally be suffixed with any of:

- `i8`, `i16`, `i32`, `i64`, `isize`, `u8`, `u16`, `u32`, `u64`, `usize`

| Base | Regex |
| ---- | ----- |
| Binary | `0b[01]([01_]*[01])?(i8\|i16\|i32\|i64\|isize\|u8\|u16\|u32\|u64\|usize)?` |
| Octal | `0o[0-7]([0-7_]*[0-7])?(i8\|i16\|i32\|i64\|isize\|u8\|u16\|u32\|u64\|usize)?` |
| Decimal | `[1-9]([0-9_]*[0-9])?(i8\|i16\|i32\|i64\|isize\|u8\|u16\|u32\|u64\|usize)?` |
| Hexadecimal | `0x[0-9a-fA-F]([0-9a-fA-F_]*[0-9a-fA-F])?(i8\|i16\|i32\|i64\|isize\|u8\|u16\|u32\|u64\|usize)?` |

## Examples

A simple decimal integer:

```
5
```

A binary integer (which equals `5` in decimal):

```
0b101
```

An octal integer (which equals `5` in decimal):

```
0o5
```

A hexadecimal integer (which equals `5` in decimal):

```
0x5
```

An integer with underscores for readability:

```
1_000
```

An integer with a type suffix, which is a signed 64-bit integer:

```
5i64
```

An integer with a type suffix, which is an unsigned 8-bit integer:

```
5u8
```
