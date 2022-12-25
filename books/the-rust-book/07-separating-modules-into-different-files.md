We can move the definition of the `front_of_house` module if we'd like, in order to reduce the apparent complexity of our code

From this:
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

To this: 
```rust
// src/lib.rs
mod front_of_house;

pub use crate::front_of_house::hosting;

pub fn eat_at_restaurant() {
    hosting::add_to_waitlist();
    hosting::add_to_waitlist();
    hosting::add_to_waitlist();
}

```

The semicolon after `mod front_of_house` , rather than starting a block, signifies to Rust that we want to load the contents of the `front_of_house` module from another file.

We move the `front_of_house` definition to a file with that name:
```rust
// src/front_of_house.rs
pub mod hosting {
	pub fn add_to_waitlist() {}
}
```

---

We can go even further, extracting the hosting module to its own file as well:
```rust
// src/front_of_house.rs
pub mod hosting;
```

And we move the definitions for the `hosting` module into its own file:
```rust
// src/front_of_house/hosting.rs
pub fn add_to_waitlist() {}
```

## Summary
- A package can be split into multiple crates
- A crate can be split into multiple modules
- Modules can be referred to with absolute or relative paths (like in a filesystem)
- Module paths can be brought into scope with the `use` statement
- Modules are private by default, but they can be made public with the `pub` keyword