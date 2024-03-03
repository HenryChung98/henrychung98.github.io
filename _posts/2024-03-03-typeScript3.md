---
layout: single
title: "TypeScript_3(Useful Internal Features)"
categories: note
tags: [typeScript]
author_profile: false
search: true
---

#### type alias

##### basic type alias

You can use type aliases to create a custom name for a type.

```typescript
type Age = number;
type Locate = [number, number];

let myAge: Age = 25;
let myLocation: Locate = [10, 10];
```

##### union type alias

Type aliases can be used to create unions of types.

```typescript
type Result = "success" | "failure";
type SearchQuery = string | string[];

let status: Result = "success";
let myQuery: SearchQuery = "a"; // or ["a", "b", "c"];
```

##### intersection type alias

Type aliases can also create intersections of types.

```typescript
type JobTitle = {
  title: string;
};
type Employee = JobTitle & {
  name: string;
  age: number;
};
// or
type EmployeeWithJob = Employee & JobTitle;
```

##### Generic type alias

Type aliases can be generic, allowing you to create reusable types that can work with different types.

```typescript
type Pair<T, U> = {
  first: T;
  second: U;
};

let coordinates: Pair<number, string> = { first: 10, second: "20N" };
```

##### mapped type alias

Type aliases can use mapped types to transform existing types.

```typescript
type Optional<T> = {
  [P in keyof T]?: T[P];
};

type PartialPerson = Optional<Person>;
```

##### combining types

You can combine existing types into a new type using type aliases.

```typescript
type Age = number;
type Result = "success" | "failure";
type Status = { age: Age; result: Result };

let myStatus: Status = { age: 25, result: "success" };
```

#### key of

The keyof operator is used to obtain the union type of all keys of a given type.

```typescript
type Person = {
  name: string;
  age: number;
  address: string;
};

type PersonKey = keyof Person;
// PersonKey is "name" | "age" | "address"

type AgeType = Person["age"];
// AgeType is number
```

#### type of

The typeof operator is used to capture the type of a value or an expression.

```typescript
const person = { name: "John", age: 30 };
type PersonType = typeof person;
// PersonType is { name: string; age: number; }


function getPerson() {
  return { name: "John", age: 30 };
}
type PersonType = typeof getPerson();
// PersonType is { name: string; age: number; }

```
