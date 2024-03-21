# 2023-04-04

## 게시판 필터 유지 기능에 대해서
### 문제 : 게시글을 한번 클릭하고 뒤로 가기를 누를 때마다 필터와 검색어가 초기화 됨. 
- 작년 12월에 개발한 게시판. 내가 구현한 메인 파트에 문제가 생겼다. 게시글을 한번 누르고 다시 돌아올 때마다 필터가 초기화 되어버린다는 것.
- 다른 사이트의 게시판 (롤 인벤, 디씨인사이드 등)을 확인해보았다. 다른 게시판의 경우, 게시글을 클릭한 후 뒤로 가기를 눌러 목록으로 돌아와도 필터가 초기화되지 않았다. 검색어 역시 그대로 유지되었다.
- 내가 게발한 게시판의 필터는 상태 관리 라이브러리가 아닌, 컴포넌트 내부에서 **useReducer** 훅을 이용해 구현한 것이다. 보통 필터가 유지되는 게시판의 경우, 필터 값과 검색어 값이 전역에서 관리된다고 한다. 로딩 때 스토어에 있는 값을 가져오기 때문에 초기화가 되지 않는 것.
- 지피티한테 방법을 물어보았다.
```js
브라우저 내장 기능 사용
브라우저의 내장 기능인 history.pushState() 를 사용하여 URL을 변경할 수 있습니다. 이를 이용하면 뒤로 가기를 했을 때도 이전 상태를 유지할 수 있습니다. 예를 들어, 게시글을 클릭했을 때 필터 정보와 함께 URL을 변경하여 이를 유지할 수 있습니다.

쿠키 또는 로컬 스토리지 사용
쿠키 또는 로컬 스토리지에 필터 정보를 저장하여, 게시글을 클릭했다가 뒤로 가기를 하더라도 정보를 유지할 수 있습니다. 이 방법은 브라우저가 닫히거나, 사용자가 직접 삭제하지 않는 이상 정보가 계속 유지됩니다.

상태 관리 라이브러리 사용
React 등의 상태 관리 라이브러리를 사용하여 필터 정보를 상태로 관리하면, 클릭 이벤트에 따라 상태를 업데이트하고 이를 유지할 수 있습니다. 이 방법은 상태 관리 라이브러리를 사용하는 애플리케이션에서 일반적으로 사용됩니다.

이 중 어떤 방법을 선택하느냐는 애플리케이션의 구조와 개발자의 개인적인 취향에 따라 다를 수 있습니다.
```
- 결국 방법은 상태 관리 라이브러리 사용밖에 없다는 결론을 내리고, 구현했던 게시판 필터와 검색창을 다시 만들어보기로 함.

# 2023-04-06
## 게시판 필터 상태 전역 관리로 변경 
### 결국 필터를 리덕스를 이용해 관리하기로 했다. 필터를 전역관리 하면 페이지를 왔다갔다 해도 필터나 검색조건이 풀리지 않음! 
1. slice 이름과 위치 정하기 
- 관리되는 데이터는 검색어, 필터조건, 글 타입(공지, F&Q, 자료 등), 정렬 등 페이지를 나갔다 들어와도 유지되어야 하는 값. 슬라이스 이름을 어떻게 붙일까? 하다가 searchSettings로 정함. 

2. 데이터 이관작업
- 컴포넌트 내에서 useReducer와 initialState를 이용해 관리되는 값 중 searchSettings에 넣어야 하는 아이들을 데리고 옴.
- 타입 선언 
- 초기값 설정


3. 리듀서 만들기
- 앞 컴포넌트에 있는 action들을 slice의 리듀서로 하나하나 만들어 줌.

4. 기존 setState로 되어있던 값들 dispatch로 바꾸어 줌!

5. 잘 동작함

### 문제점

- 홈 버튼 눌렀을 때는 모든 조건이 해제된 순수 메인 페이지가 보여져야 하는데, '뒤로 가기'를 눌렀을 때와 동일하게 동작함. 
- 게시글 안에 있는 또다른 게시글들이 터져버림 (글이 가지고 있는 offset때문에... )

내일 목표는 이 두 가지 문제를 모두 해결하는 것이다.


# 2023-04-07 
## (게시판 아님) 관리자가 아닌 일반사용자 로그인 시, '그룹설정'이 안 표시되는 문제 해결
- Setting에서 특정 그룹에 대한 설정을 '제한'으로 걸어 두면, 관리자가 아닌 일반 사용자한테는 '그룹 설정' 이라는 텍스트가 안 뜨고, 해당 그룹의 설정을 바꿀 수 없게 된다.
- 문제 상황 : 그룹 별로 '제한'을 각각 설정할 수 있음에도 불구하고, 일반 사용자 로그인 시 '그룹 설정'이라는 텍스트가 모두 사라져 있다. '제한'이 걸려있지 않은 그룹의 경우, '그룹 설정'이라는 텍스트가 떠야 한다.

