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

# While loops

```
while x > 0 {
	// ...
}

do {
	// ...
} while x > 0;
```

## Details

While loops take a boolean expression and conditionally execute the code in the block repeatedly as long as the condition remains true. Do-while loops will always execute the block at least once before beginning to check the condition for future iterations.

## Rationale

This is a pretty standard while loop, so it should be comfortable for most programmers to use.

## Syntax

```ebnf
(* assume value and statement are defined elsewhere *)

statement-body = "{" { statement } "}";

while-loop = "while" value statement-body
		   | "do" statement-body "while" value ";";
```

## Examples

A simple while loop:

```
let x = 5;

while x > 0 {
	// ... (will be called 5 times)

	x--;
}
```

A simple do-while loop:

```
let x = 0;

do {
	// ... (will be called once)

	x--;
} while x > 0;
```
