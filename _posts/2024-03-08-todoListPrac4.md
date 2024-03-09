---
layout: single
title: "To Do List Practice_4"
categories: project
tags: [todolist]
author_profile: false
search: true
---

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

Now just need to save dbList in localStorage.
