# Strings

- `b` return the value as a byte array instead of a unicode string
- `r` (raw) do not escape backslashes or format strings
- Escape codes are `\a`, `\b`, `\e`, `\f`, `\n`, `\r`, `\t`, `\u{HHHH}`, `\v`, `\xHH`, `\oOOO`, `\0`, `\\`, `\?` where `?` is any character

```
"hello, world"

b"hello, world"

"all strings
are multiline by default"

#"this string can contain " characters "#

r"this string doesn't escape \ characters"

"{x} all strings are format strings by default"

p"use u to disable this"

bpr#"this string does not allow formatting or escapes and is returned as a byte array.

it is multiline and can contain " characters."#
```