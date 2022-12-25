### Map()

Use map when you want to manipulate all the values in an array - for example multiply them by 2. In this example map is used to change all the values in the array into Euros.
```
const dollars = [32, 45, 50];

const euros = dollars.map(eachAmount => eachAmount * .93);

//.93 was the exchange on google on 21st Jan 2017
euros //  [29.76, 41.85, 46.5]
```
Map traverses the array from left to right. It invokes a function (in this case, eachAmount * .93) on eachAmount (which you can call whatever you want). When the method is finished mapping all the elements it returns a new array with all the translated elements.

### Filter()

Use when you want to remove unwanted elements from an array.
```
const euros = [29.76, 41.85, 46.5];
const above30 = euros.filter(euro => euro >= 30);
above30 // [ 41.85, 46.5]
```
Filter works like map in that it invokes a function but the function will only return an array of elements that pass the criteria. It returns a new array.
