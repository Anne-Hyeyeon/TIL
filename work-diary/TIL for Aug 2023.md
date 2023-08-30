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
- 

# 2023-08-18
## 깊은 오브젝트 비교 함수 (재귀함수 연습)

```ts
export function compareDeeply<T extends { [keyStr: string]: any }>(inputData: T, baselineData: T): Partial<T> {
  function findDifferences(sourceObj: any, compareObj: any): any {
    // Declare the result object
    const differenceResult: any = {};

    for (const keyStr in sourceObj) {
      // Check if the current keyStr is a unique property of sourceObj
      if (Object.prototype.hasOwnProperty.call(sourceObj, keyStr)) {
        // Get the values of the current keyStr from both sourceObj and compareObj
        const valueFromSource = sourceObj[keyStr];
        const valueToCompare = compareObj[keyStr];

        // If both valueFromSource and valueToCompare are objects and not arrays
        if (
          valueFromSource &&
          valueToCompare &&
          typeof valueFromSource === 'object' &&
          typeof valueToCompare === 'object' &&
          !Array.isArray(valueFromSource) &&
          !Array.isArray(valueToCompare)
        ) {
          // Recursively compare the values of valueFromSource and valueToCompare
          const nestedDifference = findDifferences(valueFromSource, valueToCompare);
          // If differences are found, add them to the result object
          if (Object.keys(nestedDifference).length) {
            differenceResult[keyStr] = nestedDifference;
          }
          // If valueFromSource and valueToCompare are not objects or are arrays
        } else if (!isEqual(valueFromSource, valueToCompare)) {
          // Directly add the value from valueFromSource to the result object
          differenceResult[keyStr] = valueFromSource;
        }
      }
    }
    return differenceResult;
  }

  return findDifferences(inputData, baselineData);
}
```


# 2023-08-22
## Comparing Performance: for Loops vs. Recursive Functions

1. `Risk of Stack Overflow` : Recursive functions use the function call stack. If the depth of the recursive calls becomes too deep, it can lead to a stack overflow. On the other hand, for loops are not affected by this issue.

2. `Overhead` : Recursive calls introduce overhead associated with function calls. With each call, a new stack frame is created, storing information like local variables and return addresses. A for loop performs operations directly without this additional overhead.

3. `Optimization` : Modern compilers may support "tail recursion optimization." This optimization can convert tail recursive calls into loops, reducing the overhead of recursive functions.

4. `Readability and Maintenance`: Some algorithms are much more concise and intuitive when expressed recursively. In contrast, implementing such algorithms might become more complicated using a for loop.

5. `Memory Usage`: Recursion uses stack memory with each function call, so deep recursive calls can lead to significant memory usage. for loops don't have this additional memory consumption.

### conclusion
In conclusion, if **performance considerations** are crucial, it might be better to use a **for loop** or another iterative structure over recursion. However, for **simplicity, readability, and maintainability**, **recursion** might be more suitable in certain situations.

The actual performance difference can depend on the specific problem, implementation, the language used, and other factors. Therefore, if performance is crucial, it's recommended to implement using both approaches and conduct performance tests to choose the optimal method.


# 2023-08-23
## Difference between directly using `props` and using `destructuring`

```js
const MyComponent = (props) => {
    return (
        <div>
            <p>{props.name}</p>
            <button onClick={props.handleClick}>Click Me</button>
        </div>
    );
}
```

```js
const MyComponent = ({ name, handleClick }) => {
    return (
        <div>
            <p>{name}</p>
            <button onClick={handleClick}>Click Me</button>
        </div>
    );
}
```

1. **Readability and Clarity**:
- Using destructuring makes it easy to identify at the top of the code which `props` the component expects and takes in. This provides clear visibility to the reader about the `props` the component depends on, enhancing readability.
- Conversely, using `props` directly can lengthen the code when referencing nested objects or arrays. For instance, you'd have something like `props.state.data.length`, which becomes lengthy.
2. **Code Brevity**:
- With destructuring, you can directly use each prop as a variable without repeatedly referencing it.
- For example, you can destructure `props` as `{ state, handlers, setTab }`, and in the subsequent code, you can use it in a concise manner like `state.data.length` or `handlers.refresh()`.
3. **Compatibility with TypeScript**:
- If you're using TypeScript, destructuring becomes particularly useful when defining the types of `props` for a component. It allows for clear type checking for each `prop`.
- In conclusion, **there's no substantive performance difference between the two methods.** The choice typically hinges on the developer's preference, code readability, and the coding style guide of the project.
- props를 그대로 썼을 때와 그렇지 않을 때의 성능 차이가 궁금했는데, 가독성과 간결성을 제외하고는 별 차이 없다고 한다. 다만, TS쓸 때는 props를 구조분해할당하여 타입을 체킹하는 게 더 간편하다.
``


# 2023-08-25
## What's the difference between directly calling Object.prototype.hasOwnProperty and not doing so?

