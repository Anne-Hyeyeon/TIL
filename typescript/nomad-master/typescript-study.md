# 노마드코더 마스터클래스 타입스크립트 공부기록

## 0. Introduction
### Typescript란? 
- JS를 기반으로 한 프로그래밍 언어 : TS는 JS 복붙인데, 거기에다가 새로운 기능만 살짝 추가한 것.
- `strongly-typed` 언어 : 실행하기 전에 **data type**을 검사한다.
- 자바스크립트와의 비교
```js
const plus = (a,b) => a+b 
```
위 함수가 있을 때,   
plus(2,2)는 4라는 결과값을 주지만, js는 a와 b가 어떤 타입이어야 하는지 전혀 모른다. 
js는 그냥 a+b결과만 내보내줄 뿐이다.   
그렇다면 plus (2,"hi")를 해볼까? '2hi'가 나와버린다.   
 
- js에게 a,b가 언제나 number라는 사실을 말해주고 싶다.   
**만약 a,b가 number 타입이 아닐 경우, 나한테 알려주게 하려면?**   

- 코드를 publish하기 전에 js가 도와줄 수 있는 방법이 있을까?   
**없다.** js는 도와주지 않을 것이다. JS는 stongly-typed된 언어가 아니기 때문이다.

- typescript는 프로그램이 작동하기 전에,  **'이 데이터타입은 뭐야?'** 라고 한번 체크해 준다.    
- (js랑 똑같지만, '~~가 틀렸어' 라고 말하는 것 빼고는 다 똑같다.)
- TS 세계에서는, const plus = (a,b) => a + b;에서 a와 b가 어떤 데이터타입을 가지는지 모른다며 잔소리를 막 해댄다.    반면 js는 마이웨이임. **안알랴줌**

```js
const plus = (a:number, b:number) => a + b;
```
- 주의할 점 : 브라우저는 TS를 알아듣지 못한다. TS는 **complie**해서 보통의 JS로 만들어주어야 한다.
