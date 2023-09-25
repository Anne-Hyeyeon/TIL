# 2023-09-01
![image](https://github.com/Anne-Hyeyeon/TIL/assets/93920435/730b3db7-9c98-4de2-b8bd-135d252e9b7b)
## 컴파일 타입 체크 (Compile-time type Check)
타입스크립트에서는 기본으로 두 종류의 타입 체크가 있다.

1. 컴파일 타임 타입 체크: 이 부분이 타입스크립트의 핵심 중 하나다. 소스 코드를 컴파일할 때 타입을 검사한다. 이 과정에서 타입 오류가 나면 컴파일이 실패한다. 대부분의 타입 정보는 컴파일 후에 사라진다.

2. 런타임 타입 체크: 타입스크립트는 런타임에 대한 타입 검사를 기본으로 제공하지 않는다. 그래서 런타임에서 타입을 체크해야 할 필요가 있으면 직접 코드를 작성해야 한다.

타입스크립트의 몇몇 고급 기능은 실제로 컴파일된 JavaScript 코드에도 영향을 줄 수 있다. 예를 들어, const enum은 런타임에는 없는 특별한 열거형을 만드는데, 이건 타입스크립트 컴파일러가 특별하게 다룬다.

타입스크립트에서 여러 요소가 컴파일 시 타입 체크와 관련이 있다. **네임스페이스, 타입, 값, 열거형, 함수, 변수, 클래스** 등이 이에 포함된다. 이런 요소들의 타입은 컴파일 타임에 체크되어서 프로그램이 안정적으로 동작할 수 있도록 도와준다. 대부분의 타입 정보는 런타임에는 사라지지만, 몇몇 특별한 경우에는 런타임에서도 영향을 준다.

 
<img src="https://github.com/Anne-Hyeyeon/mystorage/blob/main/declare2.png?raw=true" />


1. **네임스페이스**: 보통 타입과 값 둘 다에 적용되지만 컴파일할 때 네임스페이스 내의 타입과 인터페이스를 검사한다.

2. **타입**: 컴파일할 때 변수나 함수 매개변수, 반환 값 등의 타입을 확인한다.

3. **값**: 값 자체는 런타임에 존재하지만, 그 타입은 컴파일할 때 확인된다.

4. **enum**: enum은 런타임과 컴파일 시간 모두에 존재할 수 있다. 반면에 const enum은 컴파일할 때 인라인으로 바뀌기 때문에 런타임에는 없다.

5. **함수** : 함수의 매개변수 타입이나 반환 타입 같은 것들은 컴파일 시간에 확인한다.

6. **변수**: 변수의 타입도 컴파일할 때 확인한다. let, const, var로 선언된 변수의 타입 정보는 이 때 사용된다.

7. **클래스*: 클래스의 프로퍼티나 메서드, 생성자 등의 타입은 컴파일할 때 검사한다. 클래스 자체는 런타임에도 존재하고, 인스턴스를 만들면 해당 타입의 객체가 런타임에 생성된다.



# 2023-09-11
## Named Exports
Named exports are a feature of JavaScript's ES6 module system that allows multiple values to be exported from a single module.

### Characteristics:
`Clarity`: Each export has its own unique name. This provides clarity for the module's users about what values they can import from it.
`Multiple Value Exports` : A module can export multiple values.
`Destructuring` : When using named exports, one can utilize destructuring to selectively import the values they want.

### How to use:
- Exporting:
```js
// module.js
export const functionA = () => { /* ... */ }
export const functionB = () => { /* ... */ }
export const valueC = 123;
```

- importing: 
```js
// anotherModule.js
import { functionA, functionB, valueC } from './module';
```

- Rename the imports:
```js
import { functionA as newFunctionA, functionB } from './module';
```

### Pros and Cons:
1)Pros:
- Useful when you have multiple values to export.
- Provides clear visibility to readers about what the module offers.
- Provides flexibility by allowing selective imports of functions or values.

2) Cons:
- You have to use the exact name as it was exported (although renaming is possible).
- an sometimes add **unnecessary complexity**, especially if a module exports a large number of values.
In conclusion, named exports are beneficial when a module needs to provide multiple values, especially when **each value has a clear meaning and role**.
- However, there are cases where it might be more appropriate to export just a single value or main functionality. It's important to choose the right approach based on the situation.


