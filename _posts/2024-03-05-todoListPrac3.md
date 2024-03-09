---
layout: single
title: "To Do List Practice_3"
categories: project
tags: [todolist]
author_profile: false
search: true
---

#### calendar class

I will add small calendar to save todo list by date. I created new file to contain calendar class. I got a calendar class from chatGPT, and modified serveral issues.

Now I see a calendar.

![des1](/assets/images/2024-03-05-todoListPrac3/des1.png)

The to do list should be shown depending on the selected date. I added one more parameter in todoItems for savedDate and declared the listDate as a selected date.

```typescript
function saveItems() {
let todoItems: { isChecked: boolean; text: string, savedDate: Date }[] = [];
.
.
const listDate = calendar.selectedDate;
.
.
todoItems.push({ isChecked, text: liContent, savedDate: listDate });
}
.
.
```

#### from scratch

I think I should have done creating a calendar and create to do list. I have no clue how can I apply calendar to my previous code. I will start from scratch for to do list part.

First, get selected date.

```typescript
const days = ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"];
const months = [
  "Jan",
  "Feb",
  "Mar",
  "Apr",
  "May",
  "Jun",
  "Jul",
  "Aug",
  "Sep",
  "Oct",
  "Nov",
  "Dec",
];

document.addEventListener("click", () => {
  console.log(`${calendar.selectedDate}`);
  listDate.innerHTML = `${
    months[calendar.selectedDate.getMonth()]
  } ${calendar.selectedDate.getDate()}, ${calendar.selectedDate.getFullYear()}`;
});
```

```HTML
<h2 id="listDate">select date</h2>
```

![des2](/assets/images/2024-03-05-todoListPrac3/des2.png)

I noticed formatting date is hassle and hard to read since it is too long, so I made a function.

```typescript
function formattingDate(date: Date): string {
  return `${months[date.getMonth()]} ${date.getDate()}, ${date.getFullYear()}`;
}
```

and replace

```typescript
document.addEventListener("DOMContentLoaded", () => {
  listDate.innerHTML = formattingDate(today);
});

document.addEventListener("click", () => {
  listDate.innerHTML = formattingDate(calendar.selectedDate);
});
```

And need database list. First, create an interface and a database list.

```typescript
interface Data {
  date: Date;
  isChecked: boolean;
  content: string;
}

const dbList: Data[] = [];
```

After, need to create a function for adding data to the database list.

```typescript
function addData(selectedDate: Date, isChecked: boolean, content: string) {
  const newItem: Data = {
    date: selectedDate,
    isChecked: isChecked,
    content: content,
  };
  dbList.push(newItem);
  console.log(dbList[dbList.length - 1]);
}
```

![des3](/assets/images/2024-03-05-todoListPrac3/des3.png)

And now I will create showData function. This is pretty same idea as the addNewList function that I have created before. The point of this function is get data from the database and compare with current selected data and show.

```typescript
function showData(db: Data[], selectedDate: Date) {
  // to erase previous data and show selected date's data
  todoList.innerHTML = "";

  db.forEach((item) => {
    if (selectedDate.getDate() === item.date.getDate()) {
      const checkBox = document.createElement("input") as HTMLInputElement;
      checkBox.type = "checkbox";
      const li = document.createElement("li") as HTMLLIElement;
      li.textContent = item.content;
      checkBox.addEventListener("change", () => {
        li.classList.toggle("done", checkBox.checked);
      });
      // remove button
      const removeBtn = document.createElement("button") as HTMLButtonElement;
      removeBtn.textContent = "Remove";
      removeBtn.classList.add("removeBtn");
      removeBtn.addEventListener("click", () => {
        listBox.remove();

        // Remove the item from dbList array
        const index = dbList.findIndex((dbItem) => dbItem === item);
        if (index !== -1) {
          dbList.splice(index, 1);
          showData(dbList, selectedDate); // Update displayed data
        }
      });
      // contains checkbox, li, removeBtn
      const listBox = document.createElement("div") as HTMLDivElement;
      listBox.classList.add("listBox");
      listBox.appendChild(checkBox);
      listBox.appendChild(li);
      listBox.appendChild(removeBtn);

      // append div to ul
      todoList.appendChild(listBox);
    }
  });
}
```
