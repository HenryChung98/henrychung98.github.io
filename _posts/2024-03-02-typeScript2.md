---
layout: single
title: "TypeScript_2(Prevent Type Errors)"
categories: note
tags: [typeScript]
author_profile: false
search: true
---

#### simple types

- boolean
- number
- string
- bigint
- undefined
- null

NaN, Infinity are considered number, so you can check using

```typescript
Number.isFinite;
Number.isNaN;
.
.
.
```

![des1](/assets/images/2024-03-02-typeScript2/des1.png)

#### type checking

You are able to define a type of variable before you assign a value.

Here are several examples

```typescript
let value1: number;
let value2: number = 10;
let array1: string[] = [];
let array2: [number, string] = [1, "a"];

// these all give error. will be noticed with a red line
value1 = "a"; // should be number
array1.push(3); // should be string
array2 = [9, "a", 3]; // should be 1 number 1 string
array2 = [9, 2]; // should be 1 number 1 string
```

There is special type called 'literal type' which is considered exact values.

```typescript
const literalVal1 = "hello world"; // type: "hello world"(subset of string)
const literalVal2 = 10; // type: 10(subset of number)
let val = "hello world";

function printSomething(a: "hello world") {
  console.log(a);
}

printSomething(literalVal1); // "hello world"
printSomething(val); // error since val is string(not literal type)

function printSomething2(a: string) {
  console.log(a);
}
printSomething2(literalVal1); // "hello world"
```

You can define object types as well.

```typescript
let student: {
  firstName: string;
  lastName: string;
  studentNumber: number;
  gender: boolean;
  hobby?: number; // optional property
}; = {
    firstName: "Henry",
    lastName: "Chung",
    studentNumber: 123456789,
    gender: true;
}


// this object should be all "string": "number"
let obj: { [id: string]: number } = {
    one: 1,
    two: 2,
  };
```

and function

```typescript
function add(a: number, b: number, c?: number) {
  if (c === undefined) {
    return a + b;
  } else {
    return a + b + c;
  }
}
```

so you easily can find an error regarding type mismatch.

```typescript
let student = {
  firstName: "Henry",
  lastName: "Chung",
  studentNumber: 123456789,
  gender: true,
};
student.studentNumber = "987654321"; // error

const updateStudent = {
  firstName: "Henry",
  lastName: "Chung",
  studentNumber: 123456789,
  gender: "male",
};

student = updateStudent; // error since type of genders are incompatible
```

#### any

In TypeScript, the any type represents a dynamic or untyped value, allowing flexibility but sacrificing static type checking. It's recommended to avoid using any and prefer more specific types for better type safety. If necessary, you can explicitly cast variables to any using "as" or a colon.

```typescript
let dynamicValue: any = "Hello, TypeScript!";
dynamicValue = 42; // no error, not recommended

let dynamicValue: any = "Hello, TypeScript!";
let stringValue: string = dynamicValue as string;

// e.g.
const parsedProduct = JSON.parse('{ "name": "Henry", "number": 12345 }') as {
  name: string;
  number: number;
};
```

#### enum

Enums, short for enumerations, allow you to define a set of named constant values, typically representing a collection of related values.

```typescript
enum Color {
  Red,
  Green,
  Blue,
}

let myColor: Color = Color.Red;
console.log(myColor); // 0
```

But there is an issue. Since the default values of enum members are assigned numerically, starting from 0, the actual value of myColor is 0 in this case. This value could be considered falsy, so when working with enums, especially when dealing with conditionals, assigning specific values to enum members is recommended.

```typescript
enum Color {
  Red = "Red",
  Green = "Green",
  Blue = "Blue",
}

let myColor: Color = Color.Red;
console.log(myColor); // Red
```

#### interface

Interfaces in TypeScript define a contract for the shape of an object. They specify the properties and their types that an object must have.

```typescript
interface Person {
  name: string;
  age: number;
}

const person: Person = {
  name: "John",
  age: 25,
};

// can describe the shape of functions, including parameter types and return types.
interface Calculator {
  add(x: number, y: number): number;
  subtract(x: number, y: number): number;
}
const calculator: Calculator = {
  add: (x, y) => x + y,
  subtract: (x, y) => x - y,
};
const resultAddition = calculator.add(5, 3);
const resultSubtraction = calculator.subtract(8, 3);
```

Interfaces can extend other interfaces, allowing you to compose and reuse definitions.

```typescript
interface Shape {
  color: string;
}

interface Square extends Shape {
  sideLength: number;
}

// e.g.
let shape: Square = {
  color: "red",
  sideLength: 2,
};
```