# 2023-09-14
## clean-up logic on useEffect

### What is the Cleanup Logic?
- When using the useEffect hook, you might create subscriptions, timers, or even manually manipulate the DOM. Over the life of a component, these side effects might need to be cleaned up to prevent memory leaks, unhandled events, or unexpected behaviors.

- To specify this cleanup, the function passed to useEffect can return a function. This returned function is the cleanup function.

### When does the Cleanup Logic Run?
- Before re-running the side effect: If the useEffect hook has dependencies and the dependencies change, before running the effect again, React will first perform the cleanup of the previous effect.

- Component Unmount: When the component using the effect is removed from the UI, React ensures the cleanup function is called. This behavior ensures that any lingering side effects are disposed of before the component is fully unmounted.

```ts
useEffect(() => {
    // This might be a subscription to a data stream or event listeners, etc.
    const subscription = someService.subscribe(data => {
        // Do something with the data
    });

    // Cleanup logic
    return () => {
        // Unsubscribe when the component unmounts or if the effect reruns
        subscription.unsubscribe();
    };
}, []); // Empty dependency array means this effect runs once on mount and the cleanup runs on unmount
```

### Important Note:
If your useEffect does not have a cleanup function and **you're seeing memory leaks or unexpected behavior**, it's possible you need to add one. On the other hand, if you have a cleanup function but are experiencing performance issues or flickering, it's possible that your useEffect is running more often than necessary. **Always ensure your dependency array is correctly specified to prevent effects** and their cleanup from running excessively.

- Remember, the goal of the cleanup function is **to reset everything to its original state** or to ensure that no lingering side effects remain. It's an essential tool in ensuring the robustness of React components that deal with side effects.



# 2023-09-15
## Class Naming Conventions for Better Code

1. `Make it meaningful`: The className should reflect the **purpose or content** of the element. For example, for a div representing a user's profile picture, you might use a name like profile-picture.

2. `Consider using BEM` (Block Element Modifier): BEM is one of the well-known methodologies for naming CSS classes. The main principles of BEM are:

### BEM
- Block: An independent entity (e.g., button)
- Element: A component within the block (e.g., button__icon)
- Modifier: A variant or state of the block or element (e.g., button--large)
- Short but clear: Class names should be concise yet clear in conveying the purpose or content of the element. E.g.: btn-submit, header-title

3. `Use kebab-case`: CSS class names typically use **kebab-case** (words in lowercase connected by hyphens). E.g.: user-profile, main-content

4. `Avoid names related to structure`: Avoid names related to layout or position like **left, right, top, bottom**. This is because if the design or layout changes, these names may no longer be appropriate.

5. `Use names related to state` : For classes representing a **state or change**, use names indicating the state such as **active, disabled, collapsed**.

6. `Maintain consistency` in your code: It's crucial to use consistent naming conventions throughout the project. For instance, if you're using the prefix btn for all buttons, stick to it consistently.

- Following these principles enhances code readability, facilitates collaboration among team members, and helps in easily understanding the purpose or state of an element when modifying CSS or JS in the future.

```css
/* 블록 */
/* Block: Represents the main button */
.button {
  background-color: blue;
  border: none;
  border-radius: 4px;
  color: white;
  padding: 10px 20px;
  text-align: center;
  text-decoration: none;
}

/* Element: Text inside the button */
.button__text {
  font-size: 16px;
  font-weight: 500;
}

/* Modifier: A large version of the button */
.button--large {
  padding: 15px 30px;
}

/* Modifier: Button with a red background */
.button--danger {
  background-color: red;
}

/* Modifier: Highlighted text inside the button */
.button__text--highlighted {
  font-weight: 700;
  color: yellow;
}

/* Modifier: Small text inside the button */
.button__text--small {
  font-size: 12px;
}
```
# 2023-09-19
## useQuery


**useQuery** is a foundational hook provided by React Query for fetching, caching, and syncing asynchronous data in React applications.

1. **Declarative Data Fetching**: By simply providing a key and an asynchronous function, `useQuery` fetches the data and manages its state transitions from loading to success or error.

2. **Caching**: Once data is fetched, `useQuery` automatically caches the result. Subsequent calls with the same key will return the cached data without needing to re-fetch.
    
