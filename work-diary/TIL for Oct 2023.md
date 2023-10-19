# 2023-10-11
## Handling Undefined Data Errors in Frontend Applications
### Problem
1. Error report received from the QA team stating the main screen of a specific server isn't displaying.
2. Upon checking, a particular value on a specific page is coming in as undefined.
3. This value is being sourced from the redux store using `useSelector`.

**Question: Even if the backend does not send the data, what measures can be taken on the front end to prevent errors due to undefined?**


### Solution:

- **Data Validation**:
    - Check the validity of the data received from the backend.
    - For instance, verify if a particular key exists in an object, if an array is empty, or if a value is null or undefined.
- **Setting Default Values**:
    - Define default values to be used in the absence of data to prevent errors.
- **Use Optional Chaining (`?.`)**:
    - In JavaScript, safely access nested properties of an object using the `?.` operator.
    - Example: `const value = data?.user?.name;`
- **Utilize Nullish Coalescing (`??`)**:
    - Use the `??` operator to substitute null or undefined values with another value.
    - Example: `const value = data.user.name ?? 'Default Name';`
- **Employ React Error Boundaries**:
    - Use Error Boundaries in React to catch errors in a component tree and render a fallback UI.
    - This ensures only the error-prone component gets replaced while the rest of the application continues to function.
- **Manage Loading State**:
    - Handle a loading state while fetching data from the backend. If data isn't ready, display a spinner or placeholder.
- **Error Handling**:
    - When using APIs like Axios or Fetch, capture errors from API calls using .catch() or try/catch blocks.
    - In case of an error, display an error message to the user or implement retry logic.
- **Adopt TypeScript**:
    - Using TypeScript can help catch type-related errors at compile-time, reducing runtime errors.
- **Automate Testing**:
    - Write tests for components and functions using tools like Jest or React Testing Library. This ensures code can be safely deployed with every change.
 


# 2023-10-13
## The reasons why functional programming techniques and for loops often clash

- While removing the for loop as written by the senior developer...

1. **`Immutability`** : Functional programming emphasizes the immutability of data. It operates by **maintaining the original data** and **creating new data** instead of modifying existing data. This immutability helps keep the code predictable and error-resistant. However, for **loops are typically used to change variables and mutate data**, which clashes with these two approaches.

2. **`Side Effects`**: Functional programming aims to **minimize side effects**. Side effects occur when functions modify external state or depend on external state. for loops often involve modifying external state and can lead to various side effects during the iteration. This makes the code harder to predict and debug.

4. **`Readability`**: Functional programming uses **higher-order functions** and a **declarative style** to enhance code readability. In contrast, **for loops are imperative and require detailed explanations of how a task is performed**. This results in functional programming having a more concise and readable code style.

5. **`Parallelism and Optimization`**: Functional programming provides a structure that makes **parallelism and optimization easier**. Functional code consists of pure functions, making it easier to avoid concurrency issues. In contrast, for loops are imperative, which can make parallelism and optimization more challenging.

Therefore, functional programming and for loops differ significantly in terms of code writing and maintenance approaches. Functional programming, especially in complex and error-prone programs, can offer a more useful approach due to its advantages.


# 2023-10-17
## When never[] type is inferred in useState
### Problem

```tsx
const [listItems, setListItems] = useState([]);

useEffect(() => {
    const totalItems = 10;
    const generatedItems = Array.from({ length: totalItems }, (_, idx) => ({
        label: `${idx + 1} year`, 
        key: idx + 1,
    }));
    setListItems(generatedItems); // Error occurs, the argument of type '{ title: string; value: number; }[]' cannot be assigned to the parameter of type 'SetStateAction<never[]>'.
}, []);
```

### Cause
- This error originates from a type mismatch in TypeScript. The discrepancy arises because the `setListItems function`, generated through the useState hook, **does not match the type of the totalItems** state variable.

- To address this, **the argument for the setListItems function and the type of the totalItems state variable must align**. The error message indicates that it cannot be assigned to a parameter of type 'SetStateAction<never[]>'. This is because the argument type for the setListItems function is inferred as never[], but we are attempting to pass an array of type { label: string; key: number; }[].

- **When utilizing useState([]), TypeScript infers an empty array as the initial state and deduces its type as never[]**. The `never[] type` represents an array that **cannot contain any elements.**

- Subsequently, when calling the setListItems function, it tries to retain the totalItems state variable's type as never[]. However, since we aim to pass an array of { label: string; key: number; }[] type to the setListItems function, this results in a type mismatch error.

### Solution
1. Set the **initial state value correctly**. Explicitly specify the initial state value as an array type so that TypeScript can infer the correct type.
```tsx
const [totalItems, setListItems] = useState<{ label: string; key: number; }[]>([]);
```

2. Without explicitly setting the initial state value as { label: string; key: number; }[], **pass values of type { label: string; key: number; }[] to the setListItems function**.
```tsx
setListItems([{ label: '1 year', key: 1 }, { label: '2 years', key: 2 }, /* ... */]);
```

