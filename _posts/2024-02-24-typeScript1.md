---
layout: single
title: "TypeScript1(Introduction)"
categories: note
tags: [typeScript]
author_profile: false
search: true
---

### introduction

TypeScript is a superset of JavaScript that adds static typing to the language. It brings several advantages to the development process, making it a useful choice for many developers and projects.

When we code with JavaScript, runtime errors often occur since JavaScript does not check whether the code is fine before it ie executed. The reason why it happens is JavaScript is Interpreted Programming Languages(implementations execute instructions directly, without the need for a separate compilation step).

Also, JavaScript is a dynamically typed language, so we can use variables as we want, but if you make a mistake, it is quite hard to find them.

TypeScript secures these issues. TypeScript introduces static typing, allowing developers to define and enforce types for variables, parameters, and return values. Also with static typing, the codebase becomes more self-documenting.

### setting

First, create a folder and go to terminal, and get package.json.

```zsh
npm init
```

After, we need to install TypeScript.

```zsh
npm install --save-dev typescript
```

make sure typescript is added.
![des1](/assets/images/2024-02-24-typeScript1/des1.png)

and type this

```zsh
npx tsc --init
```

now you will see tsconfig.json file is added.

Go to package.json, and modify this part.
![des2](/assets/images/2024-02-24-typeScript1/des2.png)

Now all set up. You can create main.ts and execute typing

```zsh
npm run build
```

Once you execute it, main.js will be created. You can execute typing

```zsh
npm start
```
