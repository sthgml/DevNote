# frontend-survival-week01

프론트엔드 생존코스 1주차 과제

## 계속 써먹는 환경설정 총정리

### 1. 패키지 설치를 위한 node 시작하기

1. 노드를 설치한다.
    [nodejs.org](nodejs.org)
2. 터미널로 설치가 잘 되었는지 확인  
  `node -v`
3. 작업을 시작할 폴더를 생성한다. (대문자 금지)  
  `mkdir my-app`
4. 폴더 안으로 이동한다. (m치고 tab하면 자동완성됨)
  `cd my-app`
5. node package manager 사용을 시작한다.  
  `npm init` => 질문폭격  
  `npm init -y` => 다 yes로 대답

### 2. 패키지 설치

#### 0. .gitignore 작성

1. .gitignore파일을 만든다.  
  `touch .gitignore`
2. [.gitignore Gernerator](https://url.kr/8q2pao)
의 도움을 받아 내용물을 채운다.
3. 최소한 `node_modules` 와 `dist`는 넣자.

#### 1. TypeScript

1. dev 디펜던시로 타입스크립트를 install

    ```node
    npm i -D typescript
    npx tsc --init
    ```

1. tsconfig.json 파일 수정

    ```json
    // 주석되어있는 것을 풀고 
    "jsx": "preserve"
    // 수정
    "jsx": "react-jsx"
    ```

1. package.json 파일 수정 -> 문법오류 확인 명령어 check 추가 -> CI 등에 추가한다

    ```json
    //  `sciprts` 파트에 추가
    "chek": "tsc --noEmit"
    ```

#### 2. React

1. react 설치

    ```node
    npm i react react-dom
    npm i -D @types/react @types/react-dom
    ```

1. 기본코드 작성

    ```node
    mkdir src
    touch src/index.tsx
    touch src/App.tsx
    ```

1. App.tsx 내용채우기

    ```tsx
    import React from 'react';

    export default function App() {
      return (
        <div>Hello, world!</div>
      );
    }
    ```

1. index.tsx 내용채우기

    ```tsx
    import ReactDOM from "react-dom/client";
    import App from "./App";
    
    const element = document.getElementById('root');
    
    if (element) {
      const root = ReactDOM.createRoot(element);
      root.render(<App/>)
    }
    ```

#### 3. JEST + swc

1. jest 설치

    ```node
    npm i -D jest @types/jest @swc/core @swc/jest jest-environment-jsdom @testing-library/react @testing-library/jest-dom@5.16.4
    ```

1. jest.config.js 만들기

    ```js
    module.exports = {
      testEnvironment: 'jsdom',
      setupFilesAfterEnv: ['@testing-library/jest-dom/extend-expect'],
      transform: {
        '^.+\\.(t|j)sx?$': ['@swc/jest', {
          jsc: {
            parser: {
              syntax: 'typescript',
              jsx: true,
              decorators: true,
            },
            transform: {
              react: {
                runtime: 'automatic',
              },
            },
          },
        }],
      },
      testPathIgnorePatterns: [
        '<rootDir>/node_modules/',
        '<rootDir>/dist/',
      ],
    };
    ```

1. jest-setup.js 만들기

    ```js
    import '@testing-library/jest-dom';
    ```

1. src/App.test.tsx 만들기

    ```tsx
    import { render } from '@testing-library/react';

    import App from './App';

    describe('App', () => {
      it('renders greeting message', () => {
        const { container } = render(<App />);

        expect(container).toHaveTextContent('Hello, world!');
      });
    });
    ```

1. package.json scripts에 명령어 추가

    ```json
    {
      "scripts": {
        // ...(전략)...
        "test": "jest"
      }
    }
    ```

1. 명령어 써보기

    ```node
    npm test
    ```

#### 4. ESLint

1. eslint를 설치한다.  

    ```node
    npm i -D eslint
    npx eslint --init
    ```

1. 질문에 대답한다.  

    ```node
    ? How would you like to use ESLint? …
    ❯ To check syntax, find problems, and enforce code style

    ? What type of modules does your project use? …
    ❯ JavaScript modules (import/export)

    ? Which framework does your project use? …
    ❯ React

    ? Does your project use TypeScript?
    › Yes

    ? Where does your code run? …
    ✔ Browser

    ? How would you like to define a style for your project? …
    ❯ Use a popular style guide

    ? Which style guide do you want to follow? …
    ❯ Airbnb: https://github.com/airbnb/javascript
    ❯ XO: ~~

    ? What format do you want your config file to be in? …
    ❯ JavaScript

    ? Would you like to install them now with npm?
    › Yes
    ```

1. `package.json`에 `devDependencies` 추가된 내용 확인

    ```json
    "@typescript-eslint/eslint-plugin": "^6.16.0",
    "@typescript-eslint/parser": "^6.16.0",
    "eslint": "^8.56.0",
    "eslint-config-xo": "^0.43.1",
    "eslint-config-xo-typescript": "^1.0.1",
    "eslint-plugin-react": "^7.33.2",
    ```

1. `.eslintrc.js` 파일에 다음 세 줄을 추가

    ```js
      env: {
        ...,
        jest: true,
      },
      extends: [
        ...,
        'plugin:react/jsx-runtime',
      ],
      rules: {
        ...,
        'react/react-in-jsx-scope': 'off',
        },
    ```

1. `package.json`에 `"scripts"` 명령어 추가

    ```json
    "lint": "eslint --fix --ext .js,.jsx,.ts,.tsx .",
    ```

1. `.eslintignore` 파일을 작성한다. `.gitignore` 파일과 똑같이 작성해도 ok
1. lint 실행시켜보기

    ```node
    npm run lint
    ```

1. 저장할때마다 lint 실행되게 하기

    ```node
    mkdir .vscode
    touch .vscode/settings.json
    ```

    ```json
    {
      "editor.rulers": [
          80
      ],
      "editor.codeActionsOnSave": {
          "source.fixAll.eslint": true
      },
      "trailing-spaces.trimOnSave": true
    }
    ```

#### 5. Parcel

1. parcel을 설치한다.

    ```node
    npm i -D parcel
    ```

1. package.json에 명령어 추가

    ```json
    "start": "parcel --port 8080",
    "build": "parcel build",
    ```

1. `.gitignore`, `.eslintignore` 에 `.parcel-cache` 폴더 추가

1. `index.html` 파일 작성

    ```html
    <!DOCTYPE html>
    <html lang="ko">
    <head>
      <meta charset="UTF-8">
      <title>Sample</title>
    </head>
    <body>
      <div id="root"></div>
      <script type="module" src="./src/index.tsx"></script>
    </body>
    </html>
    ```

1. package.json 파일 수정

    ```json
    "main": "index.js", // 노드에서 실행할 경우
    =>
    "source": "index.html", // 웹서버에서 실행할 경우
    ```

1. 실행시켜보기

    ```node
    npm start
    ```

1. package.json 에 npm 단축 명령어 최종.json

    ```json
    "start": "parcel --port 8080",
    "build": "parcel build",
    "check": "tsc --noEmit",
    "lint": "eslint --fix --ext .js,.jsx,.ts,.tsx .",
    "test": "jest",
    "coverage": "jest --coverage --coverage-reporters html",
    "watch:test": "jest --watchAll"
    ```
