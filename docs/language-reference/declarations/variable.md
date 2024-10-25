# Variable declarations

```
let x = 5;

let x: f64 = 5.3;

let x: const bool = false;
// OR
const x: bool = false;

let x: &bool = &x;
// OR
ref x: bool = &x;

opt ref x: bool

opt x: bool

ptr x: void



type IntPointer = ptr int;

// Linter warning
let x: pointer int = &y;

// Idiomatic
pointer x: int = &y;
```
