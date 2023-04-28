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

# Chapter 4. 객체

- 원시 타입은 사실 자바스크립트가 사용하는 복잡한 객체의 겉만 훑을 뿐이다.

## 4.1 객체 타입

- {} 구문을 사용해서 객체 리터럴을 생성했을 때, 타입스크립트는 해당 속성을 기반으로 새로운 객체 타입 또는 타입 형태를 고려하게 된다.
- 생성된 객체 타입은 객체의 값과 `동일한 속성명`과 `동일한 원시타입`을 갖는다.
- 값의 속성에 접근하기 위해서는 `value.멤버` 또는 `value['멤버']` 구문을 사용해야 한다.
- null과 undefined를 제외한 모든 값은, 그 값에 대한 실제 타입의 멤버 집합을 가진다. 따라서 TS는 모든 값의 타입을 확인하기 위해 객체 타입을 이해해야 한다.
  > 이 말은, JS에서 null과 undefined를 제외한 모든 값들은 자신이 가진 실제 데이터 타입에 따라 사용 가능한 멤버 함수와 속성들이 존재한다는 의미다. TS에서는 null과 undefined를 제외한 모든 값들이 객체 타입으로 간주되어, 다양한 멤버 함수와 속성을 가지게 된다. 예를 들면, 문자열(string) 데이터 타입의 값은 문자열에 대해서만 적용 가능한 다양한 내장 멤버 함수와 속성을 가지고 있다. 'toUpperCase()'와 같은 함수는 문자열에만 적용 가능한 함수다. TS에서는 값에 대해 다양한 멤버 함수와 속성을 제공하고, 이를 이용해 해당 값이 특정 타입임을 확인할 수 있다.

### 4.1.1 객체 타입 선언

- 객체의 타입을 **명시적으로** 선언하고 싶을 땐 어떻게 해야 할까? 타입이 선언된 객체와는 별도로 객체의 형태를 설명하는 방법이 필요하다.
- 객체 타입은 필드 값 대신 타입을 사용해 설명한다.

### 4.1.2 별칭 객체 타입

- `{born: number, name: string}`같은 객체 타입을 작성하는 것 대신, 객체 타입에 타입 별칭을 할당해 사용하는 방법이 일반적이다.
- 이는 타입스크립트의 오류 메시지를 좀더 직접적으로 읽기 쉽게 만드는 추가 이점이 있다.

## 4.2 구조적 타이핑

- 타입스크립트의 타입 시스템은 `구조적으로 타입화(structurally typed)`되어 있다.
  > 구조적 타이핑이란 ? TS에서 값의 타입이 해당 값이 가진 `구조(구조체)`에 의해 결정된다는 것을 의미함.
- 이름이 다른 두 개의 인터페이스가 있을 때, 해당 인터페이스들이 가진 구조가 동일하다면 같은 타입으로 간주함.
- TS에서는 값의 타입이 이름이나 명시적으로 선언된 타입보다는, 해당 값이 가진 **구조**에 의해 결정됨.

```ts
interface Person {
  name: string;
  age: number;
}

interface Employee {
  name: string;
  age: number;
  employeeId: number;
}
```

- 위 두 개의 인터페이스는, 동일한 구조를 가지고 있으므로 같은 타입으로 취급이 된다.
- 이러한 특징 때문에, 매개변수나 변수가 특정 타입으로 선언된다면 타입스크립트에 어떤 객체를 사용하든 해당 속성이 있다고 말해야 한다.

> 덕 타이핑(duck typying) : 구조적 타이밍과 반대되는 개념. 덕 타이핑은 '오리처럼 보이고 오리처럼 꽥꽥거리면, 오리일 것이다`라는 문구에서 유래했다.

- 타입스크립트에서 구조적 타이밍은 **정적 시스템이 타입을 검사하는 경우**다.
- 덕 타이핑은 런타임에서 사용될 때까지 객체 타입을 검사하지 않는다.
- 정리 : 자바스크립트는 **덕 타입**인 반면, 타입스크립트는 **구조적으로 타입화**된다.

### 4.2.1 사용 검사

