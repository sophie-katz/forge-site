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

# Scope

These are the different types of scopes within Forge. They are always represented by a block of code which is wrapped in curly braces `{` and `}`.

- [Declaration scope](#declaration-scope)
- [Statement scope](#statement-scope)
- [Function/statement body](#functionstatement-body)

## Declaration scope

The declaration scope is used for the global scope and declaration bodies, like structs and interfaces.

```
// In example.frg

// <-- this is declaration scope (global)

struct MyStruct {
    // <-- this is declaration scope (struct body)
}

fn main() {
    // <-- this is NOT declaration scope, but statement scope (function body)
}
```

Only declarations are allowed in this scope. For example, these are allowed:

- Function declarations
- Struct declarations
- etc.

But these are not allowed:

- Statements
- Expressions
- etc.

You cannot create nested scopes within the a declaration scope using `{` and `}`:

```
// In example.frg

// This is allowed
fn main() {
    // ...
}

// This is NOT allowed
{
    fn privateFunction() {
        // ...
    }
}
```

## Statement scope

This scope is used for function and statement bodies, like `if` and `while`.

```
// In example.frg

// <-- this is not statement scope, but declaration scope (global)

fn main() {
    // <-- this is statement scope (function body)

    // ...

    if (x) {
        // <-- this is statement scope (if body)
    }
}
```

Some declarations are allowed in this scope. For example:

- Variable declarations
- Function declarations

But all others are not allowed. For example:

- Struct declarations
- Type alias declarations
- etc.

All statements are allowed in this scope.

You can create nested scopes within a statement scope using `{` and `}`:

```
fn main() {
    let x = 5;

    {
        let y = 10;
    }

    y = 15; // this will cause an error because 'y' is private to the nested scope
    x = 10; // this is allowed
}
```

### Rationale

Functions are allowed in statement scope because you can just as easily define a function using a lambda expression and a variable. Simply allowing function declarations will let people use a simpler syntax to achieve the same thing.
