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

const [listItems, setListItems] = useState([]);

useEffect(() => {
    const totalItems = 10;
    const generatedItems = Array.from({ length: totalItems }, (_, idx) => ({
        label: `${idx + 1} year`, 
        key: idx + 1,
    }));
    setListItems(generatedItems); // Error occurs, the argument of type '{ title: string; value: number; }[]' cannot be assigned to the parameter of type 'SetStateAction<never[]>'.
}, []);


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




