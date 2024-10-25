# Structure declarations

`struct` declares structures for how data is stored

```
struct MyStruct {
	a: int;
	b: int;
}
```

## Inheritance

```
struct MyStruct: MyOtherStruct, MyInterface {}
```

## Methods

```
struct MyStruct {
	a: int;
	b: int;
	
	fn sum(): int {
		return self.a + self.b;
	}
}
```

## Constant members

```
struct MyStruct {
	a: int;
	const b: int; // idiomatic
	// OR
	b: const int; // linter warning
	
	fn doesChangeValue() {
		self.a++;
	}
	
	const fn doesNotChangeValue() {
		
	}
	
	static fn slfkjsdf() {}
}

const x: MyStruct = ...;

// This is OK
x.doesNotChangeValue();

// This is not
x.doesChangeValue(); // error because 'x' is const
```

## Static members

```
struct MyStruct {
	static DEFAULT_A: int = 0;
	static DEFAULT_B: int = 0;

	a: int;
	b: int;
	
	fn getDefault() -> MyStruct {
		return {
			a: DEFAULT_A,
			b: DEFAULT_B,
		};
	}
}
```
