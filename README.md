# 소프트웨어 조사 - React
**팀원:**
> 전공/학번/이름/github계정 형식으로 작성해주세요.
- 컴퓨터학부 글솝/2023012004/정솔빈/solempty
- 전자공학부/2018113271/황재정 /JaeJeongHwang
- 컴퓨터학부 인컴/2023012324/김세희/sei135
- 컴퓨터학부 인컴/2023009887/김나현/Dansoeun

## 1. 개요
- Meta에서 개발한 오픈 소스 자바스크립트 라이브러리입니다.
- 웹 렌더링 기능 존재: UI/UX 및 DB, API(fetch, axios ...) 통신이 가능합니다.
- 모바일 앱 UI/UX로 제작 가능합니다.
  
## 2. 라이선스
> 회사 및 가격(예: 오토캐드 250만원/연) 또는 오픈소스(예: Apach 2.0) 등

MIT 라이선스 (BSD 라이선스에 기반)

## 3. 주요기능
> [React](https://ko.react.dev/) 조사할 때 참고하세용 출처는 하이퍼링크로 달았습니다

1) 컴포넌트 구조
2) 비동기 처리 및 DB 통신
3) Router
4) 유닛 테스트

### React Design Pattern - 나현
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




### React의 핵심, 상태관리와 데이터 흐름 - 재정

### React의 도구와 테스트-솔빈
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


### Router - 세희
#### Routing
사용자가 요청한 URL에 따라 해당 URL에 맞는 페이지를 보여주는 것이 ROUTING입니다. ROUTING과 관련된 수많은 라이브러리 중 사람들이 가장 많이 쓰는 라이브러리가 REACT ROUTER입니다. React Router는 SPA(Single Page Application)에서 페이지 간 탐색을 가능하게 하며, URL 구조에 따라 다른 컴포넌트를 렌더링해 UI를 동적으로 구성할 수 있습니다.

여기서 SPA는 전체 페이지를 갱신하는 것이 아니라, 서버로부터 필요한 데이터만 받아 갱신하면 되기 때문에 사용자와 상호작용이 빠르고, 서버에서는 요청받은 데이터만 전달하면 되기에 서버 과부하가 적어진다는 장점을 갖고 있습니다. 하지만, SPA로 웹페이지를 구현할 경우 자바스크립트 파일의 크기가 커지며, 그렇기 때문에 처음 웹페이지를 불러올 때 시간이 오래 걸릴 수 있다는 단점이 있습니다.

#### UI
UI는 버튼, 텍스트, 이미지와 같은 작은 요소로 구성되어 있습니다. React를 통해 작은 요소들을 재사용하고 중첩할 수 있는 컴포넌트로 조합할 수 있습니다. 여기서 웹사이트부터 휴대폰 앱에 이르기까지 화면에 있는 모든 것을 컴포넌트로 나눌 수 있습니다.
