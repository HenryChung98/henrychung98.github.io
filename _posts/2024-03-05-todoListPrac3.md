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

I think I should have done creating a calendar and create to do list. I will start from scratch for to do list part.

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

and modify

```typescript
document.addEventListener("DOMContentLoaded", () => {
  listDate.innerHTML = formattingDate(today);
});

document.addEventListener("click", () => {
  listDate.innerHTML = formattingDate(calendar.selectedDate);
});
```

And need database list

```typescript
const dbbList: {
  [key: string]: { date: Date; isChecked: boolean; content: string };
}[] = [];
```