- 객체 타입에 값을 제공할 때, 타입스크립트는 특정 값을 해당 객체에 할당할 수 있는지를 확인한다.
- 이때 할당하는 값에는, 객체 타입의 필수 속성이 있어야 한다.
- 객체 타입에 필요한 멤버가 객체에 없다면, TS는 오류를 발생시킨다.
- 둘 사이에 일치하지 않는 타입도 허용되지 않는다. 객체 타입은 필수 속성 이름과, 속성이 예상되는 타입을 모두 지정하기 때문이다.

### 4.2.2 초과 속성 검사

- 변수가 객체 타입으로 선언되고, 초깃값에 객체 타입에서 **정의된 것보다 많은 필드**가 있다면 타입스크립트에서 타입 오류가 발생한다.
- 하지만, **기존 객체 리터럴**을 사용하여 객체를 생성하는 경우에는 초과 속성 검사가 수행되지 않는다.

```ts
const person = {
  name: "John",
  age: 30,
  gender: "male",
};
```

- 위와 같이 person 객체가 이미 생성되어 있고

```ts
const john: Person = person;
```

- 위 객체를 Person 타입으로 선언된 변수에 할당할 때는, 초과 속성 검사가 수행되지 않는다.
- 이런 방식으로 기존에 생성된 객체를 사용하여 타입 검사를 우회할 수 있다. 그러나, 이럴 때는 오류를 미리 방지할 수 없기 때문에 주의가 필요하다.

### 4.2.3 중첩된 객체 타입

- 타입스크립트의 객체 타입도, 타입 시스템에서 중첩된 객체 타입을 나타낼 수 있어야 한다.
- 중첩된 객체 타입 예시

```ts
interface Address {
  street: string;
  city: string;
}

interface Person {
  name: string;
  age: number;
  address: Address;
}

function printPerson(person: Person) {
  console.log(`Name: ${person.name}, Age: ${person.age}`);
  console.log(`Address: ${person.address.street}, ${person.address.city}`);
}

const john: Person = {
  name: "John",
  age: 30,
  address: {
    street: "123 Main St",
    city: "Anytown",
  },
};

printPerson(john);
```

- 위 코드에서, Person 객체 타입에서는 Address 객체 타입을 포함하고 있으며, printPerson 함수에서는 Person 타입을 인자로 받는다. john 변수는 Person 타입의 객체를 할당받으며, address 속성에서는 중첩된 Address 객체를 사용한다.
- 이제 printPerson 함수를 호출할 때 john 변수를 전달하면, TypeScript는 john 변수가 Person 타입의 객체임을 인식하고, printPerson 함수에 전달될 수 있도록 한다. 함수 내부에서는 중첩된 객체 타입인 Address의 속성도 참조하여 출력한다.

### 4.2.4 선택적 속성

- 타입의 속성 애너테이션에서 : 앞에 ?를 추가하면, 선택적 속성임을 나타낼 수 있다.

```ts
interface User {
  id: number;
  name: string;
  email?: string;
}

function getUserInfo(user: User) {
  console.log(`User ID: ${user.id}, Name: ${user.name}`);
  if (user.email) {
    console.log(`Email: ${user.email}`);
  }
}

const user1: User = {
  id: 1,
  name: "John",
};

const user2: User = {
  id: 2,
  name: "Jane",
  email: "jane@example.com",
};

getUserInfo(user1); // User ID: 1, Name: John
getUserInfo(user2); // User ID: 2, Name: Jane, Email: jane@example.com
```

> 선택적 속성과 undefined의 차이점 : ?를 사용해 선택적으로 선언된 속성은 존재하지 않아도 된다. 하지만 필수로 선언된 속성과 | undefined는 그 값이 undefined 일지라도 반드시 존재해야 한다.

## 4.3 객체 타입 유니언

### 4.3.1 유추된 객체 타입 유니언 (Type Inference)

- TypeScript에서는 변수에 초기값이 할당될 경우, 해당 값을 바탕으로 타입을 유추하게 된다. 이때, 초기값이 여러 객체 타입 중 하나가 될 수 있는 경우, TypeScript는 해당 타입을 객체 타입 유니언(Object Type Union)으로 유추한다.

```ts
let myVariable = { name: "John", age: 30 };
```

- 위 코드에서 `myVariable` 변수에는 객체 리터럴이 할당되어 있다. 이 객체 리터럴은 name과 age 속성을 가지고 있으며, 이 속성들은 각각 string과 number 타입이다. 따라서 TypeScript는 myVariable 변수의 타입을 { name: string, age: number }으로 유추한다.
- 그러나 다음과 같이 코드가 바뀐다면 어떻게 될까?

