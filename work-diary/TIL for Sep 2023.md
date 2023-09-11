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


## 2023-09-11
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
