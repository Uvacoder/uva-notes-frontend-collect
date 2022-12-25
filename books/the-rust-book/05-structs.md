- The pieces of a struct can be different types

- We name each piece of data so it's clear what the values mean

- Structs are more flexible than tuples: you don't have to rely on the order of the data to specify or access the values of an instance

- Structs do not implement `Display` trait by default, so we can't log their contents using the `println!()` macro, unless we use the `{:?}` debug trait (or `{:#?}` for pretty-print)

- To define a struct:
	- keyword `struct`
	- name of struct (should describe the siginificance of the pieces of data being grouped together)
	- inside curly braces, define the names and types of the pieces of data
		- these are called **fields**
```rust
struct User {
	username: String,
	email: String,
	sign_in_count: u64,
	active: bool,
}
```

- To use a struct after defining it:
	- Create an *instance* of the struct by specifying values for each **field**
		- state the name of the struct
		- curly brackets containing `key: value` pairs
			- keys are names of fields
			- values are the data that we want to store (of the originally specified type)
		- fields do not need to be specified in the same order as the struct definition
```rust
let user1 = User {
	email: String::from("someone@example.com"),
	username: String::from("someusername123"),
	active: true,
	sign_in_count: 1,
};
```

- To get specific value from a struct:
	- use dot notation
	- `user1.email` == `"someone@example.com"`
	- if the instance is mutable, we can change the value using dot notation to assign into a field
```rust
let mut user1 = User {
	email: String::from("someone@example.com"),
	username: String::from("someusername123"),
	active: true,
	sign_in_count: 1,
};

user1.email = String::from("anotheremail@example.com");
```
- The entire instance must be mutable to assign a field, we can't just mark individual fields as mutable

-  Functions can return instances of structs (almost like constructor functions?)
```rust
fn build_user(email: String, username: String) -> User {
	User {
		email: email,
		username: username,
		active: true,
		sign_in_count: 1,
	}
};
```

- Can also use "field init shorthand" when function arguments and struct fields share the same name (like in JS):
```rust
fn build_user(email: String, username: String) -> User {
	User {
		email,
		username,
		active: true,
		sign_in_count: 1,
	}
};
```

- Can use "struct update syntax" (like javascript spread) to create a new instance of a struct that uses most of an old instance's values, but changes some:
```rust
let user2 = User {
	email: String::from("a_new_one@example.com"),
	username: String::from("new_user"),
	active: user1.active,
	sign_in_count: user1.sign_in_count,
};
```
==
```rust
let user2 = User {
	email: String::from("a_new_one@example.com"),
	username: String::from("new_user"),
	..user1
};
```

- Can define **tuple structs** that have the added meaning of a struct name but don't have names associted with the fields, just the types
	- useful when you want to give a tuple a name, and declare it as a different type from other tuples, but naming each field would be too verbose or redundant
	- tuple struct instances behave like tuples:
		- you can destructure them into individual pieces
		- can use `.` followed by the index to access an individual value
```rust
struct Color(i32, i32, i32);
struct Point(i32, i32, i32);

let black = Color(0, 0, 0);
let origin = Point(0, 0, 0);
```

- `black` and `origin` are *different types* because they're instances of different tuple structs
- Each struct defined is a separate type, even if the fields have identical types

[[05-struct-method-syntax]]