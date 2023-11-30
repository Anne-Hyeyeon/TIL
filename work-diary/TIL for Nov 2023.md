# 2023-11-01
## Typescript에서 any 타입을 쓰는 것에 대한 GPT의 답변
- 타입스크립트의 주요 이점 중 하나는 코드의 정확성을 향상시키고 버그를 줄이기 위해 더 엄격한 타입 체킹을 제공하는 것입니다. any 타입을 사용하면 타입스크립트의 이러한 이점을 상당 부분 포기하는 셈이 되죠. 실제로 any 타입은 **타입 체킹을 효과적으로 비활성화시키고**, **자바스크립트와 거의 동일**하게 만듭니다.

- ### 그럼에도 불구하고 any 타입을 써야 하는 경우는 언제야?

1. **외부 라이브러리**: 타입 정의가 없거나 불완전한 외부 자바스크립트 라이브러리를 사용할 때 `any`를 사용할 수 있습니다. 하지만 대부분의 유명 라이브러리들은 DefinitelyTyped 같은 커뮤니티를 통해 타입스크립트 타입 정의를 제공하므로, 먼저 이를 확인해 보는 것이 좋습니다.
    
2. **매우 복잡한 타입**: 일부 복잡한 객체나 함수의 경우, 타입을 정의하기가 매우 어렵거나 불가능할 수 있습니다. 이 경우 `any`를 사용할 수 있지만, 이는 일시적인 해결책이어야 하며, 더 나은 타입 정의를 위해 지속적으로 노력해야 합니다.
    
3. **동적 콘텐츠**: 사용자 입력이나 서버에서 동적으로 가져온 데이터처럼 런타임에만 알 수 있는 타입을 다룰 때 `any`를 사용할 수 있습니다. 하지만 이런 경우에도 `unknown` 타입을 사용하고 타입 가드를 통해 타입을 좁혀 나가는 것이 더 좋은 접근법입니다.
    
4. **마이그레이션 프로젝트**: 기존의 자바스크립트 프로젝트를 타입스크립트로 전환하는 과정에서 모든 타입을 한 번에 정의하기 어려울 수 있습니다. 초기 단계에서 일시적으로 `any`를 사용하되, 점차적으로 구체적인 타입으로 교체해 나가야 합니다.
    
`any` 타입은 타입스크립트의 안전망을 제거하므로, 코드의 안정성과 가독성을 떨어뜨릴 수 있습니다. 가능한 한 `any` 사용을 피하고, 필요한 경우에는 그 사용 이유를 명확히 주석으로 남겨 다른 개발자들이 이해할 수 있도록 하는 것이 좋습니다.



# 2023-11-03
## `!important` in CSS
### Understanding `!important` in CSS

- The `!important` rule in CSS is employed to elevate the priority of a specific style declaration to the highest level.
- CSS, standing for "Cascading Style Sheets," embodies the principle of "Cascading," indicating that styles are applied according to a predefined hierarchy of importance.
- This hierarchy is influenced by several elements, such as selector specificity, the order in which styles are declared, and inheritance patterns.
- `!important` supersedes these conventional rules, asserting its marked declaration as the most crucial.

```css
p {
    color: red !important;
}
p {
    color: blue;
}
```

- In the scenario illustrated above, the text within the `<p>` tags would adopt a red hue, as the `!important` rule negates the subsequent declaration.

### When is `!important` Necessary?

1. **User-defined Styles**: For reasons pertaining to accessibility, certain users may need to enforce specific styles, such as a high-contrast mode.
2. **Overriding Library Styles**: When attempting to alter styles instituted by third-party libraries or frameworks, the application of `!important` might become necessary to supplant preexisting styles.
3. **Provisional Remedies**: During the developmental phase, quick fixes for styling complications in complex stylesheets might warrant the temporary use of `!important`.

### The Pitfalls of Overusing `!important`

1. **Maintenance Challenges**: The introduction of `!important` disrupts the intrinsic cascade of stylesheets, potentially leading to confusion during subsequent code modifications or updates.
2. **Escalation of Specificity**: The use of `!important` in one style declaration may compel other developers to employ `!important` for similar properties, culminating in escalated code complexity.
3. **Debugging Difficulties**: The presence of `!important` complicates the debugging process of styling issues. Pinpointing the source of unexpected styling behaviors becomes increasingly arduous.
4. **Performance Implications**: An excessive reliance on `!important` rules can prolong the CSS processing time for browsers, thereby detrimentally impacting webpage performance.

