# Queues

- Queues are FIFO "first in first out"
- The oldest element will be the first one removed
	- Think a restaurant cooking meal courses&mdash;the first course must be sent before the second course, etc.

## Benefit of Queues

- Useful for search algorithms (like BFS for trees)
- Can be used as a cache implementation
- Adding to the back of the queue is O(1) because no items need to be moved to access the back of the queue
- The front of the queue is O(1) because no items need to be moved to access the first item

## Downside of Queues

- Trickier than stacks to implement because we add to the back of the queue and remove from the front
- Like stacks, accessing items that aren't at the front of the queue take O(n) time in the worst case

## Queue Methods

- `enqueue(item)`
	- Add an item to the back of the queue. We can use the `Array.prototype.push` method to achieve this
- `dequeue()`
	- Remove the first item from the front of the queue. We can use the `Array.prototype.unshift` method to achieve this
- `peek()`
	- Return the item at the front of the queue **without removing it**
- `isEmpty()`
	- Return `true` if the queue is empty
- `get length()`
	- Return the number of items in the queue

## Class-based Queue

1. Create a class with one property in the constructor, the queue. We use an array to represent the queue. The left side of the array represents the front of the queue. The right side of the array represents the back of the queue.

```js
class Queue {
	constructor() {
		this.queue = [];
	}
}
```

2. Add the `get length()` method to the `Queue` class.

```js
class Queue {
	constructor() {
		this.queue = [];
	}
	get length() {
		return this.queue.length;
	}
}
```

3. Add the `enqueue` method to add an item to the back of the queue (the right side of the `queue` array).

```js
class Queue {
	constructor() {
		this.queue = [];
	}
	get length() {
		return this.queue.length;
	}
	enqueue(item) {
		this.queue.push(item);
	}
}
```

4. Add the `dequeue` method which will remove and return the item at the front of the queue (the left side of the `queue` array).

```js
class Queue {
	constructor() {
		this.queue = [];
	}
	get length() {
		return this.queue.length;
	}
	enqueue(item) {
		this.queue.push(item);
	}
	dequeue() {
		return this.queue.unshift();
	}
}
```

5. Add the `peek()` method to check which item is at the front of the queue. Because we're using an array, this is the item at index 0.

```js
class Queue {
	constructor() {
		this.queue = [];
	}
	get length() {
		return this.queue.length;
	}
	enqueue(item) {
		this.queue.push(item);
	}
	dequeue() {
		return this.queue.unshift();
	}
	peek() {
		return this.queue[0];
	}
}
```

6. Add the `isEmpty()` convenience method to check whether the queue is empty. This method could be skipped, and we could just check if `this.queue.length === 0`, but this method bakes that check into the class.

```js
class Queue {
	constructor() {
		this.queue = [];
	}
	get length() {
		return this.queue.length;
	}
	enqueue(item) {
		this.queue.push(item);
	}
	dequeue() {
		return this.queue.unshift();
	}
	peek() {
		return this.queue[0];
	}
	isEmpty() {
		return this.queue.length === 0;
	}
}
```