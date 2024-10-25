# Interface declarations

`interface` declares requirements for structures

```
interface MyInterface: MyOtherInterface {}

interface MyInterface {
	fn sum(): int;
}

let myObject: MyInterface = {
	a: 5,
	b: 5,
	sum: fn () { return a + b; },
};
```