### Conclusion

In essence, while `!important` can be a useful tool in certain contexts, its judicious application is recommended. Addressing styling challenges through a more systematic approach, such as leveraging CSS classes, IDs, inline styles, and understanding selector specificity, proves to be a more sustainable strategy in the long term.


# 2023-11-06
## understanding `order` in CSS
- The `order` property in CSS is used to **adjust the order of items within a Flexbox layout**.
- By default, the child elements of a Flexbox container are laid out in the order they appear in the source code. However, the order property allows you to **change this order without altering the HTML structure or the DOM order**; it only affects the visual presentation.

- The default value of the order property is 0, and it can take positive or negative numbers. Lower numbers will place items earlier in the visual layout. For example, an item with order: 1; will be positioned before an item with order: 2;.

### Example
```html
<div class="container">
  <div class="item">1</div>
  <div class="item">2</div>
  <div class="item">3</div>
</div>
```
```css
.container {
  display: flex;
}

.item:nth-child(1) {
  order: 2;
}

.item:nth-child(2) {
  order: 3;
}

.item:nth-child(3) {
  order: 1;
}
```
- In the example above, the first item has order: 2; so it moves to the third position. The third item has order: 1;, so it moves to the first position. As a result, the order of items as they appear on the screen will be **3, 1, 2**.

- The order property can be particularly useful in responsive design, helping to rearrange the order of content based on screen size or resolution.

# 2023-11-07
## Understanding Real-time Object References in Console Logging

To comprehend how the console log displays real-time references to objects, we must examine both the properties of objects in JavaScript and the functionality of the browser console.

### Example of JavaScript Object References
```js
let myObject = { name: "ChatGPT", likes: "coding" };
console.log(myObject); // Logs { name: "ChatGPT", likes: "coding" } to the console

// Changing a property of the object
myObject.name = "GPT-4";

// When the console log is expanded, you can see the name property has been changed to "GPT-4".
```

In the code above, when we log `myObject`, the state of the object at that moment is printed to the console. However, if we alter the properties of the object after logging it, and then expand the logged object in the console, we can see the updated values.

### How the Browser Console Operates

1. **Initial Logging**: In the browser's developer tools, we log `myObject` to the console for the first time.

```js
console.log(myObject); // Logs { name: "ChatGPT", likes: "coding" } to the console
```

2. **Viewing the Object in the Console**: The object logged to the console is not immediately expanded, so its actual values are not visible yet.

3. **Modifying the Object**: After logging, the object's `name` property is changed to "GPT-4".

```js
myObject.name = "GPT-4";
```

4. **Viewing Updated Values Upon Expansion**: Now, when we expand the initially logged object in the console, it shows the updated value "GPT-4" rather than the original value "ChatGPT". This is because the console records a "reference" to the object, not a "snapshot" of it.

### The Meaning of Real-time References

This behavior is due to the way JavaScript handles objects as "reference types." The object logged in the console represents a reference to the object stored in memory. Hence, when properties of this object are modified elsewhere in the code, those changes are reflected immediately in memory. The console references this memory address to represent the current state, so if the object has been altered after being logged, the console will reflect the updated state when expanded.

### Considerations for Debugging

This functionality of the console can cause confusion for developers when tracking the state of objects through logs, as the state of a logged object can change over time. Therefore, to accurately understand the state of an object, one might need to output new logs whenever changes are made, or take measures to maintain immutability, such as copying the object.


# 2023-11-08
## Resolving Overwritten CSS Display Property Issues

**The Situation:** I applied `display: flex;` to an HTML element, but when I checked the page, it was overridden with `display: block;`. This happened because two CSS selectors were trying to apply different `display` properties to the same element.

```css
.customDropdown .optionContent .optionItem {
    display: flex;
    /* other styles */
}
.settingsPriority .optionItem {
    display: block;
    /* other styles */
}
```

**The Solution:** The second selector has higher specificity or comes later in the stylesheet, thus overriding `display: flex;`. To fix this, I tried the following methods:

1. **Increasing Specificity:** Create a selector with higher specificity to reinforce the first rule.
2. **Using `!important`:** Add `!important` to `display: flex;` to ensure this rule takes precedence. (However, be cautious as this can affect the readability and maintainability of your stylesheet.)
3. **Re-evaluating HTML Structure:** Reassess the HTML markup to ensure selectors don't apply to the same element simultaneously.

