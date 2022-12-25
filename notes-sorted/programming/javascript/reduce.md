# JavascriptNotes

A place to store tidbits of javscript that I use all the time.

### Reduce Method

The reduce method takes the following syntax:
```
let arr = [];
arr.reduce(callback(acc, curVal, index, src), initVal); 
```

##### Parameters:
```
Accumulator (acc)
Current Value (curVal)
Current Index (index)
Source Array (src)
Initial Value (initVal)
Accumulator | required: This is the accumulated value previously returned from the function or the initial value if it was supplied.
Current Value | required: This is the value of the current element in the array.
Current Index | optional: This is the index of the current element in the array.
Source Array | optional: This is the array object reduce() was called upon.
Initial Value | optional: This is the initial value to be passed to the function. If no initial value is supplied, the first element in the array will be used as the initial accumulator value and the second element becomes the current value
```

##### Examples
```
const euros = [29.76, 41.85, 46.5];

const sum = euros.reduce((total, amount) => total + amount); 

sum // 118.11
In this example the total is the first element of the array and acts as an accumulator, the amount is each value iterated over until each value of the array is added together. 
```
The above example is written in ES6 and is the same as the ES5 
```
var euros = [29.76, 41.85, 46.5]; 

var sum = euros.reduce( function(total, amount){
  return total + amount
}, 0);

sum // 118.11

// Notice that 0 after the curlies but before the outer round bracket? That is the initial value - we don't normally use it if it is 0, because that is the default - but it can come in handy if we want to use reduce to perform other operations such as filter/map
```
You don't always have to return a single value! You can use the reduce function to manipulate each element and return them in a new array.

Here it is moonlighting as a **Map** method

```
const euros = [29.76, 41.85, 46.5];

const doubled = euros.reduce((total, amount) => {
  total.push(amount * 2);
  return total;
}, []);
```
Here we are passing an empty array as the initial value, so we will push the reduce values into that unamed array! This **Reduce** function is **Bananas**

We can use it to **Filter**! GET IN!

```
const euro = [29.76, 41.85, 46.5];

const above30 = euro.reduce((total, amount) => {
  if (amount > 30) {
    total.push(amount);
  }
  return total;
}, []);
```
You thought creating a new array was amazing? Reduce can take an empty object as a start value!
```
const fruitBasket = ['banana', 'cherry', 'orange', 'apple', 'cherry', 'orange', 'apple', 'banana', 'cherry', 'orange', 'fig' ];

const count = fruitBasket.reduce( (tally, fruit) => {
  tally[fruit] = (tally[fruit] || 0) + 1 ;
  return tally;
} , {})

count // { banana: 2, cherry: 3, orange: 3, apple: 2, fig: 1 }
```
We have tallied how many times each element is in the array!

We can also use reduce to flatten an array or get items from inside a nested array...
```
const data = [[1, 2, 3], [4, 5, 6], [7, 8, 9]];

const flat = data.reduce((total, amount) => {
  return total.concat(amount);
}, []);

flat // [ 1, 2, 3, 4, 5, 6, 7, 8, 9 ]
```
Can you see what happened there? We passed in that old empty array for our start point, then concatenate the current values to the total!
Here we will extract info from an array of objects -
```
const data = [
  {a: 'happy', b: 'robin', c: ['blue','green']}, 
  {a: 'tired', b: 'panther', c: ['green','black','orange','blue']}, 
  {a: 'sad', b: 'goldfish', c: ['green','red']}
];

const colors = data.reduce((total, amount) => {
  amount.c.forEach( color => {
      total.push(color);
  })
  return total;
}, [])

colors //['blue','green','green','black','orange','blue','green','red']
```
Or if we need them to be unique numbers, we can just check to see if they are already in the array before pushing the value in there:
```
const uniqueColors = data.reduce((total, amount) => {
  amount.c.forEach( color => {
    if (total.indexOf(color) === -1){
     total.push(color);
    }
  });
  return total;
}, []);

uniqueColors // [ 'blue', 'red', 'green', 'black', 'orange']
```
We can even use reduce to map over an array of functions - called a pipeline

Starting with multiple arrays that you may need to call one after each other 
```
function increment(input) { return input + 1;}

function decrement(input) { return input — 1; }

function double(input) { return input * 2; }

function halve(input) { return input / 2; }
```
We put the function calls in an array and reduce over it:
```
let pipeline = [increment, double, decrement];

const result = pipeline.reduce(function(total, func) {
  return func(total);
}, 1);

result // 3
```
