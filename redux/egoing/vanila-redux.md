# 생활코딩 Redux (JS기반) 강의 정리
## 1. 수업 소개
- 복잡성 <-> 예측가능성
- 코드의 복잡성은 소프트웨어 개발에 있어서 치명적이다. (심지어, 한 회사를 망하게 할 수도 있다!)
- 리덕스 : app의 복잡성을 획기적으로 낮춰주는, 우리의 app을 예측 가능하게 해 주는 환상적인 라이브러리다.
- Single Source of Truth : 리덕스가 가진 최대의 장점
### 개념 1 : 하나의 객체 안에 app에 필요한 모든 data를 욱여넣음으로서 app의 복잡성을 낮춘다.   
#### 한 곳의 데이터를 중앙집중적으로 관리하면, 흩어져 있는 것보다 관리하는 게 훨씬 쉬워진다.
### 개념 2 : 데이터가 가진 공간을 다른 공간이랑 차단시킨다. 왜? 중요하기 때문에. 
#### 그러면 어떻게 데이터를 꺼낼 것인가? -> 데이터 앞을 지키고 있는 `문지기`를 통해서.
- 사용자가 직접 데이터를 바꾸지도 못하고, 가져갈 때도 getState를 통한 사람(함수)을 통해서만 가져갈 수 있다.
- 외부에서 직접 데이터를 제어할 수 없음 -> 의도하지 않게 state 값이 바뀌는 문제를 차단함으로서 `예측 가능한`앱이 될 수 있음.
- 이러한 리덕스의 특징을 이용하면, 모듈 리로딩 (우리가 코드를 작성하면 자동으로 app에 반영됨)이 가능해짐.
- app은 refresh가 되는데 data가 그대로 남아있기 때문에, 우리가 **다시 입력 작업을 할 피료가 없도록** 우리 개발 환경을 세팅할 수 있다.
- -> 후진이 없는, 전진만 있는 개발.

## 2.1 리덕스 여행의 지도 :  소개
<img src="https://github.com/Anne-Hyeyeon/TIL/blob/main/redux/egoing/redux_pic.png?raw=true" />

## 2.2 리덕스 여행의 지도 : state와 render의 관계
- 리덕스의 핵심 : store (은행), 정보가 저장되는 것
- 정보가 저장되는 것 : state, 직접 저장 불가능하고 누군가를 통해 접근해야 함.
- reducer 함수 var store = Redux.createStore(reducer);
- reducer는 리덕스에 인자로 넣어주는 함수이다. 이걸 작성하는 게 리덕스를 만드는 일의 대부분이라고 할 수 있을 정도로 중요함.
- render : 리덕스와는 상관 없는, 내 코드 
### state 앞단 직원들 : dispatch, subscribe, getState 일반인은 접근 못하는 데이터 관련해서 각각 역할 수행함.
#### getState : state값을 가져와 render에게 줌. 
- render는 state값 참조해서 ui를 만드는 것.
- state가 바뀔 때마다 render가 자동으로 되면 얼마나 좋을까? ㅠㅠ 알아서 state가 바뀔 때마다 UI가 갱신되었으면 좋겠다!
#### subscribe : (구독)함수.
- subscribe에 render함수를 등록하면, state가 바뀔 때마다 UI가 새롭게 갱신된다.


## 2.3 리덕스 여행의 지도 : action과 reducer
- onSubmit 이벤트를 살펴보자. store.dispatch 에 객체를 전달해준다. (type은 'create').
- 이때 전하는 객체가 action
- 이 action은 dispatch한테 전달된다.
### dispatch의 역할
#### 1) reducer 호출해서 state 값 바꿈
#### 2) subscribe 호출해서 render함수 호출 (화면 갱신)
- dispatch가 reducer를 호출할 때 두 개의 값을 전달한다. 1) `현재의 state값` 2) `action 데이터`
- functiond reducer(state, action)...
- reducer안에서 return해주는 객체는 새로운 state가 된다.
- `reducer`는 초기 state를 action 참조를 받아 새로운 state로 바꿔 return하는 가공자이다.
- state 변경 후, dispatch가 subscribe에 등록된 구독자들을 모두 호출, render가 일어나며 state값이 바뀐다.

