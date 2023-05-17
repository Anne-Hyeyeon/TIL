# 2023-05-12
## What is difference between attr and property in HTML?
### attribute
- An "attribute" (or "attr") is a piece of information that is **added to an HTML tag to define its properties.** 
- Attributes are used to provide additional information about an element, such as its color, size, or behavior. 
- Attributes can be defined in the opening tag of an element using the syntax "attributeName='attributeValue'", where attributeName is the name of the attribute and attributeValue is the value assigned to it.
### property
- A "property", **refers to a value** that is assigned to an element's attribute. -
- Properties are used to set and retrieve values of an element's attributes using JavaScript. 
- Properties are accessed from DOM (Document Object Model) nodes.
- For example, the "src" attribute of an image element can be accessed and changed using the "src" property of the JavaScript object representing the image element.
### Summary
- In summary, an "attribute" is part of the HTML code used to define an element's properties, while a "property" is a value assigned to that attribute that can be accessed and manipulated through JavaScript.

# 2023-05-15 
## Type Assertion VS Type Declaration
### Type Assertion
- Type assertion in TypeScript is used to assert or convert the type of a variable to a more specific type, even when the TypeScript compiler may not be able to detect it.
- Two ways to perform type assertions in TS
1) Using the "as" keyword
```ts
let myVar: any = "hello";
let myString: string = myVar as string;
```
- In this example, we first declare a variable myVar of type any and assign it a string value. We then use the as keyword to assert that myVar should be treated as a string, and assign the resulting value to a new variable myString.
2) Using the "<>" syntax:
```ts
let myVar: any = "hello";
let myString: string = <string>myVar;
```
### Type Declaration
- Type declaration in TypeScript is used to explicitly specify the type of a variable, function, or other entity. 
```ts
function addNumbers(x: number, y: number): number {
  return x + y;
}
```

# 2023-05-16
## What is useLocation hook?
### useLocation
- The useLocation hook allows you to access and interact with the current **location object** in a React component.
### location object
- The location object represents the **current URL** in your application and contains information about the **current route**, **query parameters**, and other relevant data.
### What can I do with useLocation hook?
- The useLocation hook provides a simple way to access this location object within a functional component.
- By importing and using the useLocation hook in your component, you can retrieve the current location object and access its properties such as pathname, search, state, and more.
```ts
import { useLocation } from 'react-router-dom';

const MyComponent = () => {
  const location = useLocation();

  // Accessing properties of the location object
  console.log(location.pathname);
  console.log(location.search);
  console.log(location.state);

  return (
    // JSX of your component
    // ...
  );
};
```
- You can then access properties of the location object, such as pathname, search, and state, to retrieve information about the current URL.
- UseLocation hook is typically used within components that are rendered by a Route component or nested within a component that is rendered by a Route component in order to access the routing information.


# 2023-05-17
## import React from 'react'
### What is 'import React from 'react'?'
- In React.js, the `import React from 'react'` statement is used to import the **necessary dependencies** from the React library. 
- When you use this import statement, it allows you to **access and use the core features, components, and utilities provided by React.**

## What happends when I use this import statement?
1. `Module System`: React follows the module system, which allows developers to organize their code into reusable modules. The import keyword is used to import modules from external files or libraries.
2. `Default Export` : The React library typically exports its functionality using a default export. It means that when you import from 'react', you are importing the default export of the 'react' module, which is the main React object.
```js
import React from 'react';

function Button({ text }) {
  return <button>{text}</button>;
}

export default Button;
```
3.  `React Namespace`: By importing React, you create a reference (or namespace) to the React library. This means you can access various components and utilities provided by React using the React object.
