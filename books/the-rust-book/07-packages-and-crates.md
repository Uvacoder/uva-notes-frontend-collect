## Crates
- A crate is a binary or library
- All funcitonality of a crate is accessible via the crate's name
	- This enables bringing a crate's functionality into scope anywhere that its needed
- A package can have multiple binary crates
	- they live in `src/bin`
	- each file in `src/bin` will be a separate binary crate
- The *crate root* is the source file that the Rust compiler starts from
	- It makes up the root module of a crate
	-  `src/main.rs` is conventionally the crate root of a binary crate
	-  `src/lib.rs` is conventionally the crate root of a library crate
	-  Cargo passes the crate root files to `rustc` to build the library or binary
		-  `rustc` is the Rust compiler

## Packages
- A package is one or more crates that provide a set of functionality
- Packages contain:
	-  a `Cargo.toml` that describes how to build the crates in the package
	- it *must* contain zero or one library crates
	- it can contain many binary crates 

## [Defining Modules to Control Scope and Privacy](https://doc.rust-lang.org/book/ch07-02-defining-modules-to-control-scope-and-privacy.html#defining-modules-to-control-scope-and-privacy) 

### Modules

 - Modules are organizational, allowing for greater readability and easy reuse
 - Modules control the privacy of items (public or private)
	 - In other words, modules establish Rust's *privacy boundary* that delineates stuff that external code can't access
	 - All items are private by default in Rust
		 - The privacy is like scope: children have access to the parent context by default; parents do not have access to the child context by default
	 - We can expose private items with the `pub` keyword
 - Defined with `mod` keyword followed by the module name
 ```rust
 mod front_of_house {
 	// Code
 }
 ```
 - Modules can also contain other modules, structs, enums, functions, traits, constants
 ```rust
 mod front_of_house {
 	mod hosting {
		// Code
	}
	
	mod serving {
		// Code
	}
 }
 ```
 - Modules are organized in a tree-like structure, similar to a filesystem
	 - Have parent/child/sibling relationships
 
crate
  └── front_of_house
    ├── hosting
    │   ├── add_to_waitlist
    │   └── seat_at_table
    └── serving
         ├── take_order
         ├── serve_order
         └── take_payment

## [Paths for Referring to an Item in the Module Tree](https://doc.rust-lang.org/book/ch07-03-paths-for-referring-to-an-item-in-the-module-tree.html)

Paths can take two forms:
1. Absolute paths start from a crate root using a crate name or literal crate
2. Relative paths start from the current module using `self`, `super`, or an identifier in the current module

Either form separates identifiers with the `::` syntax

Using the above `add_to_waitlist` method as an example, we could call this in two ways:
```rust
// Absolute path
crate::front_of_house::hosting::add_to_waitlist();
```
or:
```rust
// Relative path
front_of_house::hosting::add_to_waitlist();
```
- In the **absolute path** example, we can think of `crate` as being equivalent to `/` in filesystem. It is the *crate root*
- In the **relative path** example, we can access `front_of_house` because it is defined in the same scope as our current module. We could achieve the same result by importing the module into scope with the `use` keyword

## [Exposing Paths with the `pub` Keyword](https://doc.rust-lang.org/book/ch07-03-paths-for-referring-to-an-item-in-the-module-tree.html#exposing-paths-with-the-pub-keyword)

Using the same example as above, we have to make both the `hosting` module *and* the `add_to_waitlist()` method public with the `pub` keyword before the code will compile:

```rust
mod front_of_house {
    pub mod hosting {
        pub fn add_to_waitlist() {}
    }
}

pub fn eat_at_restaurant() {
    // Absolute path
    crate::front_of_house::hosting::add_to_waitlist();

    // Relative path
    front_of_house::hosting::add_to_waitlist();
}

fn main() {}
```

`front_of_house` does not need to be declared `pub` because it is a sibling to `eat_at_restaurant` and shares the same context. Therefore it has access to the `eat_at_restaurant` method

## [Starting Relative Paths with `super`](https://doc.rust-lang.org/book/ch07-03-paths-for-referring-to-an-item-in-the-module-tree.html#starting-relative-paths-with-super)

We can also use the `super` keyword as part of our relative paths, which is the equivalent of `..` in filesystem syntax

```rust
fn serve_order() {}

mod back_of_house {
	fn fix_incorrect_order() {
		cook_order();
		super::serve_order();
	}
	
	fn cook_order() {}
}
```

If we are fairly certain that the relative parent-child relationship between `back_of_house` and `serve_order()` will remain the same, then using the `super` keyword allows us to keep the items coupled. This will reduce the amount of code we would have to change if we were to refactor

## [Making Structs and Enums Public](https://doc.rust-lang.org/book/ch07-03-paths-for-referring-to-an-item-in-the-module-tree.html#starting-relative-paths-with-super)

