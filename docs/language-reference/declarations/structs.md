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

# Struct declarations

```
struct MyStruct {
	a: int;
	b: int;
}
```

## Details

`struct` declares structs for compound data storage. Structs can have either variable or function declarations within themselves. They cannot have interface, struct, or type alias declarations within themselves.

!!! note

    Function declarations within structs must have bodies.

### Accessing members

Members of a struct can be accessed using the `.` operator.

```
struct MyStruct {
	member: int;

	fn method() {
		// ...
	}
}

let x: MyStruct = {member: 5};

let y: int = x.member;

x.method();
```

### Inheritance

Structs can inherit from other structs or interface. When a struct inherits from another struct it means that all of the members from the inherited struct are also present in the inheritee.

When a struct inherits from an interface, it must implement all of the members of the interface in order to be compliant with it.

```
interface MyInterface {
	a: int;
}

struct ParentStruct: MyInterface {
	a: int;
}

struct ChildStruct: ParentStruct {
	b: int;
}

let x: ChildStruct = {a: 5, b: 6};

struct MyStruct: MyOtherStruct, MyInterface {}
```

In the above example, since `ParentStruct` implements `MyInterface`, `ChildStruct` also implements `MyInterface`.

### Constant members

Constant variable members are those that do not change over the course of the structs lifetime. They are declared with the `const` keyword.

```
struct MyStruct {
	a: int;
	const b: int; // idiomatic
	// OR
	b: const int; // causes linter warning
}
```

Constant function members are those that do not mutate the struct in any way. They are also declared with the `const` keyword.

```
struct MyStruct {
	a: int;

	fn doesChangeValue() {
		self.a++;
	}

	const fn doesNotChangeValue() {
		// ...
	}
}

const x: MyStruct = {a: 5};

// This is ok
x.doesNotChangeValue();

// This is not
x.doesChangeValue(); // error because 'x' is const
```

### Move methods

You can also declare move methods which take ownership of the struct and destroy it after the function call. For example:

```
struct MyStruct {
	a: int;
	b: int;

	move fn takeSum(): int {
		return self.a + self.b;
	}
}

let x: MyStruct = {a: 1, b: 3};

let y = x.takeSum();

x.a; // will cause an error since 'x' has been moved into 'takeSum' and no longer exists
```

### Static members

Static members are those that are declared within the namespace of the struct but are not part of any instance of the struct.

Static variable members are essentially global variables that are namespaced within the struct. Similarly, static function members are essentially global functions that are namespaced within the struct.

```
struct MyStruct {
	static DEFAULT_A: int = 0;
	static DEFAULT_B: int = 0;

	a: int;
	b: int;

	static fn getDefault() -> MyStruct {
		return {
			a: DEFAULT_A,
			b: DEFAULT_B,
		};
	}
}
```

### Protection

Members of structs can have different levels of protection with the `private` and `protected` keywords. By default, members are public.

Private members are only accessible within the struct in which they are declared. They are not accessible either by calling code or by structs which inherit the struct in which they are declared.

Protected membersare only accessible within the struct in which they are declared and by structs which inherit the struct in which they are declared. They are not accessible by calling code.

```
struct ParentStruct {
	private a: int = 1;
	protected b: int = 2;
	c: int;
}

struct ChildStruct {
	fn method() {
		self.a; // will cause an error since 'a' is private
		self.b; // this is fine because 'b' is protected
		self.c; // this is fine because 'c' is public
	}
}

let x: ChildStruct = { c: 3 };

// This would cause an error since 'a' is private
// let x: ChildStruct = {a: 1, c: 3 };

// This would cause an error since 'b' is protected
// let x: ChildStruct = {b: 2, c: 3 };

x.a; // will cause an error since 'a' is private
x.b; // will cause an error since 'b' is protected
x.c; // this is fine because 'c' is public
```

### `self` and `Self`

To access the current instance of a struct, the `self` keyword is used. To access the type of the current instance of a struct, the `Self` keyword is used.

The `self` value is a reference to the current instance. In a mutable method it is a mutable reference, in a constant method it is a constant reference. In a move method it the value itself and not a reference.

`Self` is a simple shorthand for the type of the current instance.

!!! warning

    Add some detail about `Self` with generic types.

## Rationale

Structs are a common feature of modern programming languages so much developers should feel comfortable with them.

### Why `struct` and not `class`?

Structs historically imply that data within them is structured but is not necessarily fully encapsulated. Classes, on the other hand, are historically fully encapsulated. In Forge, although you can fully encapsulate your data and only allow access through tightly controlled methods, it's more idiomatic to use object literals and static methods instead of constructors and member access instead of getters and setters. There is also no implicit or behind-the-scenes actions that take place during construction or inheritance like there commonly is in traditional object-oriented programming.

There is definitely a lot of overlap between traditional classes and Forge structs, but the `struct` keyword and name is used here to imply to the developer that it is more closely related to the historical definition of a struct rather than a class.

### Why no constructors?

Constructors are not necessary in Forge because you can just use object literals to create instances of structs. This is idiomatic in many modern programming languages and is more explicit than using constructors.

If something like a constructor is actually needed, a static method can be used to create an instance of the struct.
