# Chpater 2. 타입 시스템

## 2.1 타입의 종류

- 타입(Type) : 자바스크립트에서 다루는 `값의 형태`에 대한 설명.
- 형태 : 값에 존재하는 **속성, 매서드** 그리고 내장되어 있는 **typeof** 연산자가 설명하는 것  
  **일곱 가지 원시 타입**

```
- null
- undefined
- boolean
- string
- number
- bigint
- symbol
```

- 변수의 원시 타입 찾는 법 : IDE에서 원싯값 찾는 `let`변수 이볅한 후 변수 이름 위로 마우스를 가져가면 된다.
- 타입스크립트의 특징 중 하나는 바로 계산된 초깃값을 갖는 변수의 타입을 유추하는 것이다.

### 2.1.1 타입 시스템

- 타입 시스템 : 프로그래밍 언어가 프로그램에서 가질 수 있는 `타입을 이해하는 방법`에 대한 규칙 집합\

### 2.1.2 오류 종류

- 타입스크립트에서 접하게 되는 오류 두 가지
  (1) **구문 오류** : 타입스크립트가 자바스크립트로 변환되는 것을 차단한 경우
- 구문 오류는 타입스크립트가 **코드로 이해할 수 없는 잘못된 구문을 감지할 때** 발생한다.
- 타입스크립트가 타입스크립트 파일에서 자바스크립트 파일을 올바르게 생성할 수 없도록 차단한다.
  (2) **타입 오류** : 타입 검사기에 따라 일치하지 않는 것이 감지된 경우
- 타입 오류는 타입 검사기가 프로그램의 타입에서 오류를 감지했을 때 발생한다.
- 타입스크립트는 타입 오류가 있음에도 불구하고 자바스크립트 코드를 출력할 수는 있지만, 코드가 원하는 대로 실행되지 않을 가능성이 있다는 신호를 타입 오류로 알려준다.
- 자바스크립트 실행 전 타입 오류를 확인하고 문제를 먼저 해결하는 것이 중요하다.

#### 어떤 프로젝트는 구문뿐만 아니라 모든 타입스크립트 오류가 수정될 때까지 코드 실행을 차단하기도 한다. tsconfig.json파일을 이용해 이를 바꿀 수 있다.

## 2.2 할당 가능성

- `할당 가능성` : 함수 호출이나 변수에 값을 제공할 수 있는지 여부를 확인하는 것.
- 타입스크립트는 우선 1) 변수의 초깃값을 읽고 2) 해당 변수가 허용되는 타입을 결정한다.
- 나중에 해당 변수에 새 값이 할당되면, 새롭게 할당된 값이 초기에 읽은 타입과 일치하는지를 확인한다.

## 2.3 타입 애너테이션

#### 변수에 타입스크립트가 읽어야 할 초깃값이 없는 경우에는 어떻게 할까?

- 타입스크립트는 나중에 사용할 변수의 초기 타입을 파악하려고 시도하지 않는다.
- 그리고 기본적으로 변수를 `암묵적인 any`타입으로 간주한다. -> 변수는 세상의 모든 것이 될 수 있음을 나타냄.
- `진화하는 any` : 초기 타입을 유추할 수 없는 변수, 특정 타입을 강제하는 대신 새로운 값이 할당될 때마다 변수 타입에 대한 이해를 발전시킨다.

```ts
let rocker; // 타입 : any

rocker = "Hyeyeon Kim"; // 타입 : string

rocker.toUpperCase(); // Ok

rocker = 19.58; // 타입 : number
rocker.toPrecision(1); // Ok

rocker.toUpperCase();
// Error: 'toUpperCase' does not exist on type 'number'.
```

- 위 문제를 해결하려면 어떻게 해야 할까? **타입 애너테이션** : 초깃값을 할당하지 않고도 변수의 타입을 선언할 수 있는 구문 사용

```ts
let rocker: string;
rocker = "Hyeyeon";
```

- 타입 애너테이션은 타입스크립트에만 존재하며 런타임 코드에 영향을 주지 않는다. 또한 유효한 자바스크립트 구문도 아니다.
- tsc 명령어를 사용해 타입스크립트 소스 코드를 자바스크립트 코드로 컴파일하면 해당 코드는 삭제된다.
- 변수에 타입 애너테이션으로 정의한 타입 외의 값을 할당하면 타입 오류가 발생한다.

### 2.3.1 불필요한 타입 애너테이션

