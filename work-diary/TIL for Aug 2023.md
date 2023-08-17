# 2023-08-03
## Middlewares - RPC
### What is RPC (Remote Procedure Call)?
`Remote Procedure Call (RPC)` is a **communication protocol** and **programming paradigm** used in distributed computing environments. The main idea behind RPC is to allow programs or processes running on different machines to communicate with each other as if they were local procedures or functions. It abstracts the complexity of remote communication and provides a way to invoke functions on a remote server in a manner that appears almost identical to invoking a local function.
### Key Points of RPC
`Abstraction of Remote Calls`: RPC provides an abstraction layer that hides the underlying networking and communication details. Developers can call remote functions or procedures in a way that is conceptually similar to invoking local functions.

`Client-Server Interaction`: RPC typically involves a client-server architecture, where the client sends a request to the server to execute a specific function. The server performs the requested operation and sends the result back to the client.

`Stubs and Skeletons`: To achieve the illusion of local function calls, RPC uses stubs (on the client side) and skeletons (on the server side). The client-side stub packages the request parameters and sends them to the server, while the server-side skeleton unpacks the request, executes the function, and sends the result back.

`Interface Definition`: An important aspect of RPC is defining the interface of the remote procedures. This includes specifying the methods, their parameters, and return values in a language-independent way using an interface definition language (IDL).

