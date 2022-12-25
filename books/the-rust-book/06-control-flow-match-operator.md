[[06-enums-&-pattern-matching]]

## Match Operator
`match` is a control flow operator that allows us to compare a value against a series of patterns and then execute code based on which pattern matches

Example `match` statement:

```rust
enum Coin {
	Penny,
	Nickel,
	Dime,
	Quarter
}

fn value_in_cents(coin: Coin) -> u8 {
	match coin {
		Coin::Penny => 1,
		Coin::Nickel => 5,
		Coin::Dime => 10,
		Coin::Quarter => 25,
	}
}
```

`match` is different from `if/else` in that it doesn't require a boolean expression, you can match on any expression type

Each branch of the `match` statement is called an arm

Arms have two parts separated by the `=>` operator:
1. a pattern (`Coin::Penny`)
2. some code to run if matched (`1`)

## Patterns That Bind To Values

Match arms can bind to the parts of the values that match the pattern, **allowing us to extract values out of enum variants**

```rust
enum UsState {
	Alabama,
	Alaska,
	Arkansas,
	// etc...
}

enum Coin {
	Penny,
	Nickel,
	Dime,
	Quarter(UsState),
}

fn value_in_cents(coin: Coin) -> u8 {
    match coin {
        Coin::Penny => 1,
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter(state) => {
            println!("State quarter from {:?}!", state);
            25
        }
    }
}
```

As an example, if we passed `value_in_cents` the value `Coin::Quarter(UsState::Alaska)` we would print the innter state `Alaska` from the enum variant of `Coin::Quarter(UsState)`

## Matching With `Option<T>`

`match` allows us to deal with the potential `None` value in `Option<T>` types

```rust
fn plus_one(x: Option<i32>) -> Option<i32> {
	match x {
		None => None,
		Some(i) => Some(i + 1),
	}
}

let five = Some(5);
let six = plus_one(five); // returns Some(6)
let none = plus_one(None) // returns None
```

Here we match against the `Option<T>` enum, bind a variable to the data inside (`i`), and then execute code based on that data (`i + 1`)

## Matches Are Exhaustive

We have to cover every last possibility in order for the code to compile

In the case of `Option<T>`, being forced to explicitly handle the `None` case saves us from assuming that we have a value when we might not

This won't compile because we haven't handled the `None` case:
```rust
fn plus_one(x: Option<i32>) -> Option<i32> {
	match x {
		Some(i) => Some(i + 1),
	}
}
```

## The `_` Placeholder

`_` acts as a catch-all for the remaining potential values in a `match` statement

In this example, we only care about the values 1, 3, 5, and 7, but a `u8` has all the values from 0 to 255. We can use `_` to match the rest of the values that we don't care about

```rust
let some_u8_value = 0u8;

match some_u8_value {
	1 => println!("one"),
	3 => println!("three"),
	5 => println!("five"),
	7 => println!("seven"),
	_ => (),
}
```

`_` matches any value, so make sure that it is the last arm of the `match` statment or it will shadow everything below it

`()` is the unit value, so nothing happens in the `_` arm

## if let Syntax

`match` statements are exhaustive: they must deal with every possible branch explicitly.

`if let` syntax allows us to deal with just one possible branch and *do something* if that branch evaluates to true

Rather than this:
```rust
let some_u8_value = Some(0u8);
match some_u8_value {
	Some(3) => println!("three!");
	_=> (),
}
```

We can do this:
```rust
if let Some(3) = some_u8_value {
	println!("three!");
}
```

We can also use an `else` clause with `if let` to explicitly handle the `_` case from `match` statements

```rust
if let Some(3) = some_u8_value {
	println!("three!");
} else {
	println!("not three!");
}
```