### Conclusion
- Managing state in React with TypeScript can be challenging, especially when it comes to inferring the correct types. The aforementioned issues and solutions highlight the importance of being `explicit` about our data types, particularly when initializing state using the useState hook.
  - By providing clear type annotations and ensuring that our state updates align with these specified types, we can not only avoid unexpected TypeScript errors but also create more predictable and type-safe React components. Always remember, the clearer our code's intentions are, the fewer bugs and issues we'll encounter in the long run.


# 2023-10-18
## Exploring the 'for...in' Loop
### Situation
- I find myself using the `for...in` loop quite frequently these days. I especially use it when I want to exclude specific values from parameters. What exactly is `for...in`? Let's delve into it a bit more.

### What is the 'for...in'?
- The `for...in` loop is used in JavaScript to **iterate over the enumerable properties of an object**. This construct offers a simplified way to write code and can be immensely useful in various scenarios.

- For instance, if one wishes to **retrieve all key-value pairs from an object**, **barring a specific key**, this can be conveniently achieved using the for...in loop combined with a conditional statement.

### Usage
```js
const user = {
  name: 'John',
  age: 25,
  password: '12345',
  address: 'Seoul'
};

const filteredData = {};
for (let key in user) {
  if (key !== 'password') {
    filteredData[key] = user[key];
  }
}

console.log(filteredData);  // { name: 'John', age: 25, address: 'Seoul' }
```

- In the example above, all key-value pairs, excluding the 'password' key, were copied to the filteredData object.

### Considerations When Using the for...in Loop

1. Inherited Properties:
The for...in loop enumerates properties inherited from an object's prototype chain. To avoid this, one can employ the `Object.prototype.hasOwnProperty()` method to ascertain if the object directly owns the given property.

2. Arrays:
It is not recommended to use for...in on arrays. As arrays might possess properties beyond indices, this can lead to unexpected results. Instead, it's advisable to use alternatives like for...of or `Array.prototype.forEach()` for iterating over arrays.

### Conclusion
In modern JavaScript and TypeScript environments, there's a trend towards employing libraries or features (e.g., spread operator, Object.assign()) that treat objects and arrays immutably. This leads to writing code that's more concise and safer. However, in specific situations, the for...in loop remains a valuable tool.



# 2023-10-19

## Ensuring React Hooks are Called at the Component Top Level

### Situation
#### Original Code
```tsx
useEffect(() => {
    const priorSettingValue = useRef(currentSettingValue);
    if (priorSettingValue.current === 0 && currentSettingValue !== 0) {
      updateSetting({ key: 'backupIntervalKey', value: '0' });
    }

    priorSettingValue.current = currentSettingValue;
  }, [currentSettingValue, updateSetting]);
// Error : React Hook "useRef" cannot be called inside a callback. React Hooks must be called in a React function component or a custom React Hook function
```
- Error message: React Hook "useRef" cannot be called inside a callback. React Hooks must be called in a React function component or a custom React Hook function.

#### Updated Code
```tsx
    const priorSettingValue = useRef(currentSettingValue);

useEffect(() => {
    if (priorSettingValue.current === 0 && currentSettingValue !== 0) {
      updateSetting({ key: 'backupIntervalKey', value: '0' });
    }

    priorSettingValue.current = currentSettingValue;
  }, [currentSettingValue, updateSetting]);
```

### Root of the Problem
- In this code, the useRef hook was called **inside the useEffect**. However, one of React's hook rules is that **hooks can only be called at the top level of a component**. This means that hooks shouldn't be called inside **conditionals, loops, nested functions, etc.** Thus, the given code raised an error.

- In the updated code, the useRef hook was called outside of useEffect, at the top level of the component, adhering to React's hook rules.

### Calling Hooks Exclusively at the Component Top Level
- When we say **"call hooks at the top level,"** it implies that hooks should be directly invoked **within the body of the function component** without being indirectly triggered by specific logic, conditionals, loops, or nested functions.
#### Correct Usage:
```jsx
function MyComponent() {
  const [count, setCount] = useState(0);  // Correct position
  const value = useMemo(() => count * 2, [count]); // Correct position

  return (
    <div onClick={() => setCount(count + 1)}>
      {count} - {value}
    </div>
  );
}
```

#### Incorrect Usages:
1. Calling inside a conditional:
```jsx
function MyComponent({ isLoaded }) {
  if (isLoaded) {
    const [data, setData] = useState(null);  // Incorrect position
  }
  // ...
}
```

2. Calling inside a loop:
```jsx
function MyComponent({ items }) {
  items.forEach(item => {
    const [count, setCount] = useState(0);  // Incorrect position
  });
  // ...
}
```

3. Calling within a nested function or event handler:
```jsx
function MyComponent() {
  function handleClick() {
    const [state, setState] = useState(false);  // Incorrect position
    // ...
  }
  // ...
}
```
These restrictions exist because React uses **the order of hook calls** to manage internal states and side effects appropriately. If hooks are called conditionally or within nested functions, React wouldn't be able to track the state of hooks correctly, leading to unpredictable behaviors.
