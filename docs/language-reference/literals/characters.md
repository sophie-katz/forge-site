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

# Character literals

```
'A'
```

## Details

Character literals are exactly equivalent to string literals, except that they use `'` quotes instead of `"` quotes and they can only be exactly one grapheme cluster long.

Characters with the `b` prefix must be exactly one byte long.

Formatters are not allowed in character literals.

## Examples

A simple character literal:

```
'A'

// This will cause an error
'AB'

// So will this
''
```

A character literal with a byte prefix:

```
b'A'

// This will cause an error because it is more than one byte long
b'私'

// This will not because it is one single grapheme cluster
'私'
```
