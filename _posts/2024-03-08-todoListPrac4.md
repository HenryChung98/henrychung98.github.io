---
layout: single
title: "To Do List Practice_4"
categories: project
tags: [todolist]
author_profile: false
search: true
---

#### control check box

##### Learned New

If I code selectedDate.getDate() === item.date.getDate(), there is an issue since all months share the same date. Assume I saved data for March 1st; then, the data will be shown for April 1st, May 1st, and so on. So, I modified it to formattingDate(selectedDate) === formattingDate(item.date).
