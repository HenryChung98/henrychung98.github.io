---
layout: single
title: "Modern JavaScript(Useful Internal Features)"
categories: note
tags: [javaScript]
author_profile: false
search: true
---

#### Sort

```javascript
const letters = ["e", "c", "d", "a", "b"];
const numbers = [1, 20, 7, 25, 3600];

letters.sort();
numbers.sort();

console.log(letters); // ["a", "b", "c", "d", "e"]
console.log(numbers); // [1, 20, 25, 3600, 7]
```

By default, the sort() method converts array elements to strings and compares their sequences of UTF-16 code units. So we have to write like

```javascript
const numbers = [1, 20, 7, 25, 3600];
numbers.sort((a, b) => a - b);
console.log(numbers); // [1, 7, 20, 25, 3600]
```

#### Reverse

```javascript
const letters = ["a", "c", "b"];
const numbers = [123, 756, 252];

letters.reverse();
numbers.reverse();

console.log(letters); // ["b", "c", "a"]
console.log(numbers); // [252, 756, 123]
```

#### Map

```javascript
// create map
const myMap = new Map();

// set
myMap.set("title", "string value");
myMap.set(2024, "int value");
myMap.set(true, "boolean value");

// get
console.log(myMap.get(2024)); // string value
console.log(myMap.get(true)); // boolean value
console.log(myMap.get("title")); // string value

// has
console.log(myMap.has("title")); // true
console.log(myMap.has("name")); // false

// size
console.log(myMap.size); // 3

// delete
myMap.delete(true);
console.log(myMap.get(true)); // undefined
console.log(myMap.size); // 2

// clear
myMap.clear();
console.log(myMap.get(2024)); // undefined
console.log(myMap.size); // 0
```

#### Set

```javascript
// create set
const devices = new Set();

// add
devices.add("iPhone"); // Set(1) {"iPhone"}
devices.add("Macbook"); // Set(2) {"iPhone", "Macbook"}
devices.add("AppleWatch"); // Set(3) {"iPhone", "Macbook", "AppleWatch"}

// has
console.log(devices.has("AppleWatch")); // true
console.log(devices.has("GalaxyBook")); // false

// size
console.log(devices.size); // 3

// delete
devices.delete("AppleWatch");
console.log(devices.size); // 2

// clear
devices.clear();
console.log(devices.size); // 0
```

The feature preserves the order of initially added elements, and when attempting to add duplicate values later, those values are ignored.

Using this feature, Set is often employed to create a collection of unique values, effectively removing duplicates within an array.

```javascript
const numbers = [1, 3, 4, 3, 3, 2, 5, 5, 3, 2, 1, 4];
const uniqNumbers = new Set(numbers);

console.log(uniqNumbers); // Set(5) {1, 3, 4, 2, 5}
```

#### forEach

Iterates through each element in an array and executes a callback function for each element.

```javascript
const numbers = ["a", "b", "c"];

numbers.forEach((element, index, array) => {
  console.log(element); // a, b, c
  console.log(index); // 0, 1, 2
  console.log(array); // ['a', 'b', 'c'], ['a', 'b', 'c'], ['a', 'b', 'c']
});
```

#### Filter

Creates a new array with elements that pass a provided condition.

```javascript
const devices = [
  { name: "Macbook", brand: "Apple" },
  { name: "GalaxyBook", brand: "Samsung" },
  { name: "Zephyrus", brand: "Asus" },
  { name: "Gram", brand: "LG" },
  { name: "AppleWatch", brand: "Apple" },
];

// index, array are optional parameters
const macbooks = devices.filter((element, index, array) => {
  return element.name === "Macbook";
});
const apples = devices.filter((element, index, array) => {
  return element.brand === "Apple";
});

console.log(macbooks); //(1) [{name: "Macbook", brand: "Apple"}]
console.log(apples); // (2) [{name: "Macbook", brand: "Apple"}, {name: "AppleWatch", brand: "Apple"}]
```

#### Find

The find method works similarly to the filter method, but it stops the iteration and returns the element once a match is found.

```javascript
const devices = [
  { name: "Macbook", brand: "Apple" },
  { name: "GalaxyBook", brand: "Samsung" },
  { name: "Zephyrus", brand: "Asus" },
  { name: "Gram", brand: "LG" },
  { name: "AppleWatch", brand: "Apple" },
];

// index, array are optional parameters
const myLaptop = devices.find((element, index, array) => {
  console.log(index); // 0, 1, 2, 3
  return element.name === "Gram";
});

console.log(myLaptop); // {name: "Gram", brand: "LG"}
```

#### Some

Tests whether at least one element in the array passes the provided condition. Returns true if at least one element satisfies the condition; otherwise, returns false.

```javascript
const numbers = [1, 2, 3, 4];

const hasEvenNumber = numbers.some(function (num) {
  return num % 2 === 0;
});
// hasEvenNumber: true (because 2 is even)
```

#### Every

Tests whether all elements in the array pass the provided condition. Returns true if every element satisfies the condition; otherwise, returns false.

```javascript
const numbers = [2, 4, 6, 8];

const allEvenNumbers = numbers.every(function (num) {
  return num % 2 === 0;
});
// allEvenNumbers: true (because all numbers are even)
```

#### Reduce

Applies a function against an accumulator and each element in the array to reduce it to a single value.

```javascript
const numbers = [1, 2, 3, 4];

// index, array are optional parameters
const sum = numbers.reduce((accumulator, element, index, array) => {
  return accumulator + current;
}, 0);

console.log(sum); // 10
```

#### indexOf

Returns the index of the first occurrence of a specified element in an array. Returns -1 if the element is not found.

```javascript
const fruits = ["apple", "banana", "orange"];

const index = fruits.indexOf("banana");
// index: 1
```
