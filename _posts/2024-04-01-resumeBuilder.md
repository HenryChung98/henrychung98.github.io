---
layout: single
title: "Resume Builder Project_1"
categories: project
tags: [resume-builder]
author_profile: false
search: true
---

### Programming languages used

- nextJs

### Introduction

This project is for practicing NextJs.

some figma

### setting

create project on current directory

install node.js is need

```zsh
npx create-next-app .
```

If you have never used NextJs, you will be asked

![des1](/assets/images/2024-04-01-resumeBuilder/des1.png)

and set the rest as you need. ESLint is recommended(find and fix problems in your JavaScript code)

![des2](/assets/images/2024-04-01-resumeBuilder/des2.png)

Also I will use styled-components to practice.

```zsh
npm install styled-components
```

```javascript
import styled from "styled-components";
```

I created a form page to navigate to the page from home, I used Link tag which works similary as a tag but it provides optimized client-side navigation.

Need to import it first

```javascript
import Link from "next/link";
```

```javascript
export default function Home() {
  return (
    <>
      <Link href="/FormPage">form page</Link>
    </>
  );
}
```

### Color Select Container

For styled-components, define your styled components by calling the styled function and passing an HTML tag or another component. You can then write your CSS styles using tagged template literals.

```javascript
// should be capitalized
const ColorUl = styled.ul`
  list-style-type: none;
  padding: 0;
  margin: 0;
  text-align: center;
`;

const ColorBtn = styled.li`
  width: 40px;
  height: 40px;
  border-radius: 5px;
  border: none;
  display: inline-block;
  margin-right: 50px;
  cursor: pointer;
`;

export default function Home() {
  return (
    <>
      <ColorUl>
        <RedBtn />
        <YellowBtn />. . .
      </ColorUl>
      <br></br>
      <Link href="/FormPage">form page</Link>
    </>
  );
}
```

I might use this color container function again, so I will make it as a component.

```javascript
export default function ColorContainer() {
  return (
    <>
      <DivCon>
        <RedBtn />
        <YellowBtn />
        .
        .
        .
  );
}
```

```javascript
// index.js
export default function Home() {
  return (
    <>
      <h1>Select a Template</h1>
      <ColorContainer></ColorContainer>
      <br />
      <Link href="/FormPage">form page</Link>
    </>
  );
}
```

![des3](/assets/images/2024-04-01-resumeBuilder/des3.png)

Add color picker to select color not on the list.

```javascript
const ColorSelect = styled.input.attrs({ type: "color" })`
  border: none;
  position: relative;
  bottom: 5px;
  width: 40px;
  height: 40px;
  border-radius: 10px;
  cursor: pointer;
`;
```

![des4](/assets/images/2024-04-01-resumeBuilder/des4.png)

I want to make when the color box is clicked, the color input is changed to the color. I need useState method.

```javascript
import { useState } from "react";

export default function ColorContainer() {
  const [selectedColor, setSelectedColor] = useState("#000000");
.
.
.
  return (
    <>
      <ColorUl>
        <RedBtn onClick={() => setSelectedColor("#e46f7f")} />
        <YellowBtn onClick={() => setSelectedColor("#e46f7f")} />
        .
        .
        .
        <ColorSelect
          value={selectedColor}
          onChange={(e) => setSelectedColor(e.target.value)}
        />
      </ColorUl>
    </>
  );
}
```

![des5](/assets/images/2024-04-01-resumeBuilder/des5.png)

### Template Select Container

```javascript
const Container = styled.div`
  display: grid;
  grid-template-columns: repeat(4, 1fr);
`;
const Template = styled.div`
  background-color: white;
  width: 265px;
  height: 350px;
  border-radius: 10px;
`;
```

```javascript
export default function TemplateContainer() {
  return (
    <>
      <Container>
        <Link href="/FormPage" style={{ margin: "70px" }}>
          <Template />
        </Link>
        <Link href="/FormPage" style={{ margin: "70px" }}>
          <Template />
        </Link>
        <Link href="/FormPage" style={{ margin: "70px" }}>
          <Template />
        </Link>
        .
        .
        .
  );
}

```

![des6](/assets/images/2024-04-01-resumeBuilder/des6.png)

##### Learned New

Since each components do not share variables(like useState), all variables should be defined in parent components, so I delete ColorContainer, TemplateContainer components and added those in index file.

And added onClick in Link tag to set selectedTemplate.

```javascript
const [selectedTemplate, setSelectedTemplate] = useState(0);
<Link href="/FormPage" style={{ margin: "70px" }} onClick={() => setSelectedTemplate(0)}>
.
.
.
```

![des7](/assets/images/2024-04-01-resumeBuilder/des7.png)

Also each page does not share variables as well, but I need to export two variables from SelectPage to FormPage, so I used useRouter method to send the variable in url.

```javascript
import { useRouter } from "next/router";

export default function SelectPage() {
  const router = useRouter();
  function handleSubmit(color, template) {
    router.push(`/form/0?color=${color}&template=${template}`);
  }
  .
  .
  .
  <button
  onClick={(e) => {
    e.preventDefault();
    handleSubmit(0, selectedColor);
  }}>
    hi
  </button>
}
```

```javascript
// FormPage
import { useRouter } from "next/router";

export default function FormPage() {
  const router = useRouter();
  const { color, template } = router.query;
  console.log(`color: ${color}`);
  console.log(`template: ${template}`);
  return <></>;
}
```

![des8](/assets/images/2024-04-01-resumeBuilder/des8.png)

If there is an section sign in query, need to encode it.

```javascript
function handleSubmit(template, color) {
  router.push(`/Form?template=${template}&color=${encodeURIComponent(color)}`);
}
```

![des9](/assets/images/2024-04-01-resumeBuilder/des9.png)
