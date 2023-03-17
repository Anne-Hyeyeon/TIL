# Typescript Handbook by Captain Pangyo

### English ver. by Hykim 😺

# 👉 Basic Type of Typescript

## String

- In TypeScript, the "string" type is used to represent textual data. This declares a variable named myString that can only hold string values.

```js
let str: string = "hi";
```

# Number

- In TypeScript, the "number" type is used to represent numeric data. It is a versatile and powerful data type that allows you to work with numeric data in your programs.

```hs
let myNumber: number = 42;
```

# Boolean

- In TypeScript, the "boolean" type is used to represent logical values. A boolean variable can only hold one of two values: true or false.
- The boolean type in TypeScript is a simple yet powerful data type that allows you to represent logical values and make decisions based on them in your programs.

```js
let myBoolean: boolean = true;
```

# Array

- In TypeScript, the "Array" type is used to represent a collection of values of the same data type.

```js
let myArray: number[] = [1, 2, 3, 4, 5];
```

### TypeScript provides various methods and functions to work with arrays, including:

- `push(element: T)` : void: Adds an element to the end of the array.
- `pop(): T | undefined` : Removes and returns the last element of the array.
- `shift(): T | undefined` : Removes and returns the first element of the array.
- `unshift(element: T)`: number : Adds an element to the beginning of the array and returns the new length of the array.
- `slice(start?: number, end?: number)` : T[]: Extracts a section of the array and returns the extracted part as a new array.
- `splice(start: number, deleteCount?` : number, ...items: T[]): T[]: Adds or removes elements from an array at a specified index position.

# Tuple

- In TypeScript, a tuple is a data structure that represents an ordered list of elements of fixed types.

```js
let myTuple: [string, number] = ["Hello", 42];
```

- Tuples are useful when you want to represent a fixed set of related values, such as a coordinate pair or a date/time stamp.
- However, it's important to note that tuples have a fixed size and cannot be resized once they are created.

# Enum

- In TypeScript, an enum is a way to define a set of named constants with corresponding values.
- It allows you to define a named set of related constants that can be accessed using a keyword or an index.

```js
enum Color {
  Red,
  Green,
  Blue
}
```

- In this example, Color is the `name` of the enum, and Red, Green, and Blue are its `members`. By default, the `values` of the members are assigned starting from 0 and incrementing by 1 for each subsequent member. So, in this example, Red has a value of 0, Green has a value of 1, and Blue has a value of 2.
- You can access the members of an enum using either their name or their value. For example:

```js
console.log(Color.Red); // Output: 0
console.log(Color[0]); // Output: "Red"
```

- You can also assign specific values to enum members, like this:

```js
enum Color {
  Red = 1,
  Green = 2,
  Blue = 4
}
```

- In this example, Red has a value of 1, Green has a value of 2, and Blue has a value of 4.
- Enums are useful when you want to define a set of related constants that have specific values.
- They make your code more readable and maintainable by providing meaningful names for values that would otherwise be represented by numbers or strings.

# Any

- In TypeScript, the any type is a special type that can represent any type of value.
- It is used when you don't know or don't want to specify the type of a variable, parameter, or property at the time of declaration.

```js
let myVariable: any;

myVariable = 42; // valid
myVariable = "Hello"; // valid
myVariable = true; // valid
```

- While any can be useful in certain situations, it is generally discouraged to use it as it undermines TypeScript's static type checking and can lead to runtime errors if used incorrectly.
- This is because the any type does not provide any type safety guarantees, and it can result in unexpected behavior if you try to use a value of an incompatible type.

# Void

- In TypeScript, the void type is used to indicate that **a function does not return a value**.
- It is typically used as the return type of functions that perform some action or side effect, but do not produce a result.

```js
// In this example, the void type is used as the return type of the logMessage function, which means that it does not return a value.

function logMessage(message: string): void {
  console.log(message);
}

// In this example, the logAndReturnMessage function logs a message to the console and then returns void.

function logAndReturnMessage(message: string): void {
  console.log(message);
  return;
}
```

- When a function has a return type of void, you can still use the return statement inside the function, but you must not specify a value after the return keyword.

- The void type can also be used as the type of a variable, although it is not very common. When a variable has a type of void, it can only be assigned the value **undefined** or **null**.

# Never

- In TypeScript, the never type is used to represent values that **never occur**.
- This means that a function returning never will never return normally, and a variable of type never can **never be assigned a value**.

```js
// In this example, the throwError function always throws an error, which means it never returns normally. Therefore, its return type is never.

function throwError(message: string): never {
  throw new Error(message);
}
```

- Another use case for the never type is as the inferred type of functions with infinite loops or unreachable code:

```js
function infiniteLoop(): never {
  while (true) {}
}

function unreachableCode(): never {
  throw new Error("This code is unreachable");
}
```

- In these examples, the functions infiniteLoop and unreachableCode never return normally, so their return types are inferred as never.

# 👉 Functions in TypeScript

# Basic type declarations for functions

```js
function sum(a: number, b: number): number {
  return a + b;
}
```

- This is the basic function declaration syntax with added types to the parameters and return value of the function.

* Even if no type is specified for the return value of a function, use 'void'.

# Argument in functions

- In TypeScript, all function `parameters` are considered **required values**.
- Therefore, even if the parameter is expected to be `undefined or null`, you must pass it as an argument, and the compiler checks whether the defined parameter value has been passed.
- In other words, this means that you can only receive the **defined parameter** values and cannot receive additional arguments.
- If you want to remove this feature and not define required parameters like in regular JavaScript, you can use **?** to define optional parameters like the following:

```js
function sum(a: number, b?: number): number {
  return a + b;
}
sum(10, 20); // 30
sum(10, 20, 30); // error, too many parameters
sum(10); // no type error
```

- Parameter initialization is the same as the ES6 syntax.

```js
function sum(a: number, b = "100"): number {
  return a + b;
}
sum(10, undefined); // 110
sum(10, 20, 30); // error, too many parameters
sum(10); // 110
```