```ts
let myVariable = { name: "John", age: 30 };
myVariable = { name: "Jane" };
```

- 위 코드에서는 myVariable 변수가 초기값으로 객체 리터럴을 할당받았지만, 나중에 다시 객체 리터럴을 할당받을 수도 있다.
- 이때 TypeScript는 myVariable 변수의 타입을 객체 타입 유니언으로 유추한다.
- 즉, myVariable 변수는 { name: string, age: number } 타입의 객체나 { name: string } 타입의 객체 중 하나가 될 수 있다는 것이다.
- `객체 타입 유니언`은 TypeScript의 강력한 기능 중 하나이며, 여러 객체 타입을 통합해서 사용할 수 있도록 도와준다.

### 4.3.2 명시된 객체 타입 유니언

- 객체 타입의 조합을 명시하면, 객체 타입을 더 명확히 정의할 수 있다.
- 명시적인 객체 유니언 타입(Object Type Union)은 여러 객체 타입을 합쳐서 하나의 타입으로 만들 때 사용된다. 객체 유니언 타입은 | 기호를 사용하여 표현된다.

```js
type Person = { name: string, age: number };
type Employee = { name: string, department: string };

let myVar: Person | Employee;
```

### 4.3.3 객체 타입 내로잉

- 원시 타입 유니언처럼, 객체 타입 유니언 역시 특정 값을 사용하기 위해서는 타입을 좁혀서 사용할 필요가 있다.

```ts
type User = {
  name: string;
  age: number;
};

type Admin = {
  name: string;
  role: string;
};

type Person = User | Admin; // User와 Admin 타입으로 구성된 유니언 타입을 만든다.

let person: Person = {
  name: "John",
  age: 30,
};
// Person 타입의 변수를 선언하고 초깃값을 할당한다. 이때, person 변수 타입은 Person 유니언 타입으로 추론된다. 이 변수에는 User 또는 Admin 객체가 들어갈 수 있다.

console.log(person.role); // 오류: Property 'role' does not exist on type 'Person'.

if ("role" in person) {
  console.log(person.role); // OK: person이 Admin 타입일 때만 실행됩니다.
}
// Role 속성을 사용하기 위해 Person 타입을 Admin 타입으로 좁혀야 한다.
```

- 객체 유니언 타입 내로잉이란, 특정 속성이 존재하지 않을 수도 있기 때문에 해당 속성을 사용하기 전 타입을 좁혀주는 것을 말한다.
- 참고로 타입스크립트는 if(person.role) 과 같은 방식으로 참 여부를 확인하는 것을 허용하지 않는다. 존재하지 않는 객체의 속성에 접근하려고 시도하면 타입 오류로 간주된다.

### 4.3.4 판별된 유니언 (discriiminated union)

- 유니언 타입에 속한 각 타입의 **구분자 역할을 하는 속성**을 추가하여 해당 속성의 값에 따라 타입을 판별하는 것을 말한다.
- 타입 가드를 적용하여 더욱 정확한 타입 추론이 가능하다.

```ts
type Shape = { kind: "circle", radius: number } | { kind: "square", sideLength: number };

function getArea(shape: Shape): number {
  switch(shape.kind) {
    case "circle":
      return Math.PI * shape.radius ** 2;
    case "square":
      return shape.sideLength ** 2;
    default:
      throw new Error("Invalid shape");
```

- 위 함수에서는 kind 속성을 판별자로 사용하여 입력받은 Shape 타입의 객체가 어떤 도형인지 판별하고 있다.
- 따라서 타입 검사기는 Shape 타입에 대한 정확한 **타입 추론**을 할 수 있게 되고, 잘못된 속성에 접근할 가능성이 줄어들게 된다.
- 여기서 객체의 타입을 가리키는 속성이 바로 판별값이다. 타입스크립트는 판별 속성을 사용해 타입 내로잉을 수행한다.

## 4.4 교차 타입

