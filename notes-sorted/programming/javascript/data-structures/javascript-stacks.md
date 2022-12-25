# Stacks

- Stacks are LIFO "last in first out"
- The newest element will be the first one removed (think a stack of plates)

## Benefit of Stacks

- Allow for constant-time&mdash;O(1)&mdash;adding and removing of **the top item**
- The top is O(1) because no items need to be shifted to access the first item in the stack
- Only the first item in the stack has constant time lookup

## Downside of Stacks

- Don't offer O(1) access to items that aren't on the top
- If we want the fourth item in the stack, we'd have to pop each item off the stack that is above it until we reach the fourth item
- If we want to access the **last item** in the stack, we'd have to pop everything off the stack to get to it. This is O(n), **linear time**

## Stack Methods

- `pop()`
	- Remove the top item from the stack
- `push(item)`
	- Add an item to the top of the stack
- `peek()`
	- Return the item at the top of the stack, **without removing it**
	- Peek at it, but leave it where it is
- `isEmpty()`
	- Return `true` if the stack is empty
- `get length()`
	- Return the number of items in the stack

## Class-based Stack

1. Create a class with one property in the constructor, the stack. We use an array to represent the stack.

```js
class Stack {
	constructor() {
		this.stack = [];
	}
}
```

2. Add the `get length()` getter method to the `Stack` class

```js
class Stack {
	constructor() {
		this.stack = [];
	}
	get length() {
		return this.stack.length;
	}
}
```

3. Add the `push` method to add an item to the top of the stack array. This method will take one argument, the item to add. Because the right side of the array is the top, we can use `Array.prototype.push`

```js
class Stack {
	constructor() {
		this.stack = [];
	}
	get length() {
		return this.stack.length;
	}
	push(item) {
		return this.stack.push(item);
	}
}
```

4. Add the `pop` method to remove the top element from the stack array. Because the right side of the array is the top, we can use `Array.prototype.pop`

```js
class Stack {
	constructor() {
		this.stack = [];
	}
	get length() {
		return this.stack.length;
	}
	push(item) {
		return this.stack.push(item);
	}
	pop() {
		return this.stack.pop();
	}
}
```

5. Add the `peek` method to check which element is at the top of the stack. Because the right side of the array is the top, we need to check what the last item is in the array.

```js
class Stack {
	constructor() {
		this.stack = [];
	}
	get length() {
		return this.stack.length;
	}
	push(item) {
		return this.stack.push(item);
	}
	pop() {
		return this.stack.pop();
	}
	peek() {
		return this.stack[this.length - 1];
	}
}
```

6. Add the `isEmpty` convenience method that checks whether the stack is empty. Could also skip the method and check if `this.stack.length === 0`, but this approach bakes that check into the stack class.

```js
class Stack {
	constructor() {
		this.stack = [];
	}
	get length() {
		return this.stack.length;
	}
	push(item) {
		return this.stack.push(item);
	}
	pop() {
		return this.stack.pop();
	}
	peek() {
		return this.stack[this.length - 1];
	}
	isEmpty() {
		return this.length === 0;
	}
}
```
