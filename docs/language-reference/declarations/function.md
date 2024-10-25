# Function declarations

- You can omit type hints

```
fn add(a, b) {
	return a + b;
}

fn add(a: int, b: int): int {
	return a + b;
}
```

## Arguments

Arguments’ passing method is relatively explicit.

| Passing method | Mutability | Syntax |
| --- | --- | --- |
| Pass-by-value | Mutable | `x: int` |
| Pass-by-value | Constant | `const x: int`, `x: const int` |
| Pass-by-move | Mutable | `move x: int` |
| Pass-by-move | Constant | `most const x: int`, `move x: const int` |
| Pass-by-reference | Mutable | `ref x: int`, `x: ref int` |
| Pass-by-reference | Constant | `ref const x: int`, `ref x: const int`, `x: ref const int` |