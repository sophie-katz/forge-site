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

# Variable declarations

```
let x = 5;
```

## Details

Variable declarations have an optional type and an optional initial value. If the type is not specified, the type is inferred from the initial value. If the initial value is not specified, the variable's type must be inferrable from its usage. Variables that are not initialized on declarations must be initialized before use - there are no default values in Forge.

## Syntax

```ebnf
(* assume type, identifier, and value are defined elsewhere *)

variable-declaration-prefix = "let" | type-modifier { type-modifier };

variable-declaration = variable-declaration-prefix
                       identifier
                       [ ":" type ]
                       [ "=" value ] ";"
                     ;
```

## Examples

A simple variable declaration. `x` will be of type `int` since that is the type of the integer literal `5`.

```
let x = 5;
```

A variable declaration with an explicit type. `x` will be of type `f64`.

```
let x: f64 = 5.3;
```

A variable declaration with a constant type. Both variants here are equivalent, but the second one is more idiomatic.

```
let x: const bool = false;
// OR
const x: bool = false;
```

A variable declaration with a reference type. Both variants here are equivalent, but the second one is more idiomatic.

```
let x: ref bool = &x;
// OR
ref x: bool = &x;
```

A variable declaration with multiple type modifiers and no initial value. Note that the variable does not have an initial value of `null` but has no initial value and must be initialized before use.

```
opt ref x: bool;
```
