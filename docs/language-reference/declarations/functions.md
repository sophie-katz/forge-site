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

# Function declarations

```
fn add(a: int, b: int): int {
	return a + b;
}
```

## Details

Functions take a number of positional arguments and optionally return a value. Arguments have type hints that can optionally be omitted. The return type can also optionally be omitted.

!!! warning

    This section about omitted type hints needs more details.

The syntax for arguments is essentially equivalent to the syntax for variable declaration except without the `let` keyword.

### Arguments

There is a decent amount of complexity in how arguments are handled.

#### Passing behavior

Arguments’ passing method is relatively explicit.

| Passing method    | Mutability | Syntax                                                     |
| ----------------- | ---------- | ---------------------------------------------------------- |
| Pass-by-value     | Mutable    | `x: int`                                                   |
| Pass-by-value     | Constant   | `const x: int`, `x: const int`                             |
| Pass-by-move      | Mutable    | `move x: int`                                              |
| Pass-by-move      | Constant   | `move const x: int`, `move x: const int`                   |
| Pass-by-reference | Mutable    | `ref x: int`, `x: ref int`                                 |
| Pass-by-reference | Constant   | `ref const x: int`, `ref x: const int`, `x: ref const int` |

- **Pass-by-value** means that the value provided to the function when calling is cloned before the value is used within the function body. This is usually ideal for values which take up a small number of bytes such as integers or floats.

- **Pass-by-move** means that the function takes ownership of the value provided to it by the calling code. After the function call, the value can no longer be used in the calling code as its ownership has moved. This is the most efficient method and is ideal for larger values such as structs, strings, or arrays.

- **Pass-by-reference** means that the function is given a reference to the value provided to it by the calling code. This means that the function can access the value in place and the changes will be reflected in the calling code. This is ideal for values that are large or that need to be modified.

- **Mutability** - If a value is mutable, that simplify means that the value can be modified within the function. For pass-by-value and pass-by-move this just means that the value is declared mutable in the function body and has no impact on the calling code. For pass-by-reference this means that the value from the calling code will be implicitly modified in the function.

#### Default argument values

To make a function argument optional, you can use any of these syntaxes:

```
// b is optional and can be null
fn incrementOptional(a: int, opt b: int): int {
	return a + b ?? 1;
}

// This is functionally identical, but less idiomatic
fn incrementOptional(a: int, b: opt int): int {
	return a + b ?? 1;
}

// b is optional and defaults to 1
fn incrementDefault(a: int, b: int = 1): int {
	return a + b;
}
```

You can call `incrementOptional` using this syntax:

```
incrementOptional(5, null); // this equals 6

incrementOptional(5, 2); // this equals 7
```

Note how you still have to provide a parameter no matter what, even if it's `null`. `incrementDefault` can be called differently:

```
incrementDefault(5); // this equals 6

incrementDefault(5, 2); // this equals 7

incrementDefault(5, null); // this will cause an error
```

If you want to provide a default value for a parameter that is optional you still can:

```
fn incrementOptionalDefault(a: int, opt b: int = null): int {
	return a + b ?? 1;
}
```

This is functionally identical to `incrementDefault`:

```
incrementOptionalDefault(5); // this equals 6

incrementOptionalDefault(5, 2); // this equals 7

incrementOptionalDefault(5, null); // this will cause an error
```

All default arguments must come after all non-default arguments.

```
fn f(a: int, b: int = 5) { // this is fine
	// ...
}

fn f(a: int, b: int = 5, c: int) { // this will cause an error
	// ...
}
```

### Overloading

You can declare the same function multiple times as long as the argument types or count are unique between all of the declarations. The return type can differ between the declarations.

```
fn add(a: int, b: int): int {
	return a + b;
}

fn add(a: f64, b: f64): f64 {
	return a + b;
}
```

## Rationale

Most of these features are standard in modern programming languages, so they should be comfortable for most programmers to use.

Keyword arguments are not supported because they tend to lead to very complex function calls with many arguments. Function calls with many arguments can also be achieved by passing in an options object which is idiomatic in TypeScript. If keyword arguments are allowed as well, there is then two different ways of passing in complex data into functions and objects have more functionality than keyword arguments anyway.

Multiple returns are also not supported because the tuple type exists and can be used to achieve the same functionality without adding additional language features.

## Examples

A fully-typed function:

```
fn add(a: int, b: int): int {
	return a + b;
}
```

A function with type hints omitted:

```
fn add(a, b) {
	return a + b;
}
```

A function with an optional argument:

```
fn increment(a: int, opt b: int): int {
	return a + b ?? 1;
}
```
