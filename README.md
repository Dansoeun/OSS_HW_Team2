# 소프트웨어 조사 - React
**팀원:**
- 컴퓨터학부 글솝/2023012004/정솔빈/solempty
- 전자공학부/2018113271/황재정/JaeJeongHwang
- 컴퓨터학부 인컴/2023012324/김세희/sei135
- 컴퓨터학부 인컴/2023009887/김나현/Dansoeun

## 1. 개요
React는 Meta(전 Facebook)에서 개발한 오픈 소스 자바스크립트 라이브러리입니다.

2013년 5월에 오픈소스로 처음 공개가 되었으며 페이스북 내부에서는 2011년부터 사용되고 있습니다. 
오픈소스로 공개 된 이후로 간단한 사용 방법과 Facebook이라는 서포트, 그리고 큰 커뮤니티로 인해 빠르게 확산되어 많은 곳들에서 사용되고 있습니다.
React는 브라우저의 웹 페이지 뿐 아니라, 앱 속의 웹뷰, 실제 네이티브 앱, 영수증 등등 다양한 곳에서 활용되고 있습니다
현재 React 라이브러리 & 프레임워크 중에 가장 많이 사용되고 있고, 프론트엔드에서 매우 중요한 기술 중 하나입니다.
  
## 2. 라이선스

MIT 라이선스 (BSD 라이선스에 기반)
```
Copyright (c) <연도> <저작권 소유자>
Permission is hereby granted, free of charge, to any person
obtaining a copy of this software and associated documentation
files (the "Software"), to deal in the Software without
restriction, including without limitation the rights to use,
copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the
Software is furnished to do so, subject to the following
conditions:
```
```
The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.
```
```
THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES
OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT
HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY,
WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING
FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR
OTHER DEALINGS IN THE SOFTWARE.
```

1. 이 소프트웨어를 누구라도 무상으로 제한없이 취급해도 좋다. 단, 저작권 표시 및 이 허가 표시를 소프트웨어의 모든 복제물 또는 중요한 부분에 기재해야 한다.
2. 저자 또는 저작권자는 소프트웨어에 관해서 아무런 책임을 지지 않는다.

## 3. 주요기능

1) 컴포넌트 구조
2) React의 핵심, 상태관리와 데이터 흐름
3) 리액트 도구, 테스트, 최적화
4) UI/UX 및 네비게이션
### 1. 컴포넌트 구조 - 나현
#### 1-1. 컴포넌트 구조
#### React Design Pattern
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
- #### **Presentational Component**
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

-  ## **Component - Custom Hook**
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


- ## **Atomic Design Pattern**
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

- ## **VAC Pattern**
- View Asset Component.
- 기존의 View 컴포넌트에서 jsx와 관련된 영역을 props object로 추상화한 뒤, VAC로 분리해서 개발하는 방식
- 비즈니스 로직 뿐 아니라 UI 로직에서도 렌더링 관심사를 명확하게 분리하는 것이 목적

---
#### 1-2. [함수 컴포넌트와 클래스 컴포넌트, 컴포넌트와 Props](https://ko.legacy.reactjs.org/docs/components-and-props.html)
1. 함수 컴포넌트
```
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

2. 클래스 컴포넌트
```
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

3. 컴포넌트 합성
```
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

function App() {
  return (
    <div>
      <Welcome name="Sara" />
      <Welcome name="Cahal" />
      <Welcome name="Edite" />
    </div>
  );
}
```
- 컴포넌트는 자신의 출력에 다른 컴포넌트를 참조할 수 있음.

4. 컴포넌트 추출
```
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <img className="Avatar"
          src={props.author.avatarUrl}
          alt={props.author.name}
        />
        <div className="UserInfo-name">
          {props.author.name}
        </div>
      </div>
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```
- author(객체), text(문자열) 및 date(날짜)를 props로 받은 후 소셜 미디어 웹 사이트의 코멘트를 나타냄.
- props는 읽기 전용