- 타입스크립트에서는 & 교차 타입을 이용해 여러 타입을 동시에 나타낼 수 있다.
- 타입스크립트에서 `&`연산자는, 두 개 이상의 객체 타입을 교차시켜 하나의 타입으로 만드는 교차 타입을 만들 때 사용된다.
- 일반족으로 여러 객체 타입을 별칭 객체 타입으로 결합해 새로운 타입을 생성한다.
- 교차 타입은 유니언 타입과 결합이 가능하다.

```ts
type Person = {
  name: string;
  age: number;
};

type Employee = {
  companyId: number;
  role: string;
};

type PersonEmployee = Person & Employee;

const personEmployee: PersonEmployee = {
  name: "John",
  age: 30,
  companyId: 123,
  role: "Manager",
};
```

- 교차 타입은 더 복잡한 타입을 만들 때 유용하게 사용된다. 예를 들어, 위 예시에서 Person과 Employee 타입의 각각 다른 하위 타입들을 갖는 객체를 만들 수도 있다.

#### 교차 타입과 타입 확장(extends)의 차이점은 무엇일까?

##### 공통점

타입 관의 관계를 표현하는 방법이다.

##### 차이점

1. 교차 타입의 경우, 두 개 이상의 타입이 갖는 속성과 메서드를 모두 가지는 `새로운 타입`을 생성한다. `and`연산자와 유사하다.
2. 타입 확장은, 이미 존재하는 타입에 새로운 속성이나 메서드를 추가하는 데 사용된다. `extends` 키워드와 유사하다.

- 교차 타입은 두 개 이상의 타입이 필요한 경우에, 타입 확장은 이미 존재하는 타입에 새 속성이나 메서드를 추가할 때 사용된다.

### 4.4.1 교차 타입의 위험성

- 교차 타입을 사용할 때는 가능한 한 코드를 간결하게 유지해야 한다.

#### 긴 오류

- 복잡한 교차 타입을 만들게 되면, 할당 가능성 오류 메시지가 읽기 더 어려워진다.

```ts
type Person = { name: string; age: number };
type Employee = { company: string; salary: number };
type Student = { school: string; grade: number };
type Teacher = { school: string; salary: number };

type EmployeeAndStudentAndTeacher = Employee &
  Student &
  Teacher & { name: string };
```

- 위와 같은 예시가 있을 때

```ts
// Error : Type '{ name: string; company: string; salary: number; school: string; grade: number; }' is not assignable to type 'Employee & Student & Teacher & { name: string; }'.
// Type '{ name: string; company: string; salary: number; school: string; grade: number; }' is not assignable to type 'Employee'.
// Types of property 'salary' are incompatible.
// Type 'number' is not assignable to type 'never'.
```

#### never

- 교차 타입을 사용할 때 두 개의 원시 타입을 함께 시도하면, `never` 키워드로 표시되는 never 타입이 된다.
- never 키워드, never 타입은 프로그래밍 언어에서 bottom 또는 empty 타입을 뜻한다.
- bottom 타입은 값을 가질 수 없고 참조할 수 없는 타입이다. bottom 타입에는 그 어떠한 타입도 제공할 수 없다.

# Chapter 5. 함수

## 5.1 함수 매개변수

- 변수와 마찬가지로 TS를 사용하면 타입 애너테이션으로 `함수 매개변수`의 타입을 선언할 수 있다.

### 5.1.1 필수 매개변수

- 자바스크립트에서는 인수의 수와 상관없이 함수를 호출할 수 있지만, 타입스크립테서는 함수에 선언된 모든 매개변수가 필수라고 가정한다.
- 함수가 잘못된 수의 인수로 호출되면, 타입스크립트는 바로 타입 오류를 띄운다.
- 함수에 `필수 매개변서`를 제공하도록 강제하면, 예상되는 모든 인숫값을 함수 내에 존재하도록 만들어 타입 안정성을 강화하는 데 도움이 된다.
  > **매개변수** : 함수를 정의할 때 함수가 받을 값을 나타내는 **변수**.
  > **인수** : 함수를 호출할 때 매개변수에 제공되는 **값**

### 5.1.2 선택적 매개변수

