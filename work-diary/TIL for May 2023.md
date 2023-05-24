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

### What happends when I use this import statement?
1) step 1. `Module Resolution`: React follows the module system, which allows developers to organize their code into reusable modules. The import keyword is used to import modules from external files or libraries.
2) step 2. `Default Export` : The React library typically exports its functionality using a default export. It means that when you import from 'react', you are importing the default export of the 'react' module, which is
3) step 3. `Creating a Reference to React` : By importing React, you create a reference (or namespace) to the React library. This means you can access various components and utilities provided by React using the React object.
4) step 4. `Accessing React Features`: After importing React, you can use the React object to access different aspects of React, such as React components, hooks, context, and more. For example, you can create React components by extending React.Component, use hooks like React.useState, or access the context API using React.createContext.

### Why do I have to do 'import React from 'react''?
- `JSX Transformation`: React uses JSX (JavaScript XML) syntax, which allows you to write HTML-like code in your JavaScript files. However, JSX is not natively supported by browsers. The import React from 'react' statement is necessary because it includes the JSX transformation logic required to convert JSX code into regular JavaScript code that browsers can understand. (But after React version 17, you no longer need to import React module to use JSX transformation.
- `React Library Access`: The import React from 'react' statement gives you access to the full React library. React provides a set of functions, components, and utilities that are necessary for building and rendering user interfaces. Without importing React, you won't be able to use these features, such as creating React components, rendering them to the DOM, managing state, handling events, and more.
- `Component Inheritance`: When you create a custom component in React, you typically extend the **React.Component** class or use functional components with hooks. The import React from 'react' statement provides access to the React object, which includes the base Component class and other essential components and utilities needed for creating and managing components.

### After version 17... Automatic JSX Runtime
- Starting from React version 17, you no longer need to explicitly import the React object in most cases. This change is known as `Automatic JSX Runtime` or `JSX Transform` introduced in React 17.
- Under the Automatic JSX Runtime, React components can be used without importing React explicitly, as long as you have the necessary tools and configurations in place. This change was made to improve performance and reduce the bundle size of React applications.

### Some situations where you may need to import React after version 17
- `JSX Fragments`: If you use JSX Fragments (<React.Fragment> or the shorthand syntax <>) in your components, you will need to import React explicitly, as JSX Fragments require the React object.
```ts
import React from 'react';

function MyComponent() {
  return (
    <>
      <h1>Title</h1>
      <p>Content</p>
    </>
  );
}
```
- `Custom Hooks`: If you define custom hooks that use React features or rely on the React object, you will need to import React within those custom hooks.
```ts
- import React from 'react';

function useCustomHook() {
  // Using React state in the custom hook
  const [count, setCount] = React.useState(0);

  // Rest of the custom hook logic
  // ...
}

function MyComponent() {
  useCustomHook();

  // Rest of the component logic
  // ...
}
```
-`Conditional Rendering`: If you have conditional rendering logic that depends on React elements or components, you may need to import React to use JSX syntax within the conditional statements.
```ts
import React from 'react';

function MyComponent({ isLoggedIn }) {
  return (
    <div>
      {isLoggedIn ? <p>Welcome!</p> : null}
    </div>
  );
}
```

# 2023-05-19
## What can I do if I encounter the error message "Cannot find module './filename' or its corresponding type declarations"?
- The error message you're seeing typically occurs when the module or file you're trying to import (./filename) cannot be found or does not exist. 
1) `verify the file path`: Double-check the **file path**  of filename and ensure that it is correct. Make sure the file is located in the same directory as the file where the import statement is being used, or provide the correct relative or absolute path to the file.
2) `Check the file extension` : Ensure that the file you're trying to import has the appropriate file extension. For example, if you're importing a JavaScript file, it should have the **.js** extension.
3) `Check for typos` : Make sure there are no typos or spelling errors in the file name or path.
4) `Verify the module's existence` : Confirm that the module ./filename exists and is properly exported from its file. Check if the file contains a default export or named export that matches the import statement you're using.

# 2023-05-22
## try/catch syntax
### What is it?
- In programming, `errors or exceptions` can occur during the execution of a program. These exceptions can disrupt the normal flow of code execution. To handle such exceptions, many programming languages, including JavaScript, provide a mechanism called "try/catch."
```ts
try {
  // Code that may throw an exception
} catch (error) {
  // Code to handle the exception
}
```
### how it works
1) The code within the **try** block is executed.
2) If an **exception** occurs within the try block, the execution is **immediately transferred to the catch block.
3) The catch block receives the exception **object as a parameter**. You can choose any valid variable name (e.g., error, e, etc.) to represent the exception object.
4) Inside the catch block, you can write code to handle the exception, such as logging an error message, displaying a user-friendly error, or taking appropriate actions to recover from the exception.

- By using try/catch, you can prevent your program from crashing and provide a graceful way to handle exceptions.