---
### 2. React의 핵심, 상태관리와 데이터 흐름 - 재정
#### 상태관리 (State Management)
 React는 구성 요소 상태를 관리하기 위한 내장 기능을 제공하여 사용자 입력 처리, 데이터 가져오기, 애플리케이션 상태 변경에 따른 사용자 인터페이스 업데이트 등을 쉽게 처리할 수 있습니다. 주로 다음 두 가지 방법으로 이루어집니다

 - 로컬 상태(Local State): 각 컴포넌트에서 관리하는 상태로, 'useState' 훅을 사용하여 설정합니다.
```
const [count, setCount] = useState(0);
```
 - 전역 상태(Global State): 여러 컴포넌트에서 공유해야하는 상태로, 'useReducer' 훅이나 상태 관리 라이브러리(ex. Redux, MobX)를 사용해 관리할 수 있습니다.
```
const [state, dispatch] = useReducer(reducer, initialState);
```

#### 데이터 흐름(Data Flow) 

React는 단방향 데이터 흐름을 사용하고 있습니다.
즉, 데이터는 상위 컴포넌트에서 하위 컴포넌트로 흐릅니다.
상태 관리를 단순화하고 애플리케이션의 예측가능성과 안정성을 향상시킵니다.

이 방식은 테스트가 쉽고 확장성이 뛰어나다는 장점이 있습니다.

- Prop : 상위 컴포넌트에서 하위 컴포넌트로 데이터를 전달하기 위해 사용됩니다. 하위 컴포넌트는 props로 받은 데이터를 읽기만 할 수 있으며, 직접 변경할 수 없습니다.


```
  function ParentComponent() {
    const [value, setValue] = useState("Hello");
    return <ChildComponent message={value} />;
}

function ChildComponent({ message }) {
    return <div>{message}</div>;
}
```

- Lifting State Up: 여러 하위 컴포넌트가 동일한 데이터를 필요로 할 때, 상태를 가장 가까운 공통 상위(조상) 컴포넌트에서 관리합니다. 데이터의 일관성을 유지할 수 있습니다.

- Context API : 상태를 여러 컴포넌트에 전역적으로 제공하고 싶을 때 사용할 수 있습니다. 이를 통해 props를 깊게 전달하지 않고도 데이터에 접근할 수 있습니다.

```
const MyContext = React.createContext();

function App() {
    return (
        <MyContext.Provider value="Hello">
            <Child />
        </MyContext.Provider>
    );
}

function Child() {
    const value = useContext(MyContext);
    return <div>{value}</div>;
}

```
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
### React Router 및 UI 구성
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


#### 렌더 트리
다른 컴포넌트의 컴포넌트를 구성하는 것은 컴포넌트의 주요 특징입니다. 컴포넌트를 중첩하면 컴포넌트에 부모 자식의 개념이 생기며, 각 부모 컴포넌트는 다른 컴포넌트의 자식이 될 수 있습니다. 즉, 단일 렌더링에서 React 컴포넌트 간의 중첩 관계를 나타냅니다.

트리는 노드로 구성되어 있으며, 각 노드는 컴포넌트를 나타냅니다. React 렌더 트리에서 루트 노드는 앱의 Root 컴포넌트이며, 트리의 각 화살표는 부모 컴포넌트에서 자식 컴포넌트를 가리킵니다.

