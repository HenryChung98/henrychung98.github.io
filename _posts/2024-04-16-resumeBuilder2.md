---
layout: single
title: "Resume Builder Project_2"
categories: project
tags: [resume-builder]
author_profile: false
search: true
---

I made PersonalDetail form component and define a prop for onChange.

### Form

```javascript
import styles from "@/styles/Form.module.css";


export default function PersonalDetail({onChange}) {

  return (
    <>
      <form>
        <table className={styles.personalDetail}>
          <tr>
            <td>First Name</td>
            <td>Last Name</td>
          </tr>
          <tr>
            <td>
              <input name="firstName" onChange={onChange} />
            </td>
            <td>
              <input name="lastName" onChange={onChange}/>
            </td>
            .
            .
            .
      )
}
```

In Form.js, create useState for form data. There is a lot of data, so I can make it like this.

```javascript
  const [formData, setFormData] = useState({
    firstName: "",
    lastName: "",
    jobTitle: "",
    address: "",
    city: "",
    state: "",
    .
    .
    .
  });

```

And need a function to handle input change

```javascript
const handleInputChange = (e) => {
  const { name, value } = e.target;
  setFormData((prevData) => ({
    ...prevData,
    [name]: value,
  }));
};
```

This function updates the form data state whenever an input field value changes. It extracts the name and value from the input element triggering the change event, then uses setFormData to update the state, preserving existing data and updating the specific field that changed.

```javascript
return (
  <>
    <div className={styles.container}>
      <FormBox>
        <button onClick={nextForm}>NEXT</button>
        <PersonalDetail onChange={handleInputChange}></PersonalDetail>
      </FormBox>
      <PreviewBox>
        <Template1
          backColor={color}
          {...formData} // you can use spread syntax!
        />
      </PreviewBox>
    </div>
  </>
);
```

![des1](/assets/images/2024-04-16-resumeBuilder2/des1.png)