1) Setting에서 특정 그룹에 대해 '제한'으로 저장 시 `isLimited`가 1로 넘어가는 걸 확인함.
2) '그룹 설정'이라는 텍스트를 사용하는 컴포넌트를 확인해옴, GET으로 끌어 오는 데이터에는 Setting에서 보낸 `isLimited` 여부를 확인할 수 있는 값이 없음.
3) 현재는 그룹별 제한 값을 확인하지 않고, 일반 사용자의 경우 무조건 '그룹 설정'이라는 텍스트를 보이지 않게 해 놓은 걸 확인 함 -> isLimited가 걸리지 않은 그룹을 찾아서, 해당 그룹에 접속하면 일반 사용자 역시 '그룹 설정'이라는 텍스트를 볼 수 있게 해야 함.
4) 백엔드에 isLimited 설정 확인할 수 있는 값 만들어달라고 요청. 
5) 수정해야 하는 컴포넌트에서 받아오는 그룹 데이터에 isLimited가 추가됨. (0인 경우에는 일반 사용자 제한 없음, 1인 경우에는 일반 사용자 제한됨)
6) isLimited 값을 이용해 그룹별로 일반사용자에게 '그룹 설정' 텍스트 노출여부 결정함. 

- 여담 : 우리가 받아오는 data는 tree 구조로 되어 있어서 적어놓은 과정보다 훨씬 복잡하게 데이터를 추출해야 했다...

# 2023-04-11
## 게시판 본문 아래에 나오는 게시글 목록 pagination에 오류 나오는 것 해결
### <img src="https://github.com/Anne-Hyeyeon/mystorage/blob/main/20230411_182847.png?raw=true" alt="screenshot" />

###
- 위와 같이, 본문 하단에 노출되는 게시글 목록에 문제가 있는 것이다. 위 사진은 예시일 뿐이다.
- 필터가 걸려있지 않을 때는 문제가 없다. 하지만 **필터 조건**이 걸렸을 때 오류가 생긴다. 검색어랑 필터 조건이 생길 경우 Main(게시판 첫 페이지, 목록)에서 불러오는 rnum들이 모두 바뀌기 때문이다. 하지만 Detail(본문 페이지) 안에서 불러오는 데이터의 rnum들은 변하지 않아 문제가 생기는 것.
- 본문 안에 있는 게시글 목록, 페이지네이션은 본문 안에서 불러오는 rnum에 따라 정해지기 때문임.
 
 1) 프론트단에서 rnum 이용하지 않고 pagination 수정할 수 있는 법 찾아봤는데, Main 게시판 목록에서 불러오는 rnum을 이용하는 법이 있었다. 하지만 Main과 Detail (본문) 컴포넌트가 연결되어있지 않아, Main 컴포넌트 값 사용하려면 리덕스 슬라이스를 새로 만들어야 했음.
 2) 결국 백엔드 팀에 본문에 들어오는 잘못된 rnum값을 수정해달라고 요청함
 3) 원래 detail get값엔 파라미터가 따로 없었는데, 검색 필터 (위에서 전역 상태관리하게 된) 값을 가지고 와 파라미터로 쏴 줬더니 rnum이 똑바로 들어오게 됨.
 4) 전체 게시글 개수에서 rnum을 뺀 다음, 오프셋으로 나눈 값을 Math.floor해서 페이지 값 구함. 정상 작동함
      
      
# 2023-04-1
## 게시판 - lodash isEqual을 사용할 때, 특정 요소는 빼고 비교하는 방법이 있을까?
###
<img src="https://github.com/Anne-Hyeyeon/mystorage/blob/main/search.png?raw=true" alt="example" />
- 게시판의 '필터 해제'버튼은, lodash의 isEqual을 이용해서 구현된 것이다. 게시판 메인 state에는 두 개의 값이 있는데, 원래 필터값은 `initFilter`에 담기고 변경된 필터값은 `filter`에 담긴다. 
- 자세히 설명 -> 우선 사용자가 필터 조건들을 클릭하면 onChange를 통해 값이 `filter`에 들어간다.
- 필터 설정 후 '검색'버튼을 누르면 filter값이 `initFilter`값 안에 들어간다. (만약, 직전 설정된 필터값이 없으면 initialState의 필터값이 들어감.)
- 이때, 변경된 값을 탐지해서 '필터 해제'버튼을 활성화시킨다. 변경된 값이 있을 경우에만 '필터 해제'활성화. 이를 위해 isEqual(initFilter, filter) 함수를 사용한다.

