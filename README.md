# 소프트웨어 조사 - React
**팀원:**
- 컴퓨터학부 글솝/2023012004/정솔빈/solempty
- 전자공학부/2018113271/황재정/JaeJeongHwang
- 컴퓨터학부 인컴/2023012324/김세희/sei135
- 컴퓨터학부 인컴/2023009887/김나현/Dansoeun

## 1. 개요
- Meta에서 개발한 오픈 소스 자바스크립트 라이브러리입니다.
- 프론트엔드 개발자 사이에서 Angular JS, Vue.js와 더불어 많은 인기를 얻고 있다. 
- 웹 렌더링 기능 존재: UI/UX 및 DB, API(fetch, axios ...) 통신이 가능합니다.
- 모바일 앱 UI/UX로 제작 가능합니다.
  
## 2. 라이선스
> 회사 및 가격(예: 오토캐드 250만원/연) 또는 오픈소스(예: Apach 2.0) 등

MIT 라이선스 (BSD 라이선스에 기반)

## 3. 주요기능
> [React](https://ko.react.dev/)

1) 컴포넌트 구조
2) React의 핵심, 상태관리와 데이터 흐름
3) 리액트 도구, 테스트, 최적화
4) UI/UX 및 네비게이션

### 1. 컴포넌트 구조 - 나현
### React Design Pattern
- __Presentational & Container Component Pattern & Atomic Design Pattern & VAC Pattern __
- __Presentational Component__
  - 화면에 표시하는 것만 담당. props를 통해서 데이터나 콜백을 받아옴
  - UI와 관련된 상태만 가짐 (대표 예시: dropdown 열림 여부)
- __Container Component Pattern__
  - 동작, data fetch 등의 business logic만을 담당
  - Presentational Component에 보여줄 데이터를 가져오거나, 변화시키거나, 행동/동작 등을 정의
  - DOM Markup이나 스타일(css) 없이, 연관이 있는 서브 컴포넌트를 렌더링
  - stateful한 경향
---
- **Presentational Component**
1. 보편적인 폴더 구조
```
components
├── Login
│   ├── LoginContainer.tsx
│   ├── LoginPresentation.tsx
│   └── Login.style.ts
└── User
    ├── UserContainer.tsx
    ├── UserPresentation.tsx
    └── User.style.ts
...
```

#### 장점
- 기능과 UI를 명확하게 분리하므로, 코드가 복잡할수록 가독성이 개선되고 유지보수가 용이해짐
- UI 컴포넌트가 추출되므로, 마크업이 편리, UI 재사용이 가능함
  
#### 단점
- hooks의 도입 이후, Dan Abramov는 이 패턴을 더 이상 추천하지 않음
  - 불필요하게 맹목적으로 패턴을 강제하게 됨
  - hooks의 도입으로 로직 분리가 쉬워지고, 로직 또한 재사용할 수 있게 됨

- **Component - Custom Hook**
  - hooks의 도입 이후, Dan Abramov가 새롭게 제안한 방식이다.

1. 보편적인 폴더 구조
```
components
├── ui
│   ├── atoms // 가장 작은 단위의 컴포넌트
│   │   ├── Input
│   │   └── Checkbox
│   ├── molecules // atom을 여러 개 조합한 컴포넌트 
│   │   └── LoginInputs
│   └── organisms // molecule과 atom을 조합하여 만든 컴포넌트
│       └── LoginComponent
├── templates // 컴포넌트를 넣어 사용할 레이아웃
│   ├── LoginTemplate
│   ├── UserTemplate
│   └── BookTemplate
└── pages // 가장 큰 단위의, templates에 atom, molecule, organism 등을 주입한 컴포넌트
    └── Login
```

#### 장점
- UI에서 기능을 명확하게 분리함
- 연관된 기능 단위로 묶어서 분리할 수 있으므로, 로직을 재사용할 수 있음


- **Atomic Design Pattern**
  - 2013년 Brad Frost에 의해 처음으로 제시되었다. 원래는 디자인 시스템을 위한 패턴이다.
  - 디자인 시스템에서 컴포넌트를 효율적으로 구성하는 방식에 대한 내용이다.
 