### Structs
- `pub` before a struct definition makes the struct public, but the struct's fields will still be private
- We can make the fields public on a case-by-case basis
- If a struct has a private field, we must provide an associated public function that constructs an instance of the struct (`summer()` in the book's example)
```rust
pub struct Breakfast {
	pub toast: String,
	seasonal_fruit: String,
}
```
Here we can modify the `toast` field, but the `seasonal_fruit` field is not exposed publicly

Full example from the book:
```rust
mod back_of_house {
    pub struct Breakfast {
        pub toast: String,
        seasonal_fruit: String,
    }

    impl Breakfast {
        pub fn summer(toast: &str) -> Breakfast {
            Breakfast {
                toast: String::from(toast),
                seasonal_fruit: String::from("peaches"),
            }
        }
    }
}

pub fn eat_at_restaurant() {
    // Order a breakfast in the summer with Rye toast
    let mut meal = back_of_house::Breakfast::summer("Rye");
    // Change our mind about what bread we'd like
    meal.toast = String::from("Wheat");
    println!("I'd like {} toast please", meal.toast);

    // The next line won't compile if we uncomment it; we're not allowed
    // to see or modify the seasonal fruit that comes with the meal
    // meal.seasonal_fruit = String::from("blueberries");
}
```

### Enums

- `pub` before an enum definition makes the enum and all of its variants public

## [Bringing Paths into Scope with the `use` Keyword](https://doc.rust-lang.org/book/ch07-04-bringing-paths-into-scope-with-the-use-keyword.html#bringing-paths-into-scope-with-the-use-keyword)

- The `use` keyword allows us to import modules into any scope
- `use` is similar to a sym-link in a filesystem
- You can bring items into scope using either absolute or relative paths

### [`use` Path Idioms](https://doc.rust-lang.org/book/ch07-04-bringing-paths-into-scope-with-the-use-keyword.html#creating-idiomatic-use-paths)

- When bringing functions into scope, always stop at the parent module to make clear that the function being used is not defined locally
```rust
// Yes
use crate::front_of_house::hosting;

// No
use crate::front_of_house::hosting::add_to_waitlist;
```
- When bringing in structs, enums, and other items: use the full path
```rust
// Yes
use std::collections::HashMap;

// No
use std::collections;
```
- The exception to this rule is when bringing two items with the same name into scope with `use` because the compiler will not allow that
	- This makes intuitive sense. In the example below, if we imported all the way to `Result`, how would the compiler know which `Result` we wanted to use?
```rust
use std::fmt;
use std::io;

fn function1() -> fmt::Result {}

fn function2() => io::Result {}
```

### [Provide New Names with `as` Keyword](https://doc.rust-lang.org/book/ch07-04-bringing-paths-into-scope-with-the-use-keyword.html#providing-new-names-with-the-as-keyword)

- We could also alias the `Result` using the `as` keyword. This is also idiomatic, we can do either
```rust
use std::fmt::Result;
use std::io::Result as IoResult;

fn function1() -> Result {}

fn function2() => IoResult<()> {}
```

### [Re-exporting with `pub use`](https://doc.rust-lang.org/book/ch07-04-bringing-paths-into-scope-with-the-use-keyword.html#re-exporting-names-with-pub-use)

- Re-exporting modules allow calling code to also take advantage of the path that is defined in the `use` statement
- I don't fully understand the import of this, will return to this topic

```rust
mod front_of_house {
    pub mod hosting {
        pub fn add_to_waitlist() {}
    }
}

pub use crate::front_of_house::hosting;

pub fn eat_at_restaurant() {
    hosting::add_to_waitlist();
    hosting::add_to_waitlist();
    hosting::add_to_waitlist();
}

fn main() {}

```

### [Using External Packages](https://doc.rust-lang.org/book/ch07-04-bringing-paths-into-scope-with-the-use-keyword.html#using-external-packages)
- External packages live at [crates.io](https://crates.io/)
- We can add external dependencies to the `Cargo.toml` file at the root of our project under the `[dependencies]` field
```rust
[dependencies]
rand = "0.5.5"
```
- This tells Cargo to download the `rand` package and any dependencies it has from crates.io
	- Note that we do not need to include the `std` library in our `Cargo.toml` file because it is shipped with the Rust language.
	- Also note that we still need to `use` the `std` library in packages to bring items into scope
- We then can import the package using the `use` statement to bring it into scope
```rust
use rand::Rng;
```

### [Nested `use` Path Lists](https://doc.rust-lang.org/book/ch07-04-bringing-paths-into-scope-with-the-use-keyword.html#using-nested-paths-to-clean-up-large-use-lists)

- When using multiple items defined in the same module, we can nest the `use` statement by specifying the common part of the path, followed by curly brackets
```rust
// No
use std::cmp::Ordering;
use std::io;
 
// Yes
use std::{cmp::Ordering, io};
```
- We can do the same thing if two modules share a sub-path, using the `self` keyword
```rust
// No
use std::io;
use std::io::Write;

// Yes
use std::io::{self, Write};
```

### [Glob `*` Operator](https://doc.rust-lang.org/book/ch07-04-bringing-paths-into-scope-with-the-use-keyword.html#the-glob-operator)

- We can use the `*` operator to bring **all** public items from a path into scope
```rust
use::std::collections::*;
```

[[07-separating-modules-into-different-files]]