### 1. data.hasOwnProperty('adUse'):
- This is attempting to call the `hasOwnProperty` method **directly** on the data object.
- The problem with this approach is if there's another **property or method named hasOwnProperty on the data object or its prototype chain**, it could overshadow the original hasOwnProperty method.
- For instance, if there's a different value assigned to the hasOwnProperty name on the data object, the code data.hasOwnProperty('adUse') wouldn't work as expected.
```ts
  const data = {
  adUse: true,
  hasOwnProperty: 'Oops! I am not a function anymore!'
};

console.log(data.hasOwnProperty('adUse')); // Error!
```

### 2. Object.prototype.hasOwnProperty.call(data, 'adUse'):
- This method directly retrieves and uses the hasOwnProperty method from **Object.prototype**.
- By using .call(data, 'adUse'), it specifies the data object as the target of the method, passing 'adUse' as an argument.
- This way, regardless of any property on the data object, you're always using the original hasOwnProperty method from Object.prototype to check.


# 2023-08-28
## Overriding (Java)

In Java, Overriding refers to the act of **redefining a method in a child class** that has already been defined in the parent class.


```java
class Animal {
  void move() {
    System.out.println("Animals move.");
  }
}

class Bird extends Animal {
  // Overriding
  void move() {
    System.out.println("Birds fly.");
  }
}

public class Test {
  public static void main(String[] args) {
    Animal myAnimal = new Animal();
    Animal myBird = new Bird();

    myAnimal.move();  // Output: "Animals move."
    myBird.move();  // Output: "Birds fly."
  }
}
```
- For example, let's assume that the parent class has a method called move() that says, "Animals move." Now, in a "Bird" class that inherits from this Animal class, you can rewrite the move() method to say, "Birds fly." When an object of the "Bird" class calls the move() method, it will output "Birds fly," ignoring the parent class's "Animals move."

- Through overriding, you can implement various behaviors using the same method name.


# 2023-08-29
## When Should I Use 'useCallback' in a React Component?

The primary reason for using useCallback is to prevent unnecessary re-renders and enhance performance. Each time a function component re-renders, a new function is created. If this function is passed as a dependency to other Hooks or components, those may also re-render.

However, you don't have to use useCallback in every case. Here are some considerations:

1. `Frequency of Re-rendering`: Check if your component re-renders frequently. If not, the likelihood is you don't need to use useCallback.

```jsx
import React, { useState, useCallback } from 'react';

const ChildComponent = ({ action }) => {
  console.log('ChildComponent 렌더링');
  return (
    <button onClick={action}>
      Click Me
    </button>
  );
};

const ParentComponent = () => {
  const [count, setCount] = useState(0);
  const [text, setText] = useState('');

  const increment = useCallback(() => {
    setCount((prevCount) => prevCount + 1);
  }, []);

  console.log('ParentComponent 렌더링');

  return (
    <div>
      <h1>{count}</h1>
      <ChildComponent action={increment} />
      <input
        type="text"
        value={text}
        onChange={(e) => setText(e.target.value)}
      />
    </div>
  );
};

export default ParentComponent;

// 부모에서 함수 사용했는데 자식에서 리렌더링 되는 현상을 방지
```


3. `Size and Frequency of the Dependency Array`: The usefulness of useCallback may vary depending on how often the values in the dependency array change and how large the array is.

4. `Function Complexity` : If the function is quite complex and time-consuming, it might be useful to use useCallback to reuse a previously created function.

5. ⭐⭐⭐`Passing to Child Components`: If you are passing this function as a prop to a child component and that child component is optimized with React.memo, then it’s beneficial to use useCallback.

In the case of the onRegistryUser function you shared, it contains asynchronous logic and state changes, making it complex. If this function is frequently called, or if there are frequent re-renders or it’s passed to child components, then using useCallback may be beneficial. Otherwise, it might not be necessary.


# 2023-08-30
## Foreign Key
### What is Forign Key? 
- In a Relational Database (RDB), a Foreign Key is a field (or a set of fields) in one table that **references the Primary Key** in another table. Foreign keys are used to ensure **data integrity** and play a crucial role in **maintaining Referential Integrity**.

### Key Functions of a Foreign Key:
1. **Ensuring Referential Integrity**: A column with a foreign key constraint can only have values that exist in the primary key column of the referenced table. This prevents incorrect or inaccurate data from being stored in the database.
2. **Establishing Relationships**: Foreign keys establish relationships between tables, allowing for efficient execution of JOIN operations.

### Example:
For instance, if there are Students and Courses tables, an Enrollments table can link these two tables together.

- The StudentID in the Students table serves as its Primary Key.
- The CourseID in the Courses table serves as its Primary Key.
- The StudentID and CourseID in the Enrollments table act as Foreign Keys, referencing the Primary Keys in the Students and Courses tables, respectively.

By doing this, the Enrollments table effectively represents which students are enrolled in which courses, while also ensuring data integrity.