1. 보편적인 폴더 구조
```
components
├── ui
│   ├── atoms // 가장 작은 단위의 컴포넌트
│   │   ├── Input
│   │   └── Checkbox
│   ├── molecules // atom을 여러 개 조합한 컴포넌트 
│   │   └── LoginInputs
│   └── organisms // molecule과 atom을 조합하여 만든 컴포넌트
│       └── LoginComponent
├── templates // 컴포넌트를 넣어 사용할 레이아웃
│   ├── LoginTemplate
│   ├── UserTemplate
│   └── BookTemplate
└── pages // 가장 큰 단위의, templates에 atom, molecule, organism 등을 주입한 컴포넌트
    └── Login
```
#### 장점
- 컴포넌트를 기능의 단위로 나누므로 UI 재사용성이 뛰어남
- application과 분리하여 컴포넌트를 개발하고 테스트할 수 있음. 스타일 가이드 도구 사용이 용이.
- 통합 개발 시 백엔드 로직에 의존하지 않음
- 디자인을 일관성 있게 통일하기에 용이 (디자인 시스템 구축에 용이한 구조)

#### 단점
- 디자인 시스템을 구축하기 위한 초기 비용이 필요
  - 어디까지를 어느 단위로 볼 것인가에 대한 논의
  - 최소 단위를 재사용하기 위한 디자인 시스템
- 로직과 상태를 낮은 단위까지 공유해야 하기 때문에 props drilling issue 발생할 수 있음
- 컴포넌트가 명확하게 분리되어 있으므로, 상위 컨테이너 컴포넌트의 사이즈를 모를 때 미디어쿼리를 사용하기 어려울 수 있음.

- **VAC Pattern**
- View Asset Component.
- 기존의 View 컴포넌트에서 jsx와 관련된 영역을 props object로 추상화한 뒤, VAC로 분리해서 개발하는 방식
- 비즈니스 로직 뿐 아니라 UI 로직에서도 렌더링 관심사를 명확하게 분리하는 것이 목적


### 2. React의 핵심, 상태관리와 데이터 흐름 - 재정
#### 상태관리
상태 관리의 용이성과 성능 최적화를 위해 상태관리 라이브러리를 사용할 수 있다. 

#### 데이터 흐름
React의 개발 방식은 페이지 단위가 아닌 컴포넌트 단위로 시작하며, 상향식(Bottom-Up)으로 앱을 만들어 가는 특징이 있다.
이 방식은 테스트가 쉽고 확장성이 뛰어나다는 장점이 있다.

---
### 3. 리액트 도구, 테스트, 최적화 - 솔빈
#### 프로젝트 초기 설정 도구