- 즉시 유추할 수 있고, 변경되지 않을 예정인 값의 경우 굳이 타입 애너테이션을 사용할 필요가 없다.

## 2.4 타입 형태

- 타입스크립트는 할당된 값이 원래 타입과 일치하는지 확인하는 것뿐만 아니라, **해당 타입에서 사용 가능한 작업만을 허용하는 기능**도 제공한다.

### 2.4.1 모듈

- 자바스크립트의 경우, 비교적 최근까지 서로 다른 파일에 작성된 코드를 공유하는 방법에 관련된 사양을 제공하지 않았다.
- 그러다가 ECMA 스크립트 2015에 파일 간 가져오고 내보내는 (import & export) `ECMA스크립트 모듈(ESM)`이 추가되었다.

```ts
import { value } from "./values";
export const doubled = value * 2;
```

- 모듈 파일에 선언된 모든 것은 해당 파일에서 명시한 export 문에서 내보내지 않는 한, 모듈 파일에서만 사용할 수 있다.
- 한 모듈에서 다른 파일에 선언된 변수와 동일한 이름으로 선언된 변수는 다른 파일의 변수를 가져오지 않는 한 이름 충돌로 간주하지 않는다.
  > 모듈 : export 또는 import가 있는 파일
  > 스크립트 : 모듈이 아닌 모든 파일
- 한 모듈에서 다른 파일에 선언된 변수와 동일한 이름으로 선언된 변수는, 다른 파이르이 변수를 가져오지 않는 한 이름 충돌로 간주하지 않는다.
- 반면, 파일이 스크립트인 경우, 타입스크립트가 해당 파일을 전역 스코프로 간주하기 때문에 모든 스크립트가 파일의 내용에 접근할 수 있다.
- 따라서 스크립트 파일에 선언된 변수는, 다른 스크립트 파일에 선언된 변수와 동일한 이름을 가질 수 없다.
- 타입스클비트 파일에 Cannot redeclare... 라는 오류가 표시되면 파일에 아직 export 또는 import 문을 추가하지 않았기 때문일 수도 있다.(파일이 .ts일지라도!)
- ECMA 스크립트 사양에 따라 export 또는 import 문 없이 파일을 모듈로 만들어야 한다면, 파일의 아무 곳에나 `export {};` 를 추가해 강제로 모듈이 되도록 만든다.

```ts
// a.ts and b.ts
const shared = "Cher"; // Ok

export {};
```

# Chapter 3. 유니언과 리터럴

<h2>>🥹 상수를 제외한 모든 것은 변합니다.</h2>
- 유니언(union) : 값에 허용된 타입을 두 개 이상의 가능한 타입으로 확장하는 것.
- 내로잉(narrowing) : 값에 허용된 타입이 하나 이상의 가능한 타입이 되지 않도록 좁히는 것.

## 3.1 유니언 타입

```ts
let mathematician = Math.random() > 0.5 ? undefined : "Hyeyeon";
```

- 위에서 mathematician은 undefined 이거나 string이다.
- 이처럼 **이거 혹은 저거**와 같은 타입을 **유니언**이라고 한다.
- 유니언 타입 : 값이 정확히 어떤 타입인지 모르지만, 두 개 이상의 옵션 중 하나라는 걸 알고 있는 경우 코드를 처리하는 개념.
- 유니언 타입 나타내기 : 가능한 값 또는 구성 요소 사이에 | (수직선) 연산자를 사용해 유니언 타입 나타냄.

### 3.1.1 유니언 타입 선언