Eventually, I resolved the issue by increasing the specificity of the first selector. It allowed me to apply the desired styles and helped me realize the importance of understanding specificity in managing CSS complexity.

**Lessons Learned:** In CSS, the order of precedence in applying styles is crucial. A good grasp of specificity can effectively solve style conflict issues. And while `!important` can be useful, it should be used sparingly.

This simple experience enhanced my understanding of the intricacies of CSS. I plan to continue adding such insights to my TIL, so if you're interested in diving deeper into CSS, stay tuned for more!


# 2023-11-10
## Rest Parameter Syntax

The "Rest Parameter" syntax in JavaScript and TypeScript is a useful feature that allows you to represent an indefinite number of arguments as an array. This is particularly useful when you want to handle multiple parameters in a function without specifying each one individually. 

### Basic Concept:

1. **Syntax**: Rest parameters are denoted by three dots (`...`) followed by the name of the array that will contain the rest of the parameters.
2. **Usage**: They are used in function definitions. For instance, in a function `function sum(...numbers)`, `numbers` is an array containing all the passed arguments.

### In Destructuring:

In the context of object destructuring, as shown in your example, the rest parameter is used to gather the remaining (unassigned) properties of an object.

### Example in Object Destructuring:

```tsx
type BasicData = {
  assetImportance: string;
  name: string;
  age: number;
  [key: string]: any; // Allows any number of additional properties
};

const extractData = ({ assetImportance, ...rest }: BasicData) => {
  // 'rest' now contains all properties of BasicData except 'assetImportance'
  return rest;
};

const data = {
  assetImportance: 'High',
  name: 'John',
  age: 30,
  country: 'USA'
};

const newData = extractData(data);
// newData will be: { name: 'John', age: 30, country: 'USA' }

```

In this example, `extractData` function uses rest parameters to collect all properties of `BasicData` except `assetImportance` into a single object (`rest`), which it then returns.

### Key Points:

- **Order Matters**: The rest parameter must be the last in the destructuring pattern.
- **Flexibility**: This syntax provides a flexible way to handle an object with varying numbers of properties.
- **Clean and Readable**: Using rest parameters can lead to cleaner and more readable code, especially when dealing with multiple properties or optional properties.

In summary, the rest parameter syntax in JavaScript and TypeScript is a versatile feature for handling multiple function arguments or object properties, making the code more adaptable and concise.



# 2023-11-27
## UI에서 자식 요소들의 렌더링이 다 끝났음을 확인할 수 있는 지표가 있을까?
### 상황 설명
- 리스트가 있다. 각 리스트에는 'expanded(확장)' 버튼을 통해 하위 요소를 볼 수 있는 기능이 있다.
- 화면 오른쪽에는 '모두 펼쳐보기/모두 닫기'버튼이 있다.
- '모두 펼쳐보기/닫기'는 말 그대로 하위 요소의 확장을 결정하는 버튼이다.
- 특이사항은, '모두 펼쳐보기'값은 로컬스토리지에 저장된다는 것. '모두 펼쳐보기'상태일 때는 사용자가 다음에 들어올 때도 하위 요소가 모두 펼쳐져야 한다. 
- 여기서 문제 🌟🌟 개발자는 모든 하위 요소가 확장되었을 때, 사용자에게 그것을 알려주는 알람 하나를 넣어주고 싶다. (ex. alert으로 '확장 완료!')
- 그러기 위해서는 하위 요소들의 렌더링이 모두 끝났음을 확인하는 장치가 있어야 한다.

### 질문
- 모든 하위 요소들의 렌더링이 끝났음을 보장하는 알려주는 장치를 만들 수 있을까?

### 결론
- 리액트 컴포넌트에서 모든 자식 요소의 렌더링이 완료되었음을 직접적으로 확인할 수 있는 방법은 **없다.**

### 시도
- useEffect 내 return문으로 clear 함수를 만듦. -> 컴포넌트가 unMount 될 때 실행됨. 원하는 결과 아님.
- 리스트의 요소마다 렌더링이 끝났음을 알리는 함수를 만듦 -> 하나가 완료되면 나머지가 완료되지 않았음에도 불구하고 완료 처리가 됨.