예전에는 [Webpack](https://webpack.kr/)이나 [Babel](https://babeljs.io/docs/) 같은 모듈을 설치하고 설정해야 리액트 앱을 시작 할 수 있었지만, 현재는 [CRA](https://create-react-app.dev/docs/getting-started)를 이용해 가장 빠르고 쉽게 리액트를 설치할 수 있습니다.

![image](https://github.com/user-attachments/assets/bcd9a05b-ba33-4b76-9b0d-d2652af35f60)

여기서 `Webpack`이란 오픈소스 자바스크립트 모듈 번들러로서 여러 개로 나누어져 있는 파일들을 하나의 자바스크립트 코드로 압축하고 최적화 하는 라이브러리입니다. 여러 파일의 JS 코드를 압축하여 최적화 할 수 있어 로딩에 대한 네트워크 비용을 줄일 수 있다는 장점이 있습니다. 또, 모듈 단위로 개발이 가능하여, 가독성과 유지보수하기 좋습니다.

Babel은 최신 자바스크립트 문서를 지원하지 않는 브라우저들을 위해서 최신 자바스크립트 문법을 구형 브라우저에서도 돌 수 있게 변환시켜주는 라이브러리입니다.
```
// Babel ES6
[1, 2, 3].map((n) => n + 1);

//Babel Output ES5
[1, 2, 3].map(function(n) {
  return n + 1;
});
```
`npx create-react-app <폴더이름>` 이라는 명령어를 사용하면 바로 React 어플리케이션을 만드는데 필요한 세팅을 한번에 할 수 있습니다.


#### 코드 일관성을 위한 도구
[Eslint](https://eslint.org/docs/latest/)와 [Prettier](https://prettier.io/docs/en/)를 이용해 여러 사람이 함께 프로젝트를 진행할 때 같은 코딩 스타일을 유지할 수 있습니다.

느슨한 형식의 언어인 JavaScript에서는 코드 에러가 자주 발생합니다. JavaScript는 동적 분석(프로그램을 직접 실행해서 코드를 분석하는 방법)으로 에러를 찾기 때문에, 코드를 직접 실행해서 확인해봐야하는데

이를 도와주는 것이 Linter입니다. Linter는 코드를 정적으로 분석하기 때문에, 프로그램을 실행하지 않고도 코딩 컨벤션에 위배되는 코드나 안티 패턴을 자동으로 검출힙니다. 추가적으로 간단한 코드 포맷팅 기능도 있습니다.

Prettier를 사용하면 코드를 완전히 다시 작성해줍니다. 변경이 필요한 부분만 바꾸는 것이 아니라, 코드 전체를 새로 작성되며 코드 내용은 변하지 않고, 구조적 뷰만 변경됩니다.

### React Testing Library, Jest를 통한 단위 테스트와 통합 테스트
테스트 코드는 소프트웨어 개발에 있어 품질과 안정성을 높이는데 큰 도움을 줍니다. 유지보수측면에서 리팩터링을 할 때 도움이 되기도 합니다.
테스트 코드를 작성하다 보면 테스트가 가능하게 작성하다보니 코드를 간결하고 유연하게 작성하거나, 의존성을 최소화 하는 방향으로 코드를 만들게 됩니다. 즉, 자연스레 유지보수성과 재사용성이 높아지고, 문서화 측면 등에서도 도움이 됩니다.

#### React Testing Library
[React Testing Library](https://testing-library.com/docs/react-testing-library/intro/)는 React 컴포넌트를 테스트하기 위한 라이브러리로, DOM을 기반으로 실제 사용자와 상호 작용하는 것처럼 테스트를 작성할 수 있습니다.
BBD 방법론에 울리며 간결하면서도 꼭 필요한 API를 지원합니다. BBD란 사용자 행위를 기반으로 시나리오를 구성해 테스트 코드를 작성하는 방식입니다. Jest와 jsdom기반의 브라우저 DOM Testing입니다.

#### Jest
[Jest](https://jestjs.io/)는 거의 모든 기능과 플랫폼을 지원하고 Facebook에서 개발한 JavaScript Testing Framework입니다.

#### 단위 테스트
단위 테스트(Unit Testing)는 애플리케이션의 가장 작은 단위인 개별 함수 또는 컴포넌트가 올바르게 작동하는지 확인하는 테스트입니다.

1. 새로운 기능 추가 시: 새로운 기능을 추가하거나 기존 기능을 수정할 때 기존 기능이 의도대로 작동하는지 확인할 수 있습니다.
2. 버그 수정 시: 버그를 수정한 후 동일한 버그가 다시 발생하지 않도록 보장합니다.
3. 코드 리팩토링 시: 코드 구조를 변경할 때 기능이 유지되는지 확인할 수 있습니다.
4. 문서화: 단위 테스트는 코드의 작동 방식을 이해하는 데 도움을 줄 수 있습니니다.

**Jest**는 단위 테스트, 통합 테스트, 스냅샷 테스트 등을 지원하며, 쉽게 설정하고 사용할 수 있는 환경을 제공합니다.

- 간편한 설정: CRA(Create React App) 프로젝트에는 이미 Jest가 포함되어 있어 추가 설정이 필요 없어요. 별도의 설정 없이 바로 사용할 수 있습니다.
- 풍부한 기능: Jest는 단위 테스트, 통합 테스트, 스냅샷 테스트 등 다양한 테스트를 지원하며, 다양한 matcher와 assertion을 제공합니다. 또한, 코드 커버리지 측정, 모킹(mocking), 타이머 제어 등의 기능도 포함되어 있습니다.
- 빠른 테스트 실행: Jest는 테스트 실행 속도가 빠르며, 변경된 파일만 테스트하는 watch 모드도 지원합니다. 이를 통해 개발 중에 빠르게 피드백을 받을 수 있습니다.
- 스냅샷 테스트: Jest는 스냅샷 테스트를 지원하여, 컴포넌트의 UI가 변경되었는지 쉽게 확인할 수 있습니다.

**React Testing Library**는 테스트의 유지보수성을 높이고, 사용자 중심의 테스트를 작성하는 데 중점을 두고 있습니다.

- 사용자 중심 테스트: React Testing Library는 컴포넌트를 실제 사용자와 상호 작용하는 방식으로 테스트할 수 있게 해줍니다. 이를 통해 더 현실적이고 신뢰성 있는 테스트를 작성할 수 있습니다.
- 간단한 API: React Testing Library는 간단하고 직관적인 API를 제공하여, 쉽게 테스트를 작성할 수 있습니다. 테스트 작성 시 불필요한 구현 세부 사항에 집중하지 않고, 컴포넌트의 실제 동작에 집중할 수 있습니다.
- Jest와의 통합: React Testing Library는 Jest와 완벽하게 통합되어, Jest의 matcher와 assertion을 그대로 사용할 수 있습니다.
- 유지보수성 향상: React Testing Library는 테스트 코드의 유지보수성을 높이는 데 도움을 줍니다. 컴포넌트의 내부 구현보다는 외부 동작에 중점을 두어 테스트를 작성하므로, 리팩토링 시 테스트 코드의 변경을 최소화할 수 있습니다.

#### 통합 테스트
통합 테스트는 여러 개의 모듈이나 컴포넌트가 함께 작동하는지 확인하기 위해 수행하는 테스트입니다.
각 개별 모듈이 올바르게 작동하더라도, 상호작용하면서 문제가 발생할 수 있기 때문에 중요합니다.

1. 여러 컴포넌트나 모듈이 상호작용할 때 예상치 못한 오류가 발생할 가능성이 있을 때
2. 데이터베이스, API 등 외부 시스템과의 통합을 확인해야 할 때
3. 사용자 플로우를 검증하고 싶을 때 (예: 폼 제출, 페이지 내비게이션)
위와 같은 경우에서 사용합니다.

위 단위 테스트에서 설명한 Jest와 React Testing Library를 사용해 통합 테스트를 진행할 수 있습니다.

### 최적화
#### React.memo를 이용한 성능 최적화
리엑트는 컴포넌트를 먼저 렌더링 한 뒤, 이전에 렌더링 된 결과와 비교하여 DOM 업데이트를 결정합니다. 만약 렌더링 결과가 이전과 다르다면 리엑트는 DOM을 업데이트 합니다.

이 과정에서 만약 컴포넌트가 [React.memo()](https://ko.react.dev/reference/react/memo)로 둘러 쌓여 있다면, 리엑트는 컴포넌트를 렌더링하고 결과를 Meomoizing합니다. 그리고 다음 렌더링이 일어날 때 렌더링하는 컴포넌트의 props가 같다면, Memoizing된 내용을 재사용합니다.

여기서 Memorizing이란 주어진 입력값에 대한 결과를 지정함으로써 같은 입력값에 대해 함수가 한번만 실행되는 것을 의미합니다.
처음 렌더링할 때 결과를 Memoizing하고 다음 렌더링 시 props가 같기 때문에 Memoizing된 내용을 재사용합니다.

**React.memo()**는 props 혹은 props의 객체를 비교할 때 얕은 비교를 하고, 비교 방식을 원하는대로 수정하고 싶다면 React.memo()의 두 번째 매개변수로 비교함수를 넣어주면 됩니다.

원하는 컴포넌트를 React.memo로 감싸주면 React.memo가 적용되고 필요하지 않은 컴포넌트는 렌더링이 되지 않습니다. 

리렌더링을 막기 위한 도구로 사용하면 버그 유발 가능성이 있기 때문에 profiler를 이용해서 성능상 이점이 있는지 확인 후 사용해야합니다.

#### useCallback을 이용한 함수 최적화
원래 컴포넌트가 렌더링될 때 그 안에 있는 함수도 다시 만들게 됩니다.
하지만 똑같은 함수를 컴포넌트가 리렌더링 된다고 해서 계속 만들게 되면 자식 컴포넌트에 props로 내려준다면 함수를 포함하는 컴포넌트가 리렌더링 될 때 마다 자식 컴포넌트도 함수가 새롭게 만들어져 계속 리렌더링 하게 됩니다. 이를 해결하기 위해 [useCallback](https://ko.react.dev/reference/react/useCallback)을 사용합니다.

**useCallback**은 memoization된 함수를 반환하는 함수입니다. useCallback 안에 콜백 함수와 의존성 배열을 순서대로 넣어서 적용할 수 있습니다.

여기서 Memoization은 비용이 많이 드는 함수 호출의 결과를 저장하고 동일한 입력이 다시 발생할 때 캐시된 결과를 반환하여 컴퓨터 프로그램의 속도를 높이는데 주로 사용되는 최적화 기술입니다.

함수 내에서 참조하는 state, props가 있다면 의존성 배열에 추가하면 되고, useCallback으로 인해서 의존성 배열에 추가해준 state 혹은 props가 변하지 않는다면 함수는 새로 생성되지 않습니다.
새로 생성되지 않기에 메모리에 새로 할당되지 않고 동일 참조 값을 사용하게 됩니다.
의존성 배열에 아무것도 없다면 컴포넌트가 최초 렌더링 시에만 함수가 생성되며 그 이후에는 동일한 참조 값을 사용하는 함수가 됩니다.

#### useMemo를 이용한 결과 값 최적화
Components 내의 compute 함수가 만약 복잡한 연산을 수행하면 결과 값을 리턴하는데 오랜 시간이 걸립니다. 이때 컴포넌트가 계속 리렌더링 된다면 수행하는데 오랜 시간이 걸리고 UI 지연 현상이 일어납니다. 이를 해결하기 위해 [useMemo](https://ko.react.dev/reference/react/useMemo)를 이용합니다.

**useMemo**는 compute 함수에 넘겨주는 a, b의 값이 이전과 동일하다면 컴포넌트가 리렌더링 되더라도 연산을 다시 하지 않고 이전 렌더링 때 저장해두었던 값을 재활용합니다.

useMemo로 해당 내용을 감싸준 후 첫 번째 인수에 의존성 배열의 compute 함수에서 사용하는 값을 넣어주면 적용됩니다.

---

### 4. UI/UX 및 네비게이션 - 세희
### Router
#### Routing
사용자가 요청한 URL에 따라 해당 URL에 맞는 페이지를 보여주는 것이 ROUTING입니다. ROUTING과 관련된 수많은 라이브러리 중 사람들이 가장 많이 쓰는 라이브러리가 REACT ROUTER입니다. React Router는 SPA(Single Page Application)에서 페이지 간 탐색을 가능하게 하며, URL 구조에 따라 다른 컴포넌트를 렌더링해 UI를 동적으로 구성할 수 있습니다.

여기서 SPA는 전체 페이지를 갱신하는 것이 아니라, 서버로부터 필요한 데이터만 받아 갱신하면 되기 때문에 사용자와 상호작용이 빠르고, 서버에서는 요청받은 데이터만 전달하면 되기에 서버 과부하가 적어진다는 장점을 갖고 있습니다. 하지만, SPA로 웹페이지를 구현할 경우 자바스크립트 파일의 크기가 커지며, 그렇기 때문에 처음 웹페이지를 불러올 때 시간이 오래 걸릴 수 있다는 단점이 있습니다.

#### UI
UI는 버튼, 텍스트, 이미지와 같은 작은 요소로 구성되어 있습니다. React를 통해 작은 요소들을 재사용하고 중첩할 수 있는 컴포넌트로 조합할 수 있습니다. 여기서 웹사이트부터 휴대폰 앱에 이르기까지 화면에 있는 모든 것을 컴포넌트로 나눌 수 있습니다.

#### 트리와 UI의 관계
React는 서로 중첩된 많은 컴포넌트로 구성되어 있습니다. React와 많은 다른 UI 라이브러리는 UI를 트리로 모델링하며 애플리케이션을 트리고 생각함으로써 컴포넌트 간의 관계를 이해합니다.
- 트리로서의 UI
  - 트리는 요소와 UI 사이의 관계 모델
  - UI는 종종 트리 구조를 사용하여 표현됨
  - 예시
    - 브라우저는 HTML([DOM](https://developer.mozilla.org/ko/docs/Web/API/Document_Object_Model/Introduction))과 CSS([CSSOM](https://developer.mozilla.org/ko/docs/Web/API/CSS_Object_Model))을 모델링하기 위해 트리 구조 사용
    - 모바일 플랫폼은 뷰 계층 구조를 나타내는 데 트리를 사용
브라우저와 모바일 플랫폼처럼 React도 React 앱의 컴포넌트 간의 관계를 관리하고 모델링하기 위해 트리 구조를 사용합니다. 트리는 React 앱에서 데이터가 흐르는 방식과 렌더링 및 앱 크기를 최적화하는 방법을 이해하는 데 유용한 도구입니다.
![image](https://ko.react.dev/_next/image?url=%2Fimages%2Fdocs%2Fdiagrams%2Fpreserving_state_dom_tree.dark.png&w=1080&q=75)