## 3. Redux가 좋은 가장 중요한 이유
<img src="https://github.com/Anne-Hyeyeon/TIL/blob/main/redux/egoing/redux_why.png?raw=true" alt="redux" />

- Redux 없이 네 가지 색깔의 창고 안에 네 가지 속성을 바꿔야 한다고 생각하면, 부품이 몇 개나 들까? 각 기능마다 하나씩 부품을 소모해야한다면...
- 하지만, 리덕스가 있다면 어떻게 될까?
- 스토어에게 상태 바뀌었음을 알려주면, 알아서 다른 곳에다가도 '상태가 바뀌었으니 얼른 바꾸세요'라고 해 준다. 각자 알아서 업데이트 된다.
- 각각의 부품은 몇개의 로직이 필요한 게 될까? 1) 상태 바뀌었을 때 알려주는 로직 2) 상태가 변경되었을 때 자신을 변화시키는 로직 색깔당 총 두 개 필요함. 따라서 총 8개 
- 크롬 개발자 도구 리덕스 ! 각각의 요소 누르면 걔네한테 그동안 어떤 변화가 있었는지 확인할 수 있다.
- js 디버거는 현재의 상태를 보고, redux 를 이용하면 각각의 변화가 생겼을 때, 어떤 상태인지를 볼 수 있다.  (시간 여행)
- 파일로 받은 후 임포트해주면 설정을 그대로~쓸 수 있다!

## 4. Redux가 없다면
### 얼마나 불편한지 함 보이소~
```html
<html>
    <body>
        <style>
                    .container {
            border: 5px solid black;
            padding: 1rem;
            margin-bottom:1rem;
        }
        body{
            margin:1rem;
        }
        </style>
        <h1>Without redux</h1>
        <div id="red"></div>
        <div id="green"></div>
        <div id="blue"></div>
        
        <script>
function red(){
    document.querySelector('#red').innerHTML = `
        <div class="container" id="component_red" style="background-color:yellow">
            <h1>red</h1>
            <input type="button" value="fire" onclick="
            document.querySelector('#component_red').style.backgroundColor = 'red';
            document.querySelector('#component_green').style.backgroundColor = 'red';
            document.querySelector('#component_blue').style.backgroundColor = 'green';
            ">
        </div>
    `;
}
red();
function green(){
    document.querySelector('#green').innerHTML = `
        <div class="container" id="component_green" style="background-color:yellow">
            <h1>green</h1>
            <input type="button" value="fire" onclick="
            document.querySelector('#component_red').style.backgroundColor = 'green';
            document.querySelector('#component_green').style.backgroundColor = 'green';
            document.querySelector('#component_blue').style.backgroundColor = 'green';
            ">
        </div>
    `;
}
green();
function blue(){
    document.querySelector('#blue').innerHTML = `
        <div class="container" id="component_blue" style="background-color:yellow">
            <h1>blue</h1>
            <input type="button" value="fire" onclick="
            document.querySelector('#component_red').style.backgroundColor = 'blue';
            document.querySelector('#component_green').style.backgroundColor = 'blue';
            document.querySelector('#component_blue').style.backgroundColor = 'blue';
            ">
        </div>
    `;
}
blue();
        </script>
    </body>
</html>
```

## 5.1 Redux의 적용 : store 생성
### 리덕스 설치하기
- 바닐라 자바스크립트 환경의 경우, 검색엔진에서 cdn redux 검색 후 붙여넣기
- https://cdnjs.cloudflare.com/ajax/libs/redux/4.2.0/redux.js (CDN)
- 리덕스를 이용한다? 스토어를 만든 후, 스토어의 상태를 바꾸는 게 핵심이다.
- 스토얼르 만들면 state가 생기고, reducer라는 함수를 만들어 store에 주입해주는 게 첫 번째 단계다.
- reducer는 state값을 변형시킨 후 다시 return해주는 함수
- store는 은행, dispatch는 창구 직원, reducer는 은행 장부
``` js
var store = Redux.createStore(reducer);
```
- 스토어가 전역 변수에 저장됨
- state에 있는 값을 가져오고 싶다면? getState 사용
- 이렇게 생각해보면 어떨까? reducer는 요리사, dispatch()는 종업원, action은 메뉴, component는 고객 :)