# 2023-05-23
## async/await
### What is async/await?
- A powerful feature in JS that simplifies working with asynchronous code. It allows you to wirte **asynchronous code** in a **more synchronous style**, making it easier to read and understand.
### How it works?
- The `async` is used to define an synchronous function. An asynchronous function always returns a promise object.
- Within an asynchronous function, you can use the `await` before a promise to pause the execution of the function until the promise is resolved or rejected.This allows you to wirte code that **looks synchronous but behaves asynchronously.**
- You can only use `await` inside an `async` function. However, you can use multiple await statements sequentially or even in parallel to wait for multiple promises.
```ts
 function delay(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

async function fetchData() {
  try {
    console.log('Fetching data...');
    await delay(2000); // Simulating an asynchronous operation
    console.log('Data fetched!');
  } catch (error) {
    console.error('Error:', error);
  }
}

fetchData();
```
- In the above example, the fetchData function is defined as an async function. It uses the await keyword to pause the execution for 2000 milliseconds (simulating an asynchronous operation) and then logs the message "Data fetched!".
## What does `resolve` and `resolution` mean in the context of JavaScript?
- In the context of JavaScript promises, the terms "resolve" and "resolution" refer to the outcome of a promise.
### resolve
- In the context of a promise, `resolve` refers to the **successful completion or fulfillment of a promise.
- When a promise is resolved, it means that the asynchronous operation associated with the promise has completed successfully, and the promise is considered fulfilled.
- Resolving a promise means that the associated `then` callback(s) will be executed, allowing you to handle the resolved value.
```js
const promise = new Promise((resolve, reject) => {
  // Asynchronous operation
  // When successful, call resolve with a value
  resolve('Success!');
});
```

### Resolution
- "Resolution" refers to the state of a promise, indicating whether it has been fulfilled or rejected.
- A promise can be in one of the following three states: 
1) **Pending**: The initial state when the promise is neither fulfilled nor rejected.
2) **Fulfilled**: The promise has been successfully resolved.
3) **Rejected**: The promise encountered an error or was explicitly rejected.
- When working with promises, you can handle the resolution using the `then` method to handle fulfillment or the catch method to handle rejection:
```ts
promise.then(resolvedValue => {
  // Handle fulfillment
}).catch(error => {
  // Handle rejection
});
```
- The resolvedValue represents the value with which the promise was resolved, and the error represents the reason for rejection.
- Promises provide a structured way to handle asynchronous operations in JavaScript, allowing you to handle the resolution (success or failure) of an operation and write cleaner, more maintainable asynchronous code.

# 2023-05-24
## Excess Property Checks
### What is Excess Property Checks?
- In TypeScript, excess property checks refer to a type-checking mechanism that ensures the objects assigned to a variable or passed as function arguments **don't have extra properties not defined by the assigned type.
- When you assign an object literal to a variable or pass it as an argument to a function, TypeScript checks if the object literal has any extra properties that are not explicitly defined in the type annotation or interface. If it does, TypeScript raises an error.

### Example

```js
interface Person {
  name: string;
  age: number;
}

function greet(person: Person) {
  console.log(`Hello, ${person.name}!`);
}

const john: Person = {
  name: "John",
  age: 30,
  occupation: "Engineer" // Extra property not defined in Person interface
};

greet(john); // Object literal may only specify known properties, and 'occupation' does not exist in type 'Person'.

```
- In this example, the Person interface defines the name and age properties. However, when assigning the john object to the Person type, it includes an extra property occupation that is not part of the Person interface. TypeScript detects this and raises an error: Object literal may only specify known properties, and 'occupation' does not exist in type 'Person'.
-  If you want to assign objects with additional properties, you can use type assertions (as) or explicitly define the object's type as a wider type that allows extra properties, such as any or an index signature.


## How to Avoid Excess Property Checks?
### 1) Assigning an object with extra properties to another variable
```ts
interface Person {
  name: string;
  age: number;
}

function greet(person: Person) {
  console.log(`Hello, ${person.name}!`);
}

const john: Person = {
  name: "John",
  age: 30,
  occupation: "Engineer" 
};

let tmp = { name: 'Joan', age:30, occupation:'Engineer' }
tmp = john

greet(tmp) // no error
```
- In TypeScript, when you assign an object with extra properties to **another variable**, TypeScript performs excess property checks at the point of **object literal assignment.
-  Once the object literal **passes the type-check at the assignment site**, TypeScript widens the inferred type of the object to include any extra properties it may have. 
-  This widened type is then used for further type-checking.
-  In example, the error doesn't occur when assigning the john object to the tmp variable because the **excess property check is performed at the line tmp = john**
-   At that point, TypeScript checks that the **john object conforms to the type of tmp**.
-  Since the john object has extra properties not defined in the Person interface, it would raise an error at this assignment statement.
-   However, once the assignment is successful, TypeScript widens the inferred type of tmp to include any extra properties of john. This means that TypeScript treats tmp as having the type { name: string, age: number, occupation: string }, even though the Person interface only defines name and age.
- As a result, when you pass tmp to the greet function, TypeScript performs type-checking based on the widened type, which does include the occupation property. Since the greet function parameter is of type Person, and { name: string, age: number, occupation: string } satisfies the structure of Person, no error is raised.

### 2) Using a Type Assertion (casting)
-By using a `type assertion` (also known as type casting) with the as keyword, you can explicitly tell TypeScript the type of an object and bypass the excess property check.
```ts
interface Person {
  name: string;
  age: number;
}

function greet(person: Person) {
  console.log(`Hello, ${person.name}!`);
}

const john = {
  name: "John",
  age: 30,
  occupation: "Engineer" 
};

greet(john as Person); // Using type assertion
```
- In the code above, the john object has an extra property occupation that is not defined in the Person interface. However, by using the as Person type assertion, you inform TypeScript that you want to treat the john object as a Person type during the function call to greet. TypeScript will trust your assertion and won't raise an error regarding the excess property.
- It's important to note that when using type assertions, you should be cautious and make sure that the object you're asserting to a specific type does indeed adhere to the structure and behavior of that type. Using type assertions incorrectly may lead to runtime errors or type-related issues if the object doesn't match the asserted type.

