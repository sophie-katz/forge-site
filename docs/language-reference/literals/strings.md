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

# String literals

```
"hello, world"
```

## Details

String literals represent a sequence of characters. They begin and end with `"` characters.

They can also have these prefixes. Multiple prefixes may be put in sequence to apply them in combination:

- `b` return the value as a byte array instead of a unicode string
- `r` (raw) do not escape backslashes or format strings
- `d` use DOS-style newlines (`"\r\n"`) instead of UNIX-style (`"\n"`) for multiline strings

### Escape codes

You can use `\` followed by a sequence of characters to use an escape code. The following escape codes are supported:

- `\a` - equivalent to ASCII `0x07`
- `\b` - equivalent to ASCII `0x08`
- `\e` - equivalent to ASCII `0x1b`
- `\f` - equivalent to ASCII `0x0c`
- `\n` - equivalent to ASCII `0x0a`
- `\r` - equivalent to ASCII `0x0d`
- `\t` - equivalent to ASCII `0x09`
- `\u{HHHH}` - equivalent to a Unicode character where `HHHH` is the hexadecimal number value representing it
    - This may have any number of digits, but must be at least 1
- `\v` - equivalent to ASCII `0x0b`
- `\xHH` - equivalent to a byte where `HH` is the 2-digit hexadecimal number value
- `\oOOO` - equivalent to a byte where `OOO` is the 3-digit octal number value
- `\0` - equivalent to ASCII `0x00`
- `\?` where `?` is any character - it simply puts that character into the string as-is
    - `\\` is a form of this, which is equivalent to a single backslash
    - This is also commonly used for `\{` and `\}` to escape braces

### Format strings

All strings are format strings by default. This means that you can use `{...}` to insert expressions into the string. The expression must be implicitly convertible to a string.

For example:

```
"2+2 is {2 + 2}" // equivalent to "2+2 is 4"
```

Strings without any formatters should have no performance advantage over strings with the `r` prefix.

### Multiline strings

All strings are multiline by default, so this is allowed:

```
"First line
Second line" // this is equivalent to "First line\nSecond line"
```

Newline characters in these strings will always be UNIX style (`"\n"`) unless the `d` prefix is applied, then newlines will be DOS style (`"\r\n"`).

```
d"First line
Second line" // this is equivalent to "First line\r\nSecond line"
```

### Custom quotes

You can use `#` characters in addition to the quotes to make custom quotes. This is useful for strings that contain quotes.

```
#"this string can contain " characters"#

// This will cause an error
#"this string can contain "# characters"#
```

You can additionally add any valid symbol between the `#` and `"` characters to make the custom quote even more unique. Note that the symbols before and must be identical.

```
#mySymbol"this string can contain "# characters"mySymbol#

// This will cause an error
#mySymbol"this string can contain "mysymbol# characters"mySymbol#
```

## Rationale

These strings are relatively similar to those in Python and Rust, so people will be relatively familiar with them.

There are few cases where strings being format strings is actively not desired, so it is the default behavior.

## Examples

A simple string:

```
"hello, world"
```

A string that is a byte array instead of a unicode string:

```
b"hello, world"
```

A multiline string

```
"a

multiline

string" // this is equivalent to "a\n\nmultiline\n\nstring"
```

A string with `#` wrappers to allow unescaped `"` characters within the string:

```
#"this string can contain " characters "#
```

A raw string that doesn't escape characters:

```
r"this string doesn't escape \ characters"
```

A format string:

```
"{x} all strings are format strings by default"
```

A string with all features:

```
br#mySymbol"this string does not allow formatting or escapes and is
returned as a byte array.

it is multiline and can contain " characters."mySymbol#
```
