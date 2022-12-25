## [Strings](https://doc.rust-lang.org/book/ch08-02-strings.html#creating-a-new-string)

- Strings are dealt with in the section about collections because strings are implemented as a collection of bytes.

### [What Is a String?](https://doc.rust-lang.org/book/ch08-02-strings.html#what-is-a-string)

- Rust has one string type in the core language, the string slice
	- `str`
	- usually seen in borrowed form `&str`
	- UTF-8 encoded
- The `String` type is provided by Rust's standard library, and is a *growable, mutable, owned, UTF-8 encoded string type*
- When people refer to "Strings" in Rust, they usually mean the `String` and the string slice `&str` types.

### [Creating a New String](https://doc.rust-lang.org/book/ch08-02-strings.html#creating-a-new-string)

- Creating a new empty string:
```rust
let mut s = String::new();
```
- We can also call the `to_string` method on any type that implements the [`Display` trait](https://doc.rust-lang.org/std/fmt/trait.Display.html)
```rust
let data = "initial contents";
let s = data.to_string();

// Or the same thing on the literal directly
let s = "initial contents".to_string();
```
- The `String::from` function can also be used to create a `String` from a string literal
```rust
let s = String::from("initial contents");
```
- Because strings are UTF-8 encoded, any properly encoded data can be contained in a string
```rust
fn main() {
    let hello = String::from("السلام عليكم");
    let hello = String::from("Dobrý den");
    let hello = String::from("Hello");
    let hello = String::from("שָׁלוֹם");
    let hello = String::from("नमस्ते");
    let hello = String::from("こんにちは");
    let hello = String::from("안녕하세요");
    let hello = String::from("你好");
    let hello = String::from("Olá");
    let hello = String::from("Здравствуйте");
    let hello = String::from("Hola");
}

```

### [Updating a String](https://doc.rust-lang.org/book/ch08-02-strings.html#updating-a-string)

#### Appending to a String with `push_str` and `push`

- `push_str`
	- Appends a string slice to a `String`
	- Takes a string slice because we don't want to take ownership of the parameter
```rust
fn main() {
    let mut s1 = String::from("foo");
    let s2 = "bar";
    s1.push_str(s2);
    println!("s2 is {}", s2);
}
```
- `push`
	- Pushes a single character onto the end of a `String`
```rust
let mut s = String::from("lo");
s.push('l');
```

#### Concatenation with the `+` Operator or the `format!` Macro

- `+` operator
```rust
let s1 = String::from("Hello, ");
let s2 = String::from("world!");
let s3 = s1 + &s2; // s1 has been moved here and can no longer be used
```
- The signature of the method that's called when we use the `+` operator looks like this (really it's implemented with generics, this example is what it looks like with concrete String values substituted for the generics)
```rust
fn add(self, s: &str) -> String {}
```
- This is a little strange
	- `add` takes ownership of `s1` because according to the signature, `self == s1`
































