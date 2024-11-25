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

# Enum declarations

```
enum MyEnum {
  value1,
  value2,
}
```

## Details

Enum declarations define a new enumeration type with a set of possible values. Each value is a unique identifier that can be used to represent a specific option.

By default, enums are purely symbolic and cannot be cast to any other data type. For example, unlike C they cannot be converted to an integer implicitly and unlike idiomatic TypeScript they cannot be converted to a string implicitly. You can specify for this to be possible, though.

### Integer enums

```
enum MyEnum: int {
  value1,
  value2,
}

let x = MyEnum.value1 as int; // x is now 0

x = MyEnum.value2 as int; // x is now 1
```

Integer enums implicitly convert to integers. The first value is 0, the second is 1, and so on. If you specify a value for a member and do not specify a value for the following member, it will always take the next greatest integer value. For example:

```
enum MyEnum: int {
  value1 = 5,
  value2, // value2 is 6
}
```

If you attempt to have two members with the same value, the compiler will raise an error.

```
enum MyEnum: int {
  value1 = 5,
  value2 = 5, // this will cause an error
}
```

This behavior will work with any [basic integer type](../types/basic.md).

### String enums
