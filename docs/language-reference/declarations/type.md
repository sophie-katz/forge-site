# Type declarations

- `type` declares type aliases like a variable declaration
    - `explicit` removes the ability for basic types to be implicitly cast
- `struct` declares structures for how data is stored
- `interface` declares requirements for structures
- `enum` declares an enum

```
type MyInt = int;

explicit type MyInt = int;

struct MyStruct {
	a: int;
	b: int;
}

interface MyInterface {
	fn sum(): int;
}

let myObject: MyInterface = {
	a: 5,
	b: 5,
	sum: fn () { return a + b; },
};

enum MyEnum {
  value1,
  value2,
}
```
