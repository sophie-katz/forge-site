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

# Type aliases

```
type MyInt = int;
```

## Details

Type aliases allow you to create a new symbol which represents an existing type.

### Explicit type aliases

Type aliases are usually exactly equivalent to their underlying type and can be implicitly casted to and from that type. You can disable this behavior by using the `explicit` keyword.

For example, this type may be implicitly casted:

```
type MyInt = int;

let x: int = 5;

let y: MyInt = x; // cast from int -> MyInt

let z: int = y; // cast from MyInt -> int
```

But with the `explicit` keyword, this will now cause errors:

```
explicit type MyInt = int;

let x: int = 5;

let y: MyInt = x; // this will cause an error

let z: int = y; // this will cause an error
```

## Syntax

```ebnf
(* assume type and identifier are defined elsewhere *)

type-alias-declaration = [ "explicit" ] "type" identifier "=" type ";"
```
