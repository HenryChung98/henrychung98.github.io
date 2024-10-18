---
layout: single
title: "To Do List Practice_4"
categories: project
tags: [todolist]
author_profile: false
search: true
---

[To Do List Practice_1](https://henrychung98.github.io/project/todoListPrac1/)
[To Do List Practice_2](https://henrychung98.github.io/project/todoListPrac2/)
[To Do List Practice_3](https://henrychung98.github.io/project/todoListPrac3/)

##### Learned New

First, if I code selectedDate.getDate() === item.date.getDate(), there is an issue since all months share the same date. Assume I saved data for March 1st; then, the data will be shown for April 1st, May 1st, and so on. So, I modified it to formattingDate(selectedDate) === formattingDate(item.date).

Second, I am not sure the reason, but it seems document.addEventListener prevent to click checkbox.

So I added if statement to be able to click checkbox.

```typescript
document.addEventListener("click", (e) => {
  if ((e.target as HTMLElement).closest(".day")) {
    listDate.innerHTML = formattingDate(calendar.selectedDate);
    showData(dbList, calendar.selectedDate);
  }
});
```

Third,

```typescript
const index = dbList.findIndex((dbItem) => dbItem === item);
```

this variable is so useful to control the dbList. It is in the forEach loop of db which is parameter of showData. I can access and control the dbList array directly.

```typescript
// to display the correct conditions of todo list
if (index !== -1) {
  checkBox.checked = dbList[index].isChecked;
  if (checkBox.checked === true) {
    li.classList.add("done");
  }
}
// to toggle isChecked in dbList
if (index !== -1) {
  dbList[index].isChecked = checkBox.checked;
}

// to delete if remove button is clicked
if (index !== -1) {
  dbList.splice(index, 1);
  showData(dbList, selectedDate); // Update displayed data
}
```

![des1](/assets/images/2024-03-08-todoListPrac4/des1.png)

![des2](/assets/images/2024-03-08-todoListPrac4/des2.png)

Now just need saving dbList in localStorage. I added a code for that in addData function.

```typescript
function addData(selectedDate: Date, isChecked: boolean, content: string) {

  ...

  localStorage.setItem("todoItems", JSON.stringify(dbList));
}
```

##### Learned New2

If I want to get 'date' from localStorage, I need to parse it, but when I try to parse 'date', there is a problem.

![des3](/assets/images/2024-03-08-todoListPrac4/des3.png)

I got '2024-03-11T03:21:17.407Z', which follows the ISO 8601 format that is an international standard for representing dates and times in a way that is unambiguous, easy to read, and independent of language or region. JavaScript cannnot read this format, so I have handle it.

```typescript
function loadFromLocalStorage() {
  const savedItems = localStorage.getItem("dbList");

  if (savedItems) {
    const todoItems: Data[] = JSON.parse(savedItems);
    todoItems.forEach((item) => {
      item.date = new Date(item.date);
    });
    console.log(`loaded data: ${todoItems[0].date}`);
    dbList.push(...todoItems);
  }
}
```

![des4](/assets/images/2024-03-08-todoListPrac4/des4.png)

Almost everything works properly, now I just need to add 'localStorage.setItem("dbList", JSON.stringify(dbList));' this line to event listener of removeBtn, checkBox so that data in dbList will be set correctly.

