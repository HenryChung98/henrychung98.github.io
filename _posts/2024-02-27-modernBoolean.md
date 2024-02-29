---
layout: single
title: "JavaScript Boolean"
categories: note
tags: [javaScript]
author_profile: false
search: true
---

### falsy

Considered as false(falsy)

- false
- null
- undefined
- NaN
- 0
- ''

Considered as true(truthy)

- []
- {}
- everything else except falsy

### logical operators

Logical operator in JavaScript, you will get not only true, false, and also a value that you compared. For example,

```javascript
console.log("JS" && "JavaScript");
```

Both are true, so it seems like it returns true, but you will get "JavaScript".

In JavaScript, logical operators work like

| left side of value | and             | or              |
| ------------------ | --------------- | --------------- |
| truthy             | right-hand side | left-hand side  |
| falsy              | left-hand side  | right-hand side |

```javascript
console.log(true && true); // true
console.log(true && false); // false
console.log(false && true); // false
console.log(false && false); // false
```

```javascript
console.log(true || true); // true
console.log(true || false); // true
console.log(false || true); // true
console.log(false || false); // false
```

```javascript
console.log(null && undefined); // null
console.log(0 || true); // true
console.log("0" && NaN); // NaN
console.log({} || 123); // {}
```

You can use this method like

```javascript
function print(value) {
  const message = value || "Hello, world!";
  console.log(message);

  print(); // Hello, world!
  print("Javascript"); // JavaScript
}
```

In the code, value || "Hello, world!" is that if value is not given, it will return "Hello, world!"(right-hand side) since || operator return right-hand side if left-hand side is falsy.

### nullish coalescing operator

The nullish coalescing (??) operator is a logical operator that returns its right-hand side operand when its left-hand side operand is null or undefined, and otherwise returns its left-hand side operand.

```javascript
const title1 = null || "Hello";
const title2 = null ?? "Hello";
const title3 = false ?? "Hello";

console.log(title1); // Hello
console.log(title2); // Hello
console.log(title3); // false
```