렌더 트리는 React 앱의 단일 렌더링을 나타내므로 [조건부 렌더링](https://ko.react.dev/learn/conditional-rendering)을 사용하면 부모 컴포넌트가 전달된 데이터에 따라 다른 자식을 렌더링할 수 있습니다.

렌더 트리가 렌더링 단계마다 다를 수 있지만, 최상위 컴포넌트는 루트 컴포넌트에 가장 가까운 컴포넌트이며, 그 아래의 모든 컴포넌트의 렌더링 성능에 영향을 미치고 가장 복잡합니다. 리프 컴포넌트는 트리의 맨 아래에 있으며 자식 컴포넌트가 없고 자주 다시 렌더링 됩니다.

#### 모듈 의존성 트리
트리로 모델링 할 수 있는 React 앱의 다른 관계는 앱의 모듈 의존성입니다. 컴포넌트를 분리하고 로직을 별도의 파일로 분리하면 컴포넌트, 함수 또는 상수를 내보내는 JS 모듈을 만들 수 있습니다.

모듈 의존성 트리의 각 노드는 모듈이며, 각 가지는 해당 모듈의 ``import``문을 나타냅니다. 트리의 루트 노드는 루트 모듈이며, 앤트리 포인트 파일이라고도 합니다. 일반적으로 루트 컴포넌트를 포함하는 모듈입니다.

렌더 트리와 비교하자면 유사한 구조가 있지만 몇 가지 차이점이 있습니다.
- 트리를 구성하는 노드는 컴포넌트가 아닌 모듈을 나타냅니다.
- ``inspirations.js``와 같은 컴포넌트가 아닌 모듈도 이 트리에 나타납니다. 렌더 트리는 컴포넌트만 캡슐화합니다.
- 
의존성 트리는 React 앱을 실행하는 데 필요한 모듈을 결정하는 데 유용합니다. React 앱을 프로덕션용으로 빌드할 때, 일반적으로 클라이언트에 제공할 모든 필요 JavaScript를 번들로 묶는 빌드 단계가 있습니다. 이 작업을 담당하는 도구를 [번들러](https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Understanding_client-side_tools/Overview#the_modern_tooling_ecosystem)라고 하며, 번들러는 의존성 트리를 사용해 포함해야 할 모듈을 결정합니다.

앱이 커짐에 따라 번들 크기도 커집니다. 번들 크기가 커지면 클라이언트가 다운로드하고 실행하는 데 드는 비용도 커집니다. 또한 UI가 그려지는 데 시간이 지체될 수 잇습니다. 앱의 의존성 트리는 느리게 페인트되는 큰 번들 크기를 디버깅하는 데 유용하며, 어떤 코드를 번들로 묶을지 최적화할 기회를 제공합니다.

### React Router를 이용한 라우팅과 페이지 전환 애니메이션
React Transition Group는 React 애플리케이션에서 애니메이션과 트랜지션 효과를 쉽게 적용할 수 있도록 돕는 라이브러리입니다. 이 라이브러리를 사용하면 컴포넌트의 생명주기 단계에 맞춰 다양한 애니메이션 효과를 적용하여 사용자 경험을 향상할 수 있습니다.
#### Transition 컴포넌트
- 요소가 DOM에 삽입되거나 제거될 때 애니메이션 효과를 추가할 수 있습니다.
- ``in`` prop을 통해 요소가 보이거나 사라질 시점에 애니메이션을 실행할 수 있습니다.
- 네 가지 주요 상태인 ``entering``, ``entered``, ``exiting``, ``exited``를 활용하여 단계별로 다양한 스타일을 지정할 수 있습니다.

#### CSSTransition 컴포넌트
- CSS 클래스 이름을 기반으로 애니메이션을 적용합니다.
- 애니메이션 클래스 이름을 자동으로 추가해주는 ``classNames`` prop을 제공하여, ``fade-enter``, ``fade-enter-active`` 등과 같은 규칙적인 CSS 스타일을 손쉽게 사용할 수 있게 합니다.

#### TransitionGroup 컴포넌트
- 여러 개의 자식 컴포넌트가 삽입되거나 제거될 때 개별적으로 애니메이션을 적용합니다.
- 자식 컴포넌트를 감싸서 리스트 내에서 요소들이 추가되고 제거될 때 개별적인 애니메이션을 설정할 수 있도록 합니다.

#### 애니메이션을 위한 유연한 API
- 각 단계의 이벤트(예: ``onEnter``, ``onExit``)를 직접 조정할 수 있어 다양한 방식의 커스터마이징이 가능합니다.
- JavaScript로 애니메이션을 제어하는 방식도 지원합니다.

React Transition Group는 React의 기본 스타일링을 사용하면서도 더 부드러운 화면 전환과 인터랙티브한 애니메이션을 쉽게 구현할 수 있어, 동적이고 반응성 높은 UI를 만들고자 할 때 유용합니다.

### SPA(Single Page Application)의 네비게이션 구조와 사용자 경험
#### SPA
단일 페이지 애플리케이션(Single page Application)인 SPA는 서버에서 필요한 데이터만 비동기로 받아와 현재 화면에서 동적으로 다시 렌더링 하는 방식을 의미합니다. 다수의 페이지를 표시하는 데 있어서 전통적인 방식으로 페이지를 전환하지 않고, 마치 하나의 페이지인 것처럼 처리하는 기술입니다.

그렇기 때문에 페이지 전환을 할 때도 깜빡임 없이 부드럽게 넘어가 사용자의 몰입도를 높여줍니다.

#### SPA의 장점
SPA는 필요한 영역만 캐치하여 즉각적인 화면의 변화를 줄 수 있기 때문에 사용자가 느끼기에 [네이티브 애플리케이션](https://leejss.github.io/2021-07-26/native-application)과 같은 자연스러운 사용감을 줄 수 있어 몰입도를 높일 수 있습니다.
- 빠른 로딩 속도와 반응성
  - 페이지 전환 시 서버에서 전체 화면을 새로 내려받지 않기 때문에, 뛰어난 반응성과 빠른 페이지 로딩을 가능하게 합니다.
- 향상된 사용자 경험
  - 웹사이트의 속도는 이탈률, 전환율, 수익, 사용자 만족도 및 검색 엔진 순위에 직접적인 영향을 미치기 때문에 SPA를 활용할 경우 고객 체류시간이 늘어나는 효과를 누릴 수 있습니다.
- 웹/모바일 공통 아키텍처 사용
  - API 백엔드 서버를 구성하여 비동기 방식으로 데이터를 가져와서 처리하기 때문에 별도의 백엔드용 API 서버 구현 없이 웹 애플리케이션 서비스를 제공할 수 잇습니다.
- 복잡한 대규모 애플리케이션 개발
  - SPA를 사용하면 애플리케이션 사용 시 트래픽이 줄어들어 도움을 얻을 수 있습니다. 비동기 방식으로 필요한 부분만 따로 업데이트가 가능하기 때문에 실시간 업데이트나 데이터 시각화와 같은 동적 요소가 많은 웹 앱을 만들 때 유용합니다.
 
#### SPA 적용 사례
- Gmail
  - 페이지 새로고침 없이 이메일을 읽고 작성할 수 있으며, 실시간 업데이트를 통해 빠르고 부드러운 사용자 경험을 제공합니다. AJAX를 통해 비동기적으로 처리되어 빠른 응답속도를 제공함으로써 많은 사람들의 사용을 유도하고 있습니다.
- Facebook
  - SPA의 강점을 살려 빠르게 데이터를 로딩하고 상호작용이 원활한 소셜 미디어 플랫폼입니다. 페이지 전환이 부드럽고, 사용자가 스크롤을 하면 콘텐츠가 끊임없이 로딩됩니다. 채팅, 온라인 친구 목록 확인, 최근 알림 등의 모든 기능이 하나의 페이지에서 이루어지며, 방대한 웹 애플리케이션을 효과적으로 사용하기 위해 React를 자체적으로 개발하여 SPA를 구현하고 있습니다.
- Netflix
  - SPA를 이용해 사용자들이 영화와 TV 프로그램을 빠르게 찾아볼 수 있도록 서비스를 제공하고 있습니다. 영화 및 TV 프로그램을 스트리밍 하는 동안 페이지 새로 고침 없이 사용자 경험을 지속적으로 제공하며, 영화 및 TV프로그램 목록을 스크롤 하면 새로운 목록을 화면 전환 없이 로딩해서 표시해주기에 화면에 변화된 부분만 동적으로 업데이트되어 사용자 경험을 최적화하고 있습니다.
