
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
 

