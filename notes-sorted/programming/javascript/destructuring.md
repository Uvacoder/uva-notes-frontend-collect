## Destructuring

We can unpack the variables out of an object or array using destructuring.

```
const person = {
    name: Karen,
    age: 42
}
```
can be destructured to:
```
const { name, age } = person

```
```
let a, b, rest;
[a, b] = [10, 20];

console.log(a);
// expected output: 10

console.log(b);
// expected output: 20

[a, b, ...rest] = [10, 20, 30, 40, 50];

console.log(rest);
// expected output: Array [30,40,50]
```
Destructuring can easily be spotted because unlike in an object or array literal expression the values are on the left of the assignment:

```
const [firstElement, secondElement] = list;
// is equivalent to:
// const firstElement = list[0];
// const secondElement = list[1];

```
This can be used for swapping variables in an array - maybe you need to sort it -
```
const arr = [1,2,3];
[arr[2], arr[1]] = [arr[1], arr[2]];
console.log(arr); // [1,3,2]
```
