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

# If statements

```
if x > 0 {
	// ...
}
```

## Details

If statements take a boolean expression and conditionally execute the code in the block only if the expression is true. There are also else statements and else-if statements as part of this statement.

An example of an else statement:

```
if x > 0 {
	// ...
} else {
	// ...
}
```

An example of an else-if statement:

```
if x > 0 {
	// ...
} else if x < 0 {
	// ...
} else {
	// x == 0 in this case
	// ...
}
```

Else and else-if statements cannot exist on their own without an if statement. You can chain multiple else-if statements together, but only one else statement is allowed.

## Rationale

This is a pretty standard if statement, so it should be comfortable for most programmers to use.

## Syntax

```ebnf
(* assume value and statement are defined elsewhere *)

statement-body = "{" { statement } "}";

else-statement = "else" statement-body;

else-if-statement = "else" "if" value statement-body;

if-statement = "if" value statement-body
             { else-if-statement }
		     [ else-statement ];
```
