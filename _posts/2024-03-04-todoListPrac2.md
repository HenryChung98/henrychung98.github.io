---
layout: single
title: "To Do List Practice_2"
categories: project
tags: [todolist]
author_profile: false
search: true
---

#### save as csv

If I refresh, or re open it, the contents is gone. I want to save it with using csv.

There are three elements in listBox(div) checkBox, li, and removeBtn. You are able to get each elements, and the value using forEach. listBox is considered array, so you can get the each element by its index.

```typescript
function writeCSV() {
  const listItems = todoList.querySelectorAll(".listBox");

  listItems.forEach((div) => {
    // need to check div.children[0] is checkBox
    const isChecked = div.children[0];
    console.log((isChecked as HTMLInputElement).checked);

    // li.textContent
    console.log(div.children[1].textContent);
  });
}
```

I added this function to eventListener of add button to test it.

![des1](/assets/images/2024-03-04-todoListPrac2/des1.png)

Now I will modify the function to test saving to csv file.

```typescript
function writeCSV() {
  let csvContent: string = "";
  // select all divs in ul
  const listItems = todoList.querySelectorAll(".listBox");

  listItems.forEach((div, index) => {
    // need to check div.children[0] is checkBox
    const checkBoxEle = div.children[0];
    let isChecked: boolean = (checkBoxEle as HTMLInputElement).checked;

    // could be null, used js logical operator
    let liContent: string = div.children[1].textContent || "";
    csvContent += `${isChecked}, ${liContent}\n`;
    console.log(csvContent);
  });
}
```

![des2](/assets/images/2024-03-04-todoListPrac2/des2.png)

##### Learned New

I learned writing file from js, or ts is not allowed. Instead, there is a function called localStorage, which is a web storage technology in web browsers that allows you to store small amounts of data on the client side. So need to modify the csvContent parts.

```typescript
function saveIt() {
  let todoItems: { isChecked: boolean; text: string }[] = [];

  // select all divs in ul
  const listItems = todoList.querySelectorAll(".listBox");

  listItems.forEach((div) => {
    // need to check div.children[0] is checkBox
    const checkBoxEle = div.children[0];
    let isChecked: boolean = (checkBoxEle as HTMLInputElement).checked;

    // could be null, used js logical operator
    let liContent: string = div.children[1].textContent || "";
    todoItems.push({ isChecked, text: liContent });
  });
  localStorage.setItem("todoItems", JSON.stringify(todoItems));
}
```

To get the localStorage content, you need onLoad function. You can write like this

```typescript
window.addEventListener("load", () => {
  const savedItems = localStorage.getItem("todoItems");

  if (savedItems) {
    const todoItems: { isChecked: boolean; text: string }[] =
      JSON.parse(savedItems);

    todoItems.forEach((item) => {
      addNewList(item.text);
      const listBox = todoList.lastElementChild as HTMLDivElement;
      const checkBox = listBox.children[0] as HTMLInputElement;
      checkBox.checked = item.isChecked;
      listBox.children[1].classList.toggle("done", item.isChecked);
    });
  }
});
```


