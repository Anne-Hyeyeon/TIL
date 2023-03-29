
# 2023-03-01
## combineReducers from Redux-toolkit
### conbineReducers : It allows you to combine `multipile reducers` into a singler reducer function.
- It is useful when you have `multiple features` in your application that each requires their own slice of state and teir own reducer.
- You can combine these redcers into a `single root` reducer that can be passed to the Redux 'createStore'
```js
import { combileReducers } from '@reduxjs/toolkit';
import { counterSlice } from './counterSlice';
import { todoSlice } from './todoSlice';

const rootReducer = combineReducers({
  counter: counterSlice.reducer,
  todo : todoSlice.reducer,
});

export default rootReduer;
```

# 2023-03-06
## createSlice from Redux-Toolkit 
### createSlice : A uility function provided by Redux-Toolkit.
- It allows to define a slice of state and its `associated reducer` in a concise manner.
- with createSlice, you can define an object that contains slice name, initial state, and a set of reducer functions.
#### concise manner ? writing code that is clear,  easy to read, and efficient using the fewest lines of code.


# 2023-03-09
## Troubleshooting: What Happened with the Delete Logic in Checkbox?
### The following code is the delete slice that I used in my program.
#### The value of itemLists
```js
const itemLists = {
fruits: [],
cookies: [],
drinks: ['orange juice', 'coffee', 'fountain drink', 'coke']
}
```

#### deleteItem function
```js
    deleteItems: (state) => {
      const itemLists = cloneDeep(state['itemInfo']);
      state['includedItem'].forEach((item) => {
        const { flagNumber } = item;

        Object.keys(itemLists).forEach((key) => {
          const nkey = key as keyof typeof itemLists;
          const findIndex = itemLists[nkey].findIndex((el) => el.flagNumber === flagNumber);
            itemLists[nkey].splice(findIndex, 1);
        });
      });
    }
```
- There was a problem with this code: the "splice" method is executed multiple times, even though I only call the delete function once.
- When I logged the value of "findIndex," I noticed that it returned "-1" twice before returning the index of the deleted item.
- As a result, the "splice" method is called more than twice, leading to unintended deletion of an item that I didn't mean to delete.

```js
console.log(`itemList: ${itemLists}`);
console.log(`nkey: ${nkey}`);
console.log(`itemLists[nkey] : ${itemLists[nkey]}`);
console.log(`flagNumber : ${flagNumber}`);
console.log(`findIndex: ${findIndex}`);
```
- To diagnose the error, I logged all values that I suspected might have caused it.
- Through this process, I discovered that the problem was caused by the "forEach" method used in the function. Specifically, the "Object.keys(itemLists).forEach..." code caused the program to loop through the "fruits," "cookies," and "drinks" values in that order.
- When it looped through the "fruits" and "cookies" values, which had no length, the "const findIndex" code returned "-1."

```js
    deleteItems: (state) => {
      const itemLists = cloneDeep(state['itemInfo']);
      state['includedItem'].forEach((item) => {
        const { flagNumber } = item;
        Object.keys(itemLists).forEach((key) => {
          const nkey = key as keyof typeof itemLists;
          const findIndex = itemLists[nkey].findIndex((el) => el.flagNumber === flagNumber);
          if (findIndex !== -1) {
            itemLists[nkey].splice(findIndex, 1);
          }
        });
      });
    }
```
 - I added a new condition that distinguishes whether the value of "findIndex" is "-1" or not.
 - As a result, the "splice" method now only executes when the value of "findIndex" is not "-1," preventing it from removing unrelated items.
 - Overall, this modification ensures that the deletion function works properly and removes the intended item only.
 
