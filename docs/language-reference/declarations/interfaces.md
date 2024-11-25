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

# Interface declarations

```
interface MyInterface {
	fn sum(): int;
}

let myObject: MyInterface = {
	a: 5,
	b: 5,
	sum: fn () { return a + b; },
};
```

## Details

`interface` declares requirements for structs and struct values. Interfaces can have either variable or function declarations within themselves. They cannot have interface, struct, or type alias declarations within themselves.

Function declarations for methods within interfaces can optionally not have a body if they need to be implemented by the inheriting struct or interface. If functions have bodies that means that the function will be declared as is on any implementing structs.

### Inheritance

Interfaces can inherit from other interfaces. They cannot inherit from structs. When an interface inherits from another interface it means that all of the members from the inherited interface are also present in the inheritee.

Interfaces do not need to implement all of the members of the inherited interface. Any that are not implemented are simply added to the interface as-is. They can, however, implement methods in inherited interfaces by providing bodies.

```
interface Sum {
	fn sum(): int;
}

interface TwoInts: Sum {
	a: int;
	b: int;

	fn sum(): int {
		return self.a + self.b;
	}
}
```

### Protection

Interface members cannot have private or protected access modifiers. They are always public.

### `self` and `Self`

`self` and `Self` are usable within interfaces and have the same definitions as within structs.

## Rationale

Interfaces are a common feature in many programming languages and most developers will be comfortable with them.