3. **Automatic Refetching**: It supports options for background refetching when the window refocuses or network connectivity is regained.
    
4. **Error and Loading States**: `useQuery` provides out-of-the-box states for handling loading and error scenarios.
    
5. **Stale Data Handling**: Allows data to be considered "stale" after a certain period, prompting refetches when stale data is accessed.
    
6. **Retry Mechanism**: In case of failure, `useQuery` can be configured to retry fetching a certain number of times.



# 2023-09-22
## Comparing Translation Strategies: Individual vs. Dynamic Approach

### Problem
-When translating the phrase "원격 연결 IP 입력" into English, the sequence of words changes, primarily due to the word "입력," which translates to "Enter." For instance:
```
Korean: 원격 연결 IP 입력
English: Enter Remote Connection IP
```

- Similarly, phrases like "SSH on Port 입력," "Telnet on Port 입력," and "Password 입력" will require continual translations for placeholders.

Given this, two approaches arise:

1. Individual Translations: Craft a unique translation for each phrase.
2. Dynamic Translation Function: Based on the user's language preference stored in localStorage, design a function that positions the word "Enter" appropriately depending on the language version (e.g., moving it to the front for the English version).

### Solving

**Individual Sentence Translation**: This approach involves pre-saving translations for every sentence. It is very clear and predictable. It also helps in understanding the context of the translated sentences.

**Advantages**:

- **Clarity**: You know exactly how each sentence will be translated.
- **Flexibility**: There's flexibility in adjusting the translation for each sentence.

**Disadvantages**:

- **Maintenance**: Every time a new sentence is added or an existing one is changed, translations for all languages need to be updated.

**Using a Dynamic Translation Function**: Write a function that offers dynamic translation capabilities for specific words or phrases like "입력". This function changes the sentence structure based on the chosen language.

**Advantages**:

- **Consistency**: The same treatment is applied to all sentences with a consistent structure.
- **Maintenance**: If new sentences with the same pattern are added, there's no need to add separate translations.

**Disadvantages**:

- **Complexity**: Sentence structures differ among languages, making the function's logic potentially complex.
- **Exception Handling**: For some sentences, the dynamic conversion logic might not be appropriate.

**Decision Making**:

- If simplicity and predictability are vital, opting for individual translations for each sentence would be best.
- If you prefer flexibility and automation, then you might choose to use a dynamic translation function.

**Personal Opinion**: Initially, using individual translations for each sentence seems like a better choice. As time goes on and many sentences with similar patterns are added, introducing a dynamic translation function could be considered.


# 2023-09-25
## How Flex vs. Width Resizing Impacts Table Layouts in Web Design

### 1. Resizing with Flex:

#### Advantages:

1. **Fluidity**: One of the main benefits of Flexbox is its fluid distribution of space amongst items. It makes adjusting the size of items within a container straightforward.
2. **Proportional Distribution**: With `flex-grow` and `flex-shrink`, items can automatically adjust based on available space.
3. **Content-Based Sizing**: Flex items can adjust their size automatically based on their internal content.
4. **Easy Alignment**: Flexbox makes it easy to center items or align them vertically/horizontally.

#### Disadvantages:

1. **Browser Support**: Older browsers might not fully support Flexbox.
2. **Complexity**: Some users might find the properties and behavior of Flexbox a bit complicated.

### 2. Resizing with Width:

#### Advantages:

1. **Simplicity**: It's easy to set the width of table columns in pixels, percentages, or other units.
2. **Predictability**: With a specified width value, the layout behavior is predictable.
3. **Browser Support**: The `width` property is well-supported across all browsers.

#### Disadvantages:

1. **Lack of Fluidity**: Table columns with a fixed width value might be more challenging to adjust fluidly.
2. **Manual Adjustments**: You may need to update the code whenever adjustments to the layout are necessary since the width of each column is set manually.
3. **Content Overflow**: If the content doesn't fit within the specified width, overflow issues can arise.

### Conclusion:

- Using `flex` is advantageous when aiming for a fluid layout and pairs well with responsive design.
- Using `width` is suitable when you want predictable behavior or precise control over the layout.

Ultimately, the choice depends on the desired functionality, the browsers that need to be supported, and the complexity of development.