- 자바스크립트에서는 함수 매개변수가 제공되지 않으면, 함수 내부의 인숫값은 `undefined`로 기본값이 설정된다.
- 생각해보면 때로는 함수 매개변수를 제공할 필요가 없을 때도 있고, undefined 값을 의도적으로 사용해야 할 때도 있다.
- 우리는 이처럼 의도적으로 선택적 매개변수에 인수를 제공하지 못하는 경우, TS에게 타입 오류를 보고하지 않았으면 할 때가 있다.
- 이 때 사용하는 게 바로 `?` 를 사용해서 **매개변수가 선택적**이라고 표시하는 것이다.
- 선택적 매개변수에는 항상 ` | undefiend`가 유니언 타입으로 추가되어 있다.
- 선택적 매개변수는 항상 암묵적으로 `undefined`가 될 수 있다.
- 함수에서 사용되는 모든 선택적 매개변수는 **마지막 매개변수**여야 한다. (만약 필수 매개변수 전에 선택적 매개변수를 위치시키면 타입스크립트 구문 오류가 발생한다.)

### 5.1.3 기본 매개변수

- 매개변수에 기본값이 있고 타입 애너테이션이 없는 경우, 타입스크립트는 해당 기본값을 기반으로 매개변수 타입을 유추한다.

```ts
function greet(name = "world") {
  console.log(`Hello, ${name}!`);
}

greet(); // "Hello, world!" 출력
greet("Alice"); // "Hello, Alice!" 출력
```

- 위의 greet 함수는 name 매개변수에 기본값 "world"을 지정하고 있다. 이 경우 name 매개변수의 타입은 문자열(string)으로 유추된다.

### 5.1.4 나머지 매개변수

> `...` 스프레드 연산자는 함수 선언의 마지막 매개변수에 위치하고, 해당 매개변수에서 시작해 함수에 전달된 나머지 인수가 모두 단일 배열에 저장되어야 함을 나타낸다.

#### 이 알쏭달쏭한 건 도대체 무슨 말일까?? GPT와 함께 알아보자.

- ... 스프레드 연산자는 배열이나 객체 등의 요소를 펼쳐서 전개할 수 있는 문법입니다.
- 이 연산자를 함수 호출 시에 사용하면 `함수의 매개변수`로 `배열` 형태로 값을 전달할 수 있습니다.

```ts
function sumNumbers(x, y, z) {
  return x + y + z;
}
```

- 위와 같은 함수가 있다고 가정할 때, 이 함수는 3개의 인자를 받아서 합산한 값을 반환합니다.
- 하지만 만약 **인자를 배열로 전달하고 싶다면** 어떻게 해야 할까요? 이때 ... 스프레드 연산자를 사용하면 됩니다.

```ts
const numbers = [1, 2, 3];
const result = sumNumbers(...numbers);
console.log(result); // 6
```

- 위 코드에서 ...numbers는 [1, 2, 3]을 펼쳐서 sumNumbers 함수에 전달하게 됩니다. 이렇게 하면 sumNumbers 함수는 x=1, y=2, z=3으로 인자를 받아들여서 결과값 6을 반환하게 됩니다. -함수의 매개변수에서 ... 스프레드 연산자를 사용하면 함수에 전달된 인수들 중에서 마지막 매개변수 이후의 모든 인수들이 **단일 배열로 저장**되게 됩니다.
- 이렇게 저장된 배열은 **함수 내에서 일반적인 배열과 마찬가지로 취급될 수 있습니다.**

```ts
function myFunc(a, b, ...rest) {
  console.log(rest);
}
```

- 이 함수에서 ...rest는 마지막 매개변수에 위치하고 있으며, 함수에 전달된 인수 중에서 a와 b를 제외한 나머지 인수들이 rest 배열에 저장되게 됩니다. 따라서 함수를 호출할 때 아래와 같이 인수들을 전달할 수 있습니다.

```ts
myFunc(1, 2, 3, 4, 5);
// 출력: [3, 4, 5]
```

- 이렇게 ... 스프레드 연산자를 사용하면 함수 호출 시에 배열 형태의 인수를 전달할 수 있습니다.

#### 다시 돌아와서, 이러한 나머지 매개변수의 타입을 어떻게 정의할 것인가?

- 나머지 매개변수의 타입은 일반 매개변수와 유사하게 선언할 수 있다.
- 단, 인수 배열을 나타내기 위해 끝에 [] 구문이 추가된다.

```ts
function concatenateStrings(separator: string, ...strings: string[]): string {
  return strings.join(separator);
}
```
