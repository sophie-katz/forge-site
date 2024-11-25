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

# Float literals

```
5.0
```

## Details

Forge supports floating-point literals with:

* Binary, octal, decimal, and hexadecimal digits
* Optional underscores for readability
* Optional suffixes for for explicit types
* Scientific notation

Float literals are always of type `f64` unless specified otherwise.

## Rationale

These are all syntaxes that are widely expcted in modern langauges.

## Syntax

See [integer literals](integer.md), as the syntax for floats is based off of integers.

Floats have the same prefixes and digits as integers, and can also allow underscores for readability. They must contain a decimal point and there must be digits on either side.

Floats can also be suffixed with `f32` or `f64` to explicitly specify the type.

| Base | Regex |
| ---- | ----- |
| Binary | `0b[01]([01_]*[01])?\.[01]([01_]*[01])?(f32\|f64)?` |
| Octal | `0o[0-7]([0-7_]*[0-7])?\.[0-7]([0-7_]*[0-7])?(f32\|f64)?` |
| Decimal | `[1-9]([0-9_]*[0-9])?\.[0-9]([0-9_]*[0-9])?(e-?[0-9]([0-9_]*[0-9])?)?(f32\|f64)?` |
| Hexadecimal | `0x[0-9a-fA-F]([0-9a-fA-F_]*[0-9a-fA-F])?\.[0-9a-fA-F]([0-9a-fA-F_]*[0-9a-fA-F])?(f32\|f64)?` |

### Scientific notation

Floats can have a scientific notation suffix with an `e` followed by an optional `-` and a sequence of digits which represent the exponent. These digits are in the same base as the float itself. This is only supported for decimal floats.

## Examples

A simple decimal float:

```
5.0
```

A binary float (which equals `5.0` in decimal):

```
0b101.0
```

An octal float (which equals `5.0` in decimal):

```
0o5.0
```

A hexadecimal float (which equals `5.0` in decimal):

```
0x5.0
```

A more complicated hexadecimal float (which equals $5 + (16^{-1} * 15) + (16^{-2} * 9) + (16^{-3} * 6) + (16^{-4} * 10) \approx 5.9743$):

```
0x5.f96a
```

A float using scientific notation (which equals $5 * 10^{1} = 50$):

```
5.0e1
```

A float using scientific notation with a negative exponent (which equals $5 * 10^{-1} = 0.5$):

```
5.0e-1
```

A float with underscores for readability:

```
5_000.0
```

A float with a type suffix, which is a 32-bit float:

```
5.0f32
```

A float with a type suffix, which is a 64-bit float:

```
5.0f64
```