### 문제 - 특정 요소를 빼고 비교를 해야 할 경우
- 사진에 보면 게시글 필터 중에는 '제목', '본문'이 있는데, initFilter값과 filter값을 비교할 때 저 '제목', '본문'체크박스 조건은 제외하고 비교하고자 함. (실제로 그런 기능이 필요한 건 아니지만, 혹시 **isEqual로 비교하는 중 특정 조건을 빼야 된다면 어떻게 해야 될까?** 라고 고민하다가...)
- 정답은 특정 요소를 제외하고 나머지를 비교하는 함수를 만드는 것!
- 참고로 '제목' '본문' 여부는 keywordType이라는 변수로 관리되고 있음.
```js
const isEqualWithoutKeywordType = (initFilter: Filter, filter: Filter) => {
  const { keywordType: k1, ...restInitFilter } = initFilter; 
  const { keywordType: k2, ...restFilter } = filter;
  return isEqual(restInitFilter, restFilter);
};
```
- initFilter와 filter를 받아와서 값 할당, 여기서 keyword_type를 제외한 나머지 값을 추출할 수 있다. keyword_type값을 뽑아서 k1, k2에 store 한 다음 나머지 값만 이용하면 됨 
- 문제는... 여기서 keywordType을 저장한 k1, k2가 사용되지 않아 노란색 줄이 쳐진다는 것
- 해결 -> k1, k2 저장 대신 `_` 사용하려고 했으나 typeScript 문법상 문제가 생김.
- 노란줄 없이 원하는 값 추출하는 법... 조금 더 고민해 보아야겠다.
###

# 2023-04-14
## Record Type of TypeScript
### What is Record Type? GPT의 답변
```
Record<string, T> is a type alias in TypeScript that defines an object type with string keys and values of type T. Essentially, it creates a type that represents an object where the keys are strings and the values can be of any type T.
```
- Record<string, T>는 타입스크립트에서 string key와 T type 타입을 가지고 있는 object의 별칭이다. 본질적으로, 이것은 key가 string이고 value가 T인 object라는 것을 나타내는 type를 생성한다.
```
For example, Record<string, number> would define an object where all the keys are strings, but the values are numbers. It can be used to create a strongly typed object when the keys are not known ahead of time, such as when parsing JSON data.
```
- 예를 들면, Record<string, number> 는 모든 key가 string이고 value가 numbers인 object를 정의하게 된다. 그것은 JSON data를 파싱할 때처럼 key를 미리 알 수 없을 때, strongly typed된 object를 생성하는 데 쓰일 수 있다. 
- 여기서 strongly typed 됐다고 함은 ->  Any attempt to pass a wrong kind of parameter as an argument, or to assign a value to a variable that is not implicitly convertible, will generate a compilation error.  

```js
type User = {
  name: string;
  age: number;
  email: string;
};

type UserDictionary = Record<string, User>;

const users: UserDictionary = {
  "user1": { name: "John", age: 25, email: "john@example.com" },
  "user2": { name: "Jane", age: 30, email: "jane@example.com" }
};

console.log(users["user1"].name); // Output: "John"
console.log(users["user2"].age); // Output: 30
```

### What is difference between Record Type and Index Signature? Record 타입과 Index Signature의 차이점
#### 두 개 다 object의 동적인 key의 type을 정의하는데 쓰인다. 차이점은 다음과 같다. 
1. **Syntax(구문)** : Record Type의 구문이 Index Signature에 비해 더 정확하고 가독성이 좋다.
2. **Usability(사용성)** : Record Type이 더 강력한데다가, object의 모든 key들을 특정 타입으로 지정하게 하는 추가 기능을 제공한다. 하지만 Index Signature의 경우 object의 key와 value 에 대한 타입만 설정하게 한다.
3. **Readability(가독성)** : Record Type은 동적인 키를 가지고 있는 object type을 정의하는 데 있어서 Self-documenting way(자기 설명적인 방식으로 코드를 작성하는 것 : 코드 자체가 정보를 제공하여, 그 의도와 작동 방식을 이해할 수 있도록 하는 것. 코드 내부에서 변수, 함수, 클래스, 메서드 등의 이름을 명확하고 직관적으로 지정하고, 주석 등을 최소화하여 `코드 자체`가 목적을 잘 설명하도록 하는 것.)인데다가 가독성을 좋게 한다. 
4. **Compatibility(호환성)** : Record Type은 Partial, Required, and Pick 등의 built-it TypeScript 타입들과 호환성이 좋다.
- 결론적으로, dynamic keys를 가지고 있는 object의 type을 지정하는 데 있어서는 Record Type이 더 좋은 선택이라고 할 수 있다. 왜냐하면 그것은 해독하고 유지하기에 더 쉬운 특징들을 제공하기 때문이다. 그러나, 만약 다이나믹 key에 대한 더 세밀한 타입 컨트롤이 필요하다면, index signature를 사용하는 게 더 나을 것이다.
