# NomadCoders - 실전형 리액트 Hooks 10개 Studynote

## Intro to useEffect
-  useEffect 는 매우 많은 use를 가지고 있다.
- `componentWillUnMount`, `componentDidMount`, `componentDidUpdate` 와 유사한 기능
- componentDidMount의 역할 : 새로고침시 함수를 실행시킴 (첫 번째 인자)
- componentWillUpdate의 역할 : 클릭시 함수를 실행시킴 
- useEffect는 2개의 인자를 받는다. 
- 첫번째는 function으로서의 effect (ComponentDidMount())
- 두 번째는 depencency(deps)  
- deps가 있다면, effect는 deps 리스트에 있는 값일 때만 변하도록 활성화된다. (ComponentDidUpdate)
- deps가 비어있으면, 첫 번째 인자로 들어온 함수가 딱 한 번만 실행된다. 
- deps는 아주 중요한 개념이다!

## useTitle 
- useEffect를 이용해서 title을 업데이트 시켜주는 hook.
- useTitle 인자에 title 이름을 넣으면 페이지 title이 변경된다.
```js
import { useEffect, useState } from "react";
import "./styles.css";

const useTitle = (initialTitle) => {
  const [title, setTitle] = useState(initialTitle);
  const updateTitle = () => {
    const htmlTitle = document.querySelector("title");
    htmlTitle.innerText = title;
  };
  useEffect(updateTitle, [title]);
  return setTitle;
  // APp 컴포넌트에서 페이지 타이틀 설정 위해서는 setTitle이 필요하다. return 시켜서 컴포넌트 내 titleUpdater에 저장
};

export default function App() {
  const titleUpdater = useTitle("Loading...");
  setTimeout(() => titleUpdater("Home"), 2000);
  return (
    <div className="App">
      <h1>useTitle</h1>
      <h2>2초 뒤에 title이 바뀝니다!</h2>
    </div>
  );
}
```

## useClick
- reference가 무엇인가? 기본적으로 우리의 component의 어떤 부분을 선택할 수 있는 방법이다. (document.getElementById처럼)
- react에 있는 모든 component는 reference element를 가지고 있다. (ref prop 이용 가능)
- 쓰는 방법 : const 변수명 = useRef();  input 등에 ref 로 변수명 넣어주기.
- 
