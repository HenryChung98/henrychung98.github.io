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

Then you will see package.json.

After, we need to install TypeScript.

```zsh
npm install --save-dev typescript
```

make sure TypeScript is added in devDependencies.

![des1](/assets/images/2024-02-24-TypeScript1/des1.png)

and type this

```zsh
npx tsc --init
```

- npx: executing node module
- tsc: TypeScript compiler module
- --init: creating initial setting file

now you will see tsconfig.json file is added.

![des2](/assets/images/2024-02-24-TypeScript1/des2.png)

Go to package.json, and modify script part

![des3](/assets/images/2024-02-24-TypeScript1/des3.png)

so that you can run the code with typing 'npm run build' for TypeScript, and 'npm run start' for JavaScript.

If you create main.ts file and execute it, main.js file will be created since TypeScript compiler(tsc) convert to js.

During this process, tsc not only convert to JavaScript file, but also [Type Check](https://www.TypeScriptlang.org/docs/handbook/advanced-types.html), [Transpile](https://www.freecodecamp.org/news/what-is-type-erasure-in-typescript/) and execute in node.js or web browser.

JavaScript file will be created depending on the version you set. You can change it in tsconfig.json file.
