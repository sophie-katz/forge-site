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

# Comments

```
// This is a single-line comment

/* This is a
 * block comment
 * over multiple
 * lines.
 */
```

## Rationale

These are equivalent to the single-line and block comments in C. These were chosen because of how this syntax is across different languages and because developers will most likely be familiar with them.

## Documentation comments

Documentation comments are a special type of comment that is used to document the code. They are similar to block comments, but they have a special prefix: `/**`.

```
/**
 * This is a documentation comment.
 */
```

This documentation comment will be applied to the next declaration that follows it. This is useful for documenting functions, classes, and other declarations.

This syntax is similar to TypeScript's JSDoc comments. It was chosen for its wide usage and minimal impact on syntax.
