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

Also, I will make several templates so need to modify template part as well. First, define selectedTemplate variable

```javascript
  let selectedTemplate;
  if (template == 1) {
    selectedTemplate = <Template1 backColor={color} {...formData} />;
  }
  else if
  .
  .
  .
```

and return this in Preview Box container.

```javascript
return (
  <>
    <div className={styles.container}>
      <FormBox>
        <button onClick={nextForm}>NEXT</button>
        <PersonalDetail onChange={handleInputChange}></PersonalDetail>
      </FormBox>
      <PreviewBox>{selectedTemplate}</PreviewBox>
    </div>
  </>
);
```

and need to modify Formbox part as well.

```javascript
let currentForm;

  function nextForm() {
    setFormOrder((prevOrder) => (prevOrder < 5 ? prevOrder + 1 : 5));
  }
  function previousForm() {
    setFormOrder((prevOrder) => (prevOrder > 0 ? prevOrder - 1 : 0));
  }

  if (formOrder == 0) {
    currentForm = (
      <PersonalDetail onChange={handleInputChange}></PersonalDetail>
    );
  } else if (formOrder == 1) {
    currentForm = (
      <ProfessionalExp onChange={handleInputChange}></ProfessionalExp>
    );
    .
    .
    .
    }
```

##### Learned New

When I change the form order, the previous form data is deleted(Priview screen looks fine). All inputs should keep containing the data.

I added parameters(props) for each form function and define input value as the arguments.

```javascript
export default function PersonalDetail({ onChange, firstName, lastName }) {

<td>
  <input name="firstName" onChange={onChange} value={firstName} />
</td>
<td>
  <input name="lastName" onChange={onChange} value={lastName}/>
</td>
```

```javascript
<PersonalDetail onChange={handleInputChange} {...formData}></PersonalDetail>
```

![des2](/assets/images/2024-04-16-resumeBuilder2/des2.png)

##### Validation

I want to make if input box get focusOut, check the validation.

First, need to define two useStates and write a function to check validation.

```javascript
const [validFirstName, setValidFirstName] = useState("");
const [validFirstNameE, setValidFirstNameE] = useState("");

const validateFirstName = (value) => {
  if (value.length < 3) {
    setValidFirstName(styles.errors);
    setValidFirstNameE("First name is too short");
  } else {
    setValidFirstName("");
    setValidFirstNameE("");
  }
};
```

and add className and onBlur to input tag

```javascript
<input
  name="firstName"
  onChange={onChange}
  value={firstName}
  onBlur={(e) => validateFirstName(e.target.value)}
  className={validFirstName}
/>
.
.
.
 <td className={styles.errors}>{validFirstNameE}</td>
```

![des3](/assets/images/2024-04-16-resumeBuilder2/des3.png)

It works. Now, need to write all valition functions for each input.

Since there are so many things to check validation, I searched how to optimize it and got like this.

```javascript
// useState
  const [validations, setValidations] = useState({
    firstName: { className: "", message: "" },
  });

// validate function
  const validateField = (field, value, regex, errorMessage) => {
    if (!value.trim() || !regex.test(value.trim())) {
      setValidations((prevValidations) => ({
        ...prevValidations,
        [field]: { className: styles.errors, message: errorMessage },
      }));
      return false;
    }
    setValidations((prevValidations) => ({
      ...prevValidations,
      [field]: { className: "", message: "" },
    }));
    return true;
  };

// check validatoin
  const validateFirstName = (value) => {
    return validateField(
      "firstName",
      value,
      /.{3,}/,
      "First name is too short"
    );
  };
.
.
.
<input
  name="firstName"
  onChange={onChange}
  value={firstName}
  onBlur={(e) => validateFirstName(e.target.value)}
  className={validations.firstName.className}
/>
.
.
 <td className={styles.errors}>{validations.firstName.message}</td>
```

If there is at least one error, I want to make the Next button not clickable, so need to use useEffect.

```javascript
const [counter, setCounter] = useState(0);

// prop to send the parent component
errorCheck(counter);

useEffect(() => {
  const isAllEmpty = (obj) => {
    const keys = Object.keys(obj);
    for (let i = 0; i < keys.length; i++) {
      const key = keys[i];
      if (obj.hasOwnProperty(key) && obj[key].message !== "") {
        return 0;
      }
    }
    return 1;
  };

  const result = isAllEmpty(validations);
  setCounter(result);
}, [validations]);
```

and error handling in parent component

```javascript
const [errorCheck, setErrorCheck] = useState(0);
const handleError = (newCounter) => {
  setErrorCheck(newCounter);
  console.log(newCounter);
};

// handle displayed form
let currentForm;

function nextForm() {
  if (errorCheck == 1) {
    setFormOrder((prevOrder) => (prevOrder < 4 ? prevOrder + 1 : 4));
  } else {
    alert("please fill the form and check error");
  }
}
function previousForm() {
  if (errorCheck == 1) {
    setFormOrder((prevOrder) => (prevOrder > 0 ? prevOrder - 1 : 0));
  } else {
    alert("please fill the form and check error");
  }
}
```
![des4](/assets/images/2024-04-16-resumeBuilder2/des4.png)

check the date validation is a bit different.
```javascript
const [workStartv, setWorkStartv] = useState("");
  const [workEndv, setWorkEndv] = useState("");

  const handleChangeDate = (e) => {
    const { name, value } = e.target;
    if (name === "workStart") {
      setWorkStartv(value);
    } else if (name === "workEnd") {
      setWorkEndv(value);
    }
    const startDate = new Date(workStart);
    const endDate = new Date(workEnd);

    const differenceInMs = endDate - startDate;

    const differenceInDays = differenceInMs / (1000 * 60 * 60 * 24);

    if (differenceInDays < 0) {
      validations.workDate.className = styles.errors;
      validations.workDate.message = "Invalid Date";
    }
    else{
      validations.workDate.className = "";
      validations.workDate.message = "";
    }
  };
```