# 2023-12-07
## tsconfig.json 설정과 express
### 상황
express가 import 되지 않는다. type: module을 tsconfig.json 에 추가하니 정상적으로 import된다.
### type: "module"`을 `package.json` 파일에 추가하는 것이란?
- type: "module"`을 `package.json` 파일에 추가하는 것은 Node.js에서 ES 모듈 문법을 사용하기 위한 설정이다.
- ES 모듈은 JavaScript의 공식 표준 모듈 시스템으로, `import`와 `export` 문을 사용하여 모듈을 불러오고 내보낼 수 있게 해 준다.
- `package.json`에 `type: "module"`을 추가하면, Node.js는 해당 프로젝트 내의 `.js` 파일들을 ES 모듈로 취급한다. 이는 다음과 같은 효과를 가진다.

###  type: "module"`을 `package.json` 파일에 추가하면 얻을 수 있는 효과
1. **ES 모듈 문법 사용 가능**: `import`와 `export` 문을 사용하여 모듈을 불러오고 내보낼 수 있다. 예를 들어, Express를 불러오는 방법은 `const express = require('express');`에서 `import express from 'express';`로 변경된다.
2. **모듈 호환성**: 최신 JavaScript 라이브러리나 프레임워크 중에는 ES 모듈 문법을 사용하는 것들이 많은데, `type: "module"` 설정은 이러한 라이브러리와의 호환성을 높인다. 

### 결론
- Express 자체가 `type: "module"` 설정에 의존하는 건 아님. 이 설정을 통해 최신 JavaScript 문법을 사용하여 Express 애플리케이션을 구축할 수 있게 되는 것임. 
- 따라서, 이 설정은 Express가 작동하는 것이 아니라, Express와 같은 모듈을 ES 모듈 문법으로 사용할 수 있게 해주는 역할을 함.
