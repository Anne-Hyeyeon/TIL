### 2023-04-26 (화)

# 모든 프로젝트에 쓰이는 리액트 훅 7가지 written by Reed Barger

https://medium.com/webdevhero/7-react-hooks-to-use-in-every-project-584d7e46810

```ts
단어 정리
functionality : (컴퓨터, 전자 장치의 기능)
across :
clarify :
on one's own :
intersect : 만나다, 교차하다, 가로지르다.
within : ~내에서
```

훅(Hooks)은 리액트의 강력한 특징 중 하나입니다.<br><br>

훅을 사용하면, 우리가 만든 애플리케이션의 컴포넌트에서 특정한 기능을 쉽게 재사용할 수 있습니다. 이처럼, 훅의 가장 큰 이점은 재사용성입니다. 당신은 컴포넌트뿐만 아니라, 서로 다른 프로젝트에서도 훅을 쉽게 재사용할 수 있습니다. <br><br>

여기, 제가 진행하는 모든 리액트 프로젝트에서 사용되는 가장 중요한 리액트 훅 7개가 있습니다. 오늘 바로 그 훅들을 당신의 프로젝트에서 사용해 보세요. 그리고 그 훅들이 리액트 앱을 만드는 데 효과적인지 직접 확인해 보시기 바랍니다.<br><br>

시작하기 전에, 모든 리액트 훅을 직접 만들 필요는 없다는 사실을 분명히 해 두어야 할 것 같습니다. 사실, 제가 소개할 모든 훅들은 `@mantine/hooks` 라이브러리부터 온 것입니다. <br><br>

Mantine은 많은 훅과 기타 기능을 보유한 훌륭한 서드파티 라이브러리(third-part library)입니다. 이 라이브러리를 이용하면, 당신이 생각하는 리액트 앱에 필요한 대부분의 중요한 기능들을 다 구현할 수 있습니다.<br><br>

`@mantine/hooks`의 공식 문서는 https://mantine.dev/ 에서 확인할 수 있습니다.

## The `useIntersection` Hook

유저들이 당신의 앱에서 스크롤을 내렸을 때, 당신은 당신이 구현한 페이지 구성요소들이 언제 유저들에게 보여지는지를 알아야 할 것입니다. <br><br>

예를 들면, 당신은 유저가 특정 요소를 보았을 때만 애니메이션이 시작되게끔 페이지를 구현하고자 할 수도 있습니다. 또는, 유저가 페이지에서 어느 정도 스크롤을 내렸을 때 요소를 숨기거나 나타나게 하게끔 만들어야 할 수도 있습니다. <br><br>

사용자에게 웹 페이지 요소가 언제 보여지는지에 대한 정보를 얻기 위해서, 우리는 Intersection Observer API라는 것을 사용할 수 있습니다. 이 API는 브라우저 안에 내장되어 있는 Javascript API 입니다. <br><br>

우리는 순수한 자바스크립트를 이용해, 그 API를 직접 사용할수도 있습니다. 하지만 스크롤 컨테이너 내에서 특정 요소가 교차하는지에 대한 정보를 얻는데 있어 가장 좋은 방법은, 바로 `useIntersection hook`을 사용하는 것입니다.

```js
import { useRef } from "react";
import { useIntersection } from "@mantine/hooks";

function Demo() {
  const containerRef = useRef();
  const { ref, entry } = useIntersection({
    root: containerRef.current,
    threshold: 1,
  });
  return (
    <main ref={containerRef} style={{ overflowY: "scroll", height: 300 }}>
      <div ref={ref}>
        <span>{entry?.isIntersecting ? "Fully visible" : "Obscured"}</span>
      </div>
    </main>
  );
}
```