`Binding`: The process of connecting a client to a specific server implementing the remote procedures is known as binding. There can be different binding techniques, such as static binding (where the client knows the server's location) and dynamic binding (where a separate service helps locate the server).

`Synchronous and Asynchronous Calls`: RPC supports both synchronous and asynchronous communication. In synchronous RPC, the client waits for the server's response before continuing. In asynchronous RPC, the client can continue its work while waiting for the response.

`Security and Error Handling`: Security mechanisms can be integrated into RPC to ensure secure communication between client and server. Error handling is also an important aspect, as network failures or remote server unavailability should be gracefully managed.

`Use Cases`: RPC is used in various scenarios, including distributed systems, client-server applications, and microservices architectures, where different components need to communicate across network boundaries.


# 2023-08-04
## itrables
**Types and Uses of Iterables**:

An iterable represents a collection of elements that can be iterated or traversed. In JavaScript, there are various types of iterables.

1. **Array**: Arrays are the most common type of iterable. Each element in an array can be accessed using an index, and they can be traversed using a for...of loop.

2. **String**: Strings are also iterables. Each character in a string can be traversed using a for...of loop.

3. **Map**: Maps consist of key-value pairs and are used for iterating over keys.

4. **Set**: Sets contain a collection of unique values. They can be traversed using a for...of loop.

5. **TypedArray**: TypedArrays are similar to arrays, but they store elements of a specific data type.

6. **Generator**: Generator functions define routines that produce values, and they return a value each time they are called. They can be used to generate and iterate over values using an iterator.


**Usage of Array.from**:

The `Array.from(iterable)` method converts an iterable or array-like object into an array. This method is used when you need to transform elements from a given iterable into an array. For instance, you can convert a string into an array or extract values from a Set or Map into an array using `Array.from`. It's also useful for converting the results of Generator functions into arrays.

Examples:
```ts
const str = 'hello';
const strArray = Array.from(str); // ['h', 'e', 'l', 'l', 'o']

const set = new Set([1, 2, 3]);
const setArray = Array.from(set); // [1, 2, 3]

function* generateNumbers() {
  yield 1;
  yield 2;
  yield 3;
}

const generatorArray = Array.from(generateNumbers()); // [1, 2, 3]

```
`Array.from` is a convenient way to convert iterable objects into arrays. It provides an easy method to transform and work with various data types as arrays.


# 2023-08-07
## useLoaderData Hook

This hook provides the value returned from your route loader.

```tsx
import {
  createBrowserRouter,
  RouterProvider,
  useLoaderData,
} from "react-router-dom";

function loader() {
  return fetchFakeAlbums();
}

export function Albums() {
  const albums = useLoaderData();
  // ...
}

const router = createBrowserRouter([
  {
    path: "/",
    loader: loader,
    element: <Albums />,
  },
]);

ReactDOM.createRoot(el).render(
  <RouterProvider router={router} />
);
```

`useLoaderData` is a hook provided by React Router. It automatically refreshes data after route actions are called and returns the latest results from the loader.

It's important to note that `useLoaderData` doesn't start fetching data itself. It simply reads the results of a fetch managed internally by React Router. This means you don't need to worry about refetching when it rerenders for reasons other than routing.

As a result, the returned data remains stable between renders, making it safe to pass to dependency arrays in React hooks like `useEffect`. The data only changes when the loader is called again after actions or specific navigations. Even if the values don't change, the identity will change in these cases.

You can use this hook not only in Route elements but also in any component or custom hook. It retrieves data from the nearest route in the context.


# 2023-08-08
## What should we use instead of &&?
1. Using ternary expressions
```js
function ComponentWithTernary({ list }) {
  return (
    <div>
      {list.length > 0 ? (
        <ul>
          {list.map((item, index) => (
            <li key={index}>{item}</li>
          ))}
        </ul>
      ) : (
        <p>No items to display.</p>
      )}
    </div>
  );
}
```

2. Use !!list.length
```js
function ComponentWithDoubleNegation({ list }) {
  return (
    <div>
      {!!list.length && (
        <ul>
          {list.map((item, index) => (
            <li key={index}>{item}</li>
          ))}
        </ul>
      )}
    </div>
  );
}
```

3. Use list.length >= 1
```js
function ComponentWithAndAndLength({ list }) {
  return (
    <div>
      {list.length >=1 && (
        <ul>
          {list.map((item, index) => (
            <li key={index}>{item}</li>
          ))}
        </ul>
      )}
    </div>
  );
}
```

 _TIPS(from_ [_MDN_](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_AND)_): The logical AND (&&) operator (logical conjunction) for a set of boolean operands will be true if and only if all the operands are true. Otherwise it will be false._
> 
> ==_More generally, the operator returns the value of the first falsy operand encountered when evaluating from left to right, or the value of the last operand if they are all truthy.

- reference : https://medium.com/javascript-in-plain-english/its-2023-please-stop-using-for-conditional-rendering-in-react-b588a09ebb17

# 2023-08-09
## React.memo
### What is React.memo?
- `React.memo is a **higher-order component (HOC)** in React that is used for **optimizing functional components** by **preventing unnecessary re-renders**.
- It works by memoizing the rendered output of a component and reusing it if the component's props have not changed.
- This can help improve the performance of your application by avoiding unnecessary renders when the component's output would be the same as before.

### example
```jsx
import React from 'react';

const MyComponent = React.memo(({ prop1, prop2 }) => {
  // Component rendering logic...
});

export default MyComponent;
```
In the above example, the MyComponent functional component will only re-render if its **prop1 or prop2 props have changed**. If the props remain the same between renders, the memoized version of the component's output will be reused, saving unnecessary render cycles.

### What is the difference between React.memo and useMemo hook?
- React.memo and useMemo are both **techniques in React that deal with optimization**, but they serve different purposes and are used in different contexts.
- React.memo is used to optimize the rendering of functional components by preventing unnecessary re-renders based on props, while useMemo is used to optimize the performance of computations within functional components by memoizing the results of those computations based on dependencies.


# 2023-08-11 
## How to flatten an Array? (small tip)
I came across this in a Medium article, and I was surprised I hadn't known about it until now :p"
- To transform a **nested array into a single-level array** in JavaScript, the `flat()` function can be utilized.
- This function produces a new array by **merging the elements of sub-arrays into it**, up to a given level of depth.

```js
const nestedArray = [[10, 20], [30, 40, [50, 60, [70, 80]]]];

const singleLevelArray = nestedArray.flat(3);

console.log(singleLevelArray); // Output: [10, 20, 30, 40, 50, 60, 70, 80]
```
- In the given code, nestedArray is a complex array with multiple layers of nested arrays, some reaching as deep as three levels.
- By invoking the `flat()` function and specifying a depth of 3, we merge all the elements from the sub-arrays into a unified array.
- As a result, singleLevelArray holds all the elements from the original nested structure in a one-dimensional format.


# 2023-08-16
## namespace, interface
- Namespace: A namespace is one of TypeScript's features for structuring and modularizing code. Namespaces are used to group related code without polluting the global scope. They are especially helpful in large projects to avoid conflicts between modules and organize code. Within a namespace, you can define components such as classes, functions, variables, and then access them using the name of the namespace.

```ts
namespace MyNamespace {
    export interface MyInterface {
        // ...
    }
    export class MyClass {
        // ...
    }
}
const instance = new MyNamespace.MyClass();
```

- Interface: An interface in TypeScript is an abstract structure used to define types. It is mainly used to specify the shape of objects or the methods and properties a class should implement. Interfaces are useful for interacting with other types or specifying that a class follows a certain format. They define an abstract contract in the code, and the actual implementation is done in another class.
```ts
interface Car {
    brand: string;
    model: string;
    startEngine(): void;
}

class ElectricCar implements Car {
    brand: string;
    model: string;

    constructor(brand: string, model: string) {
        this.brand = brand;
        this.model = model;
    }

    startEngine() {
        console.log("Electric engine started.");
    }
}

```
- In simple terms, namespaces are used for code structuring, and interfaces are used for type definitions. Namespaces are primarily used for modularization, and interfaces define the shape of structured data or the convention of a class.



# 2023-08-17
## Directly Calling vs. Dispatching Redux Actions: What's the Difference?

### Question
- `fetchAppData()` is a function exported from `utils.ts`. It's being used in `settingSystemAction` through an import and is dispatched in several pages.
- Is it possible to directly call `fetchAppData()` from the pages instead of dispatching it? Would there be any issues with that approach?


### Answer
- If `fetchAppData()` is an asynchronous action created with Redux's `createAsyncThunk` or another Redux helper, it's designed to interact with the Redux store. Directly invoking this action creator isn't problematic by itself, but doing so won't affect the Redux store.

- In other words, if you call `fetchAppData()` directly, it may perform the internal API call as defined, but the returned data will not be stored in the Redux store, nor will there be any state updates or other side effects in Redux.

### To summarize:

1. Directly invoking `fetchAppData()` won't impact the Redux store.
2. Using `dispatch(fetchAppData())` will update the Redux store's state based on the result (success or failure) of `fetchAppData()`.

- This behavior applies only if `fetchAppData` is a function designed to handle asynchronous operations related to Redux.

- Therefore, if you use the `fetchAppData()` function directly on a page, there's a high likelihood it won't behave as expected. If your reason for doing so is performance optimization or another specific scenario, it might be worth reconsidering the logic or finding an alternative approach.
