---
layout: single
title: "TypeScript_2(Type)"
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
Number.is;
```

![des3](/assets/images/2024-03-02-TypeScript2/des1.png)

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
