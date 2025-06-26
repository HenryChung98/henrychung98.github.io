---
layout: single
title: "How to Rotate Icons on Hover"
categories: note
tags: [tailwind]
author_profile: false
search: true
use_math: true
---

This is a simple example using **Tailwind CSS** to rotate an icon when the user hovers over it.  
Each time the icon is hovered, it randomly rotates either 45 degrees or -45 degrees for a fun effect.

### Code

```jsx
import { useState } from "react";

function RotatingIcon() {
  const [hoverClass, setHoverClass] = useState("");

  const handleMouseEnter = () => {
    const randomClass =
      Math.random() > 0.5 ? "hover:rotate-45" : "hover:-rotate-45";
    setHoverClass(randomClass);
  };

  return (
    <div className="flex items-center md:w-1/2 p-3">
      <img
        src={iconPath}
        alt={iconAlt}
        onMouseEnter={handleMouseEnter}
        className={`w-1/3 ${hoverClass} hover:drop-shadow-lg transition-transform duration-300`}
      />
    </div>
  );
}