# 2023-03-17
## A parameter with the REST syntax 
- A parameter with the REST syntax in JavaScript is denoted by three dots (...) followed by a parameter name.
```js
function sum(a: number, ...nums: number[]): number {
  const totalOfNums = 0;
  for (let key in nums) {
    totalOfNums += nums[key];
  }
  return a + totalOfNums;
}
```
-  It allows you to represent an `indefinite number of arguments` as an array.
-  When a function is called with arguments, the REST parameter takes in all the remaining arguments after the other parameters have been assigned.
```js
function myFunction(a, b, ...rest) {
  console.log(`a = ${a}`);
  console.log(`b = ${b}`);
  console.log(`rest = ${rest}`);
}

myFunction(1, 2, 3, 4, 5);

```
- The output of the above code will be:
```css
a = 1
b = 2
rest = 3,4,5
```
- The REST parameter is useful when you need to work with a varying number of arguments in a function.

# 2023-03-23
## keyof in Typescript.
- In TypeScript, the keyof keyword is used to **obtain a union type of all possible property keys of a given object type**
- It allows you to capture the keys of an object in a type-safe way, enabling you to write code that ensures that property accesses are valid at `compile-time`, rather than at runtime

```js
interface Person {
  name: string;
  age: number;
  email: string;
}
```
- To obtain a union type of all possible property keys of the Person type, you can use the keyof keyword as follows:
```js
type PersonKeys = keyof Person; // "name" | "age" | "address"
```
- The resulting PersonKeys type would be a **union type** of the three property keys, 'name', 'age', and 'email'.
- This type can then be used to enforce type safety when accessing properties of a Person object, as shown below:
```js
function getPersonProperty(person: Person, key: PersonKeys) {
  return person[key]; // This is type-safe because the `key` argument is guaranteed to be a valid property key of `Person`.
}

const person: Person = { name: 'John Doe', age: 30, email: 'john.doe@example.com' };
const name = getPersonProperty(person, 'name'); // This is valid because `'name'` is a valid property key of `Person`.
const address = getPersonProperty(person, 'address'); // This will result in a compile-time error because `'address'` is not a property key of `Person`.
```
- In this example, the key parameter is restricted to the keys of the Person interface, so it can only be "name", "age", or "address". This helps us write more type-safe code.

Overall, keyof is a powerful tool in TypeScript that allows us to work with object keys in a type-safe way.


# 2023-03-28
## typeof in Typescript.
- `typeof` in TypeScript is an operator that returns the data type of a value or variable at runtime.
- It is a type query operator that allows you to obtain the static type of a variable or value, as defined in your TypeScript code.
- For example, you can use the typeof operator to obtain the data type of a variable like this:

```ts
const someValue = 10;
console.log(typeof someValue); // Output: "number"
```
- You can also use typeof to create type guards that allow you to conditionally execute code based on the type of a variable. Here's an example:

```ts
function logValue(value: string | number) {
  if (typeof value === "string") {
    console.log("The value is a string: " + value);
  } else if (typeof value === "number") {
    console.log("The value is a number: " + value);
  } else {
    console.log("The value is of an unknown type.");
  }
}
logValue("hello"); // Output: "The value is a string: hello"
logValue(42); // Output: "The value is a number: 42"
```

- In this example, the typeof operator is used to determine whether the value parameter is a string or a number. Based on the result of the type check, the function prints a message to the console.


# 2023-03-29
## What is TypeScript and why is it used?
### I wrote it by myself without any reference 👍 
- TypeScript is a `superset of JavaScript`, which means it is an upgraded version of the language with added features. 
- Some of the commonly used types in TypeScript include strings and numbers, among others. 
- JavaScript, on the other hand, is not a type-sensitive language. When programming in JavaScript, there is no way to inform the computer whether a particular value is a string or a number.
- While one might question the need for this, **understanding the type of a value beforehand is crucial in the world of computers. **
- We ourselves need to know the type of food we are about to eat to avoid choking. Similarly, just by receiving the type of a value beforehand, a program can increase its stability, and prevent bugs from occurring.
- TypeScript also offers several additional features such as previewing, among others, which enhances **developer productivity. **
- In fact, there are hardly any companies today that develop solely in JavaScript, as many are using TypeScript for their projects. 
- While it is possible to develop programs in JavaScript alone, knowing TypeScript is essential for developing `stable web pages` and `improving employability.`
