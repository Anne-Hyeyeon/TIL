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

- 유니언 타입 사용 : 변수의 초깃값이 있떠라도 변수에 대한 명시적 타입 애너테이션을 제공하는 것이 유요할 때 사용 (ex. thinker라는 변수의 초깃값은 null이지만. think는 잠재적으로 null 대신 string이 될 수도 있음.

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

- 최신 프로그래밍 언어의 큰 변화 -> 잠재적으로 정의되지 않는 undefined 값으로 작업할 떄 더욱 두드러짐.
