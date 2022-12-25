## Variables and Mutability

- Variables are immutable by default
- Use the `mut` keyword to mark a variable as mutable
- Initialized with the `let` keyword

### Constants

- Naming convention is to use all-caps and snake-case
	- `RUST_CONSTANT_CONVENTION`
- Not allowed to use `mut` with constants, they are *always* immutable
- The type of constants must be annotated
- Can be declared in global scope
- Can only be set to constant values, not the result of function calls or anything else that that is computed at runtime
	- The compiler must know the value of a constant while compiling

### Shadowing

- Defining a variable again with the `let` keyword shadows the initial value
- This allows us to perform a few transformations on a value, without marking the value as mutable with `mut`
- Also allows us to change the type of a variable without changing the name

## Data Types

-   