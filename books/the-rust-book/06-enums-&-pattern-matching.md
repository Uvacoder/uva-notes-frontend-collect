**Enums ** allow us to define a type by enumerating its possible **variants**
**Enum values can only be one of its variants**
**Enums allow us to group things together, allowing them to be used more easily (in functions, etc)**

Rust enums are most similar to *algebraic data types* in functional languages like F#, OCaml, Haskell

## [Defining Enums](https://doc.rust-lang.org/book/ch06-01-defining-an-enum.html#defining-an-enum)
```rust
enum IpAddressKind {
	V4,
	V6
}
```

Enums are namespaced under their identifier (`IpAddressKind` in the example above); we use the double-colon syntax to separate variants

```rust
let four = IpAddressKind::V4;
let six = IpAddressKind::V6;
```

This allows us to define funcionality that takes our enum as a type, allowing us to write a function that takes any variant of a specified enum:

```rust
fn route(ip_kind: IpAddressKind) {}

route(IpAddressKind::V4);
route(IpAddressKind::V6);
```

## [Attaching Data to Enums](https://doc.rust-lang.org/book/ch06-01-defining-an-enum.html#enum-values)
We can attach data to each enum variant directly:

```rust
enum IpAddressKind {
	V4(u8, u8, u8, u8),
	V6(String),
}
```

The variants are not required to hold the same types or the same amount of data

Can even use structs as the data type for each variant, [as the IpAddr defined in standard library does](https://doc.rust-lang.org/std/net/enum.IpAddr.html)

```rust
struct Ipv4Addr {
	// code
}

struct Ipv6Addr {
	// code
}

enum IpAddr {
	V4(Ipv4Addr),
	V6(Ipv6Addr),
}
```


## Attaching Methods to Enums

https://doc.rust-lang.org/rust-by-example/custom_types/enum.html#type-aliases

## [The Option Enum](https://doc.rust-lang.org/book/ch06-01-defining-an-enum.html#the-option-enum-and-its-advantages-over-null-values)
[Option spec](https://doc.rust-lang.org/std/option/enum.Option.html)
	
Option is an enum defined in the standard library; it encodes scenarios where a value could be something or it could be nothing
	
It is so common that it is included in the prelude; we don't need to bring it into scope explicitly
- The same is true for `Some` and `None`, we can use them without namespacing off of `Option`

**Rust doesn't have null values**, but it does use `Option<T>` to encode the presence or absence of a value

```rust
enum Option<T> {
	Some(T),
	None,
}
```

`Option<T>` != `T`, we can't use an `Option<T>` the same way we use a regular type, because is could possibly be `None`

This results in an error:
```rust
let x: i8 = 5;
let y: Option<i8> = Some(5);

let sum = x + y
```

To use `y` as an `i8` we must explicitly handle the `None` case

[[06-control-flow-match-operator]]