- 유니언 타입 사용 : 변수의 초깃값이 있더라도 변수에 대한 명시적 타입 애너테이션을 제공하는 것이 유요할 때 사용 (ex. thinker라는 변수의 초깃값은 null이지만. think는 잠재적으로 null 대신 string이 될 수도 있음.

### 3.1.2 유니언 속성

- 값이 유니언 타입일 때 : 유니언으로 사용한 모든 타입에 존재하는 멤버 속성에만 접근이 가능.
- 유니언 타입에 존재하지 않는 속성에 대한 접근 제한 -> (ex. to UpperCase는 string 속성에서만 접근 가능) 안전 조치에 해당함. 객체가 어떤 속성을 포함한 타입으로 확실하게 알려지지 않았기 때문임.

## 3.2 내로잉

- 내로잉이란? 값이 정의, 선언 혹은 이전에 유추된 것보다 더 **구체적인 타입** 임을 코드에서 유추하는 것.
- 타입스크립트의 값의 타입이 이전에 알려진 것보다 더 좁혀졌다는 걸 알게 되면, 값을 터 구체적으로 유추하게 된다.
- 이렇게 내로잉을 통해 타입을 유추할 수 있게 해 주는 논리적 검사를 **타입 가드** 라고 부른다.

### 3.2.1 값 할당을 통한 내로잉

```ts
let admiral: number | string;
admiral = "Hyeyeon Kim";
admiral.toUpperCase(); // ok: string
admiral.toFixed();
//
// Error: Property 'toFixed' does not exist on type 'string'.
```

- 값 할당을 통한 내로잉이란, 변수에 값을 직접 할당함으로서 타입을 할당된 값의 타입으로 좁히는 것이다.
- 위의 예시에서, `admiral`변수는 초기에 number | string 으로 선언했지만 "Hyeyeon Kim" 값이 할당된 후 string 타입이라는 걸 알게 된다.

### 3.2.2 조건 검사를 통한 내로잉

```ts
// scientists: number | string의 타입
let scientist = Math.random() > 0.5 ? "Hyeyeon kim" : 51;

if (scientist === "Hyeyeon Kim) {
    // scientist: string 타입
    scientist.toUpperCase(); // Ok
}

// scientist: number | string의 타입
scientist.toUpperCase();
//
// Error: Property 'toUpperCase' does not exist on type 'string | number'
```

- 타입스크립트에서는 변수가 알려진 값과 같은지 확인하는 **if 문**을 통해 변수의 값을 좁히는 방법을 사용한다.
- 타입스크립트는 if문 내에서 변수가 알려진 값과 동일한 타입인지 확인한다.

### 3.2.3 typeof 검사를 통한 내로잉

```ts
// scientists: number | string의 타입
let researcher = Math.random() > 0.5 ? "Hyeyeon kim" : 51;

if (typeof researcher === "Hyeyeon Kim) {
    // scientist: string 타입
    scientist.toUpperCase(); // Ok: string
}
```

- 직접 값을 확인해 타입을 좁힐 수도 있지만, typof 연산자를 사용할 수도 있다.
- 위 스니펫은 타입 내로잉에서 직원되는 삼항 연산자를 사용해 다시 작성할 수 있다.

```ts
typeof researcher === "string"
  ? researcher.toUpperCase() // Ok:string
  : researcher.toFixed(); // Ok: number
```

## 3.3 리터럴 타입

- **리터럴 타입**이란? -> 조금 더 구체적인 버전의 원시 타입. 원시 타입 값 중 어떤 것이 아닌, `특정 원싯값`으로 알려진 타입이 리터럴 타입.

```ts
const philosopher = "Hypatia";
```

- 위의 philosopher 은 string 타입이라고 볼 수 있고, 실제로도 string 타입이다.
- 그러나 엄밀히 말하면, philosopher은 "Hypatia"라는 특별한 값이다.

> 원시 타입 string하고는 어떤 차이가 있을까?

- **원시 타입 string**은 존재할 수 있는 **모든 가능한 문자열의 집합**을 나타낸다. 하지만 리터럴 타입 `Hypatia`는 하나의 문자열만 나타낸다.
- 변수를 const로 선언하고 직접 리터럴 값을 할당하면 타입스크립트는 해당 변수를 할당된 리터럴 값으로 유추한다. 따라서 IDE에서 초기 리터럴 값이 할당된 const 변수 위에 마우스를 가져가면 일반적인 원시타입 대신 리터럴이 표시된다. (let으로 선언할 경우 string이 표시됨.)

> 결국 원시 타입이란, 해당 타입의 가능한 모든 리터럴 값의 집합이라고 할 수 있음. 👍

- 유니언 타입 애너테이션에서는 리터럴과 원시 타입을 섞어서 사용할 수 있다.

```ts
let lifespan: number | "ongoing" | "uncertain";

lifespan = 89; // ok
lifespan = "ongoing"; // ok

lifespan = true;
// Error: Type 'true' is not assignable to type 'number | "ongoing" | "uncertain"'
```

### 3.3.1 리터럴 할당 가능성

- 0과 1처럼 동일한 원시 타입일지라도, 서로 다른 리터럴 타입은 서로에게 할당할 수 없다.

## 3.4 엄격한 null 검사

### 3.4.1 십억 달러의 실수

- `십억 달러의 실수` : 다른 타입이 필요함에도 불구하고 `null` 값을 사용하도록 허용하는 타입 시스템을 지칭할 때 쓰는 용어.
- null 참조의 발명으로 인해 발생한 취약성 및 시스템 충돌만 해도 십억 달러정도 된다는 뜻에서 나온 용어다.
- 최신 프로그래밍 언어의 큰 변화 -> 잠재적으로 정의되지 않는 undefined 값으로 작업할 떄 더욱 두드러짐.
- null과 undefined 값으로 인한 오류를 막아주기만해도 프로그램 안정화에 큰 도움이 됨.
- 타입스크립트는 엄격한 null 검사를 시행해 충돌을 방지하고 실수를 제거할 수 있음.

### 3.4.2 참 검사를 통한 내로잉

- 타입스크립트는 잠재적 값 중 **truthy**로 확인된 일부에 한해서만 변수의 타입을 좁힐 수 있다.

```ts
// 여기서 geneticist는 string | undefined다.
if (geneticist) {
  geneticist.toUpperCase(); // Ok: string
}

geneticist.toUpperCase();
// Error: Object is possiblt 'undefined'.
```

- if 문을 통해 변수의 타입을 좁힐 수 있는 건 truthy 값인 string밖에 없다.

```ts
let biologist = Math.random() > 0.5 && "Hyeyeon";

if (biologist) {
  biologist; // string
} else {
  biologist; //string | false
}
```

- 위 코드에서 if 문 안에 있는 biologist의 타입은 string, else 블록문 안에 있는 bilologist의 타입은 false | string 이다.

1.  Math.random() > 0.5가 참일 경우 : biologist 변수에는 문자열 "Hyeyeon"이 할당된다. 이때, biologist 변수는 문자열 타입을 가지며, 조건식은 참(true)으로 평가된다. 따라서 if 블록이 실행되고, biologist 변수는 그대로 문자열 타입을 유지한다.
2.  Math.random() > 0.5가 거짓일 경우 : biologist 변수에는 falsy한 값인 false가 할당된다. 이때, biologist 변수는 불리언(Boolean) 타입이며, 조건식은 거짓(false)으로 평가된다. 따라서 else 블록이 실행되고, biologist 변수는 그대로 불리언(Boolean) 타입을 유지한다.
3.  biologist 변수가 초기화되지 않은 경우 : biologist 변수의 값은 undefined가 됩니다. 이때, biologist 변수는 undefined 타입을 가지며, 조건식은 거짓(false)으로 평가된다. 따라서 else 블록이 실행되고, biologist 변수는 그대로 undefined 타입을 유지한다.

### 3.4.3 초깃값이 없는 변수

- 자바스크립트에서 초깃값이 없는 변수 -> 기본적으로 **undefined**가 된다.
- 만약 undefined를 포함하지 않는 타입으로 변수를 선언한 다음, 값을 할당하기 전 사용하려고 시도하면 어떻게 될까?
- 값이 할당되기 전 해당 변수를 사용하려고 시도하면 오류 메시지가 나타난다.

```ts
let mathematician = string;

mathmatician?.length;
// Error: Variable 'mathmatician' is used before being assigned.

mathematician = "Mark Goldberg";
mathematician.length; // Ok
```

- 만약 변수 타입에 undefined가 포함되어 있다면 오류는 보고되지 않는다. undefined의 경우 유효한 타입이기 때문에 사용 전에 정의할 필요가 없음을 타입스크립트에 나타낸다.

## 3.5 타입 별칭 (Type Alias)

- `타입 별칭` : 재사용하는 타입에 더 쉬운 이름을 할당하는 것.
- **type 새로운 이름 = 타입** 형태를 가진다.
- 타입 별칭은 파스칼 케이스(PascalCase)로 이름을 지정한다.
- 타입 별칭은 타입 시스템의 복사해서 붙여넣기처럼 작동한다. 상당히 길었던 유니언 타입도 타입 별칭을 이용하면 축약할 수 있다. 가독성도 훨씬 좋아진다.

### 3.5.1 타입 별칭은 자바스크립트가 아닙니다

- 타입 별칭은 자바스크립트로 컴파일되지 않고 순전히 타입스크립트 시스템에만 존재한다.
- 따라서 타입 별칭은 런타임 코드에서 참조할 수 없다. 런타임에 존재하지 않는 항목에 접근하려고 하면 타입 오류로 알려준다.

```ts
type SomeType = string | undefined;

console.log(SomeType);
// Error: 'SomeType' only refers to a type, but is being used as a value here.
```

### 3.5.2 타입 별칭 결합

- 타입 별칭은 다른 타입 별칭을 참조할 수 있다.
