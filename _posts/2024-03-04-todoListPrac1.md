---
layout: single
title: "To Do List Practice_1"
categories: project
tags: [todolist]
author_profile: false
search: true
---

### Programming languages used

- html
- css
- typeScript

### introduction

This project is for practicing TypeScript.

### setting

initial setting
[TypeScript Setting](https://henrychung98.github.io/note/typeScript1/)

![des1](/assets/images/2024-03-04-todoListPrac1/des1.png)

### code

First, get all variables in initial settings.

```typescript
const todoList = document.getElementById("lists") as HTMLUListElement;
const inputListEle = document.getElementById("inputList") as HTMLInputElement;
const addBtn = document.getElementById("addBtn") as HTMLButtonElement;

addBtn.addEventListener("click", () => {
  const inputList = inputListEle.value;
  console.log(inputList);
});
```

If I don't use as, TypeScript is not automatically aware of the type of that element.

I tested it and it works, so I will create add new list function.

```typescript
function addNewList(text: string) {
  const li = document.createElement("li") as HTMLLIElement;
  li.textContent = text;
  todoList.appendChild(li);
}
```

and modify event listener function

```typescript
addBtn.addEventListener("click", (e) => {
  const inputList = inputListEle.value;
  addNewList(inputList);
  inputListEle.value = "";
});
```

If I click the button, new list is created and appended.

![des2](/assets/images/2024-03-04-todoListPrac1/des2.png)

I wrote css codes for done, removeBtn, and divBox for a list,

```css
.listBox {
  width: 100%;
  display: flex;
  justify-content: space-between;
  height: 20px;
  margin: 30px;
}
.done {
  opacity: 0.5;
  text-decoration: line-through;
}
.removeBtn {
  background-color: red;
  height: 20px;
  margin-right: 20px;
}
```

and

- Create checkBox, li, removeBtn
- Create div and add classList
- Append 3 elements to div
- Append div to todoList(ul)

```typescript
function addNewList(text: string) {
  const checkBox = document.createElement("input") as HTMLInputElement;
  checkBox.type = "checkbox";

  const li = document.createElement("li") as HTMLLIElement;
  li.textContent = text;

  const removeBtn = document.createElement("button") as HTMLButtonElement;
  removeBtn.textContent = "Remove";
  removeBtn.classList.add("removeBtn");

  const listBox = document.createElement("div") as HTMLDivElement;
  listBox.classList.add("listBox");
  listBox.appendChild(checkBox);
  listBox.appendChild(li);
  listBox.appendChild(removeBtn);

  todoList.appendChild(listBox);
}
```

Now I see this screen.

![des3](/assets/images/2024-03-04-todoListPrac1/des3.png)

I need to make checkBox, removeBtn work properly.

- When checkBox is clicked, apply done class.
- When removeBtn is clicked, remove the list.

Just add these in the add new list function.

```typescript
checkBox.addEventListener("change", () => {
  li.classList.toggle("done", checkBox.checked);
  });
.
.
.
removeBtn.addEventListener("click", () => {
  listBox.remove();
});
```

If I click the checkBox,

![des4](/assets/images/2024-03-04-todoListPrac1/des4.png)

and removeBtn also works.
