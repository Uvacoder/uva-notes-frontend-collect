[[05-structs]]
- Similar to functions:
	- declared with `fn` keyword and their name
	- can have as many parameters as we'd like and a return value
- different in that:
	- they are defined within the context of a struct (or enum or trait object)
	- their first parameter is always `self`, which represents the instance of the struct the method is being called on (similar to `this` in JS?)

- Can also define **associated functions**
	- do not take `self` as a parameter
	- not methods, because they don't have an instance (`self`) of the struct to work with
	- often used for constructors that return a new instance of the struct
	- call **associated functions** with `::` syntax because the function is **namespaced by the struct**

Methods can take ownership of `self`, borrow `self` immutably (`&self`), or borrow `self` mutably (`&mut self`)

## Defining Methods
1. start with `impl` (implementation) block
2. define the function within the `impl` block like other functions
3. call the method using . syntax (`rectangle.area()`)

**Main benefit of using methods instead of regular functions is for organization. All the things we can do with a type are contained with an `impl` block instead of being potentially scattered throughout our code.**

Structs can have multiple `impl` blocks if required