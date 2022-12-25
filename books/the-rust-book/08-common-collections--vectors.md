## Vectors `Vec<T>`
- Vectors store multiple values in a single data structure that occupies contiguous memory
- Vectors can only store values of the same type (that's that the `T` means)

### Creating a New Vector
- To create a new empty vector (in this instance to hold `i32` values):
```rust
let v: Vec<i32> = Vec::new();
```
- We must add the type annotation here because there is no value in the vector for the compiler to infer a type from
- In most common situations, vectors are provided with initial values, enabling the compiler to infer the vector's type
	- The `vec!` macro helps with this, creating a new vector with the values provided:
```rust
let v = vec![1, 2, 3];
```

### Updating a Vector
- We use the `push` method to add values to a vector
- Variables referring to vectors must also be declared as mutable in order to change the value
```
let mut v = Vec::new();

v.push(5);
v.push(6);
v.push(7);
v.push(8);
```

### Dropping a Vector Drops Its Elements
- As with all `structs`, when a vector goes out of scope its values are dropped
```rust
{
	let v = vec![1, 2, 3, 4]
	// we can do stuff with v here
} // <-- v goes out of scope and its values are dropped beyond this point
```

### Reading Vector Elements
- There are two ways to read vector elements:
1. Using `&` and `[]`, which returns a reference
2. Using `get`, which returns an `Option<&T>`
```rust
let v = vec![1, 2, 3, 4, 5];

let third: &i32 = &v[2]; // <-- accessed with bracket notation using the value's index (this returns a reference)
println!("The third element is {}", third);

match v.get(2) { // <-- accessed with .get() using the value's index (this returns an Option<&T>)
	Some(third) => println!("The third element is {}", third),
	None => println!("There is no third element")
}
```
- The first method (`&v[2]`) will cause the program to panic when attempting to access values that are out of the vector's bounds
	- Use this method if you want the program to crash if there's an attempt to access elements past the end of the vector
- The second method (`v.get(2)`) will not cause the program to panic, but will return `None` if the value is not found / is beyond the vector's bounds
	- Use this method if you don't want the program to crash if there's an attempt to access elements past the end of the vector
- Once the program is sure that the references are valid, the borrow checker enforeces ownership and borrowing rules
	- This means that we can't have a mutable and immutable reference in the same scope:
```rust
let mut v = vec![1, 2, 3, 4, 5]

let first = &v[0] // <-- this is an immutable borrow

v.push(6) // <-- this is a mutable borrow, causing the code to error at compile
```

### Iterating Over Vector Values
- We can iterate over vectors with a `for` loop
	- This example gets immutable references to each element and prints them:
```rust
let v = vec![100, 32, 57]

for i in &v {
	println!("{}", i);
}
```
- We can also iterate over mutable references in a mutable vector to make changes to each element:
	- To change the value the the mutable reference refers to, we use the dereference operator `*` which will be covered in [[15-smart-pointers]]
```rust
let mut v = vec![100, 32, 57]

for i in &mut v {
	*i += 50;
}
```

### Using an Enum to Store Multiple Types
- While we can't directly store different types in a vector, the variants of an enum ([[06-enums-&-pattern-matching]]) are defined under the same enum type, so if we need to use different values in a vector we can define and use an enum
- This approach requires that we know ahead of time the exhaustive list of types the code will get at runtime to store in the vector
	- If we don't know this information ahead of time, we can use a trait object [[17-object-oriented-programming-features-of-rust]]
```rust
enum SpreadsheetCell {
	Int(i32),
	Float(f64),
	Text(String),
}

let row = vec![
	SpreadsheetCell::Int(3),
	SpreadsheetCell::Text(String::from("blue")),
	SpreadsheetCell::Float(42.12),
];
```
- I think the type for this vector would be `Vec<SpreadsheetCell>`



















