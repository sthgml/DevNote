# Global Style & Theme

## 학습 키워드

- Reset CSS
- `box-sizing` 속성
- `word-break` 속성
- Theme
- ThemeProvider

## GlobalStyle

npm i styled-reset

import {Reset} from 'styled-reset';

최상위 컴포넌트에 씨우기

```jsx
render(<Reset>
  <App />
</Reset>)
```

``` jsx
import { createGlobalStyle } from 'styled-components';
const GlobalStyle = createGlobalStyle`
  html {
    font-size: 62.5%;
  }
  * {
    font: inherit;
  }
`
export default GlobalStyle;
```

## ThemeProvider

styled-components의 빛!
styled-components를 만들 때 전달해주던 props를 매 번 전달해주지 않아도
어디서든 동일한 props를 사용할 수 있도록 함

== 디자인시스템의 근간

변수 네이밍 주의사항

- style 자체가 아닌 이 style 이 디자인 시스템 내에서 하는 역할을 기준으로 네이밍
  - ex. color {background, primary, secondary..}
  - ex. font-size {header, desc, warnMsg ...}

### 타입 잡기

```ts
const Theme = {
  color {
    background: '#fff',
    primary: '#00f',
  }
}
// ... not
type Theme = {
  color {
    background: string;
    primary; 'string;
  }
}
// ... rather
type Theme = typeof theme;
```

### 사용법

1. 최상단(App.tsx)에서 감싸기

    ```ts
    import defaultTheme from '...//...';
    import useDarkMode from 'usehooks-ts';
    // ...
    const {isDarkMode, toggle: toggleDarkMode} = useDarkMode();
    const theme = isDarkMode? darkTheme: defaultTheme;
    // ...
    <ThemeProvider theme={theme}>
    {otherComponents}
      <Button onClick={toggleDarkmode} active={isDarkMode}>
    </ThemeProvider>
    ```

1. styled.d.ts 에서 타입 지정해주기

    그동안 '@types/~~' 이름으로 import 한 패키지들이 이런 이름의 파일에 타입을 지정한 것!

    ```ts
    import 'styled-components';
    import Theme from '../' // 위에서 만든 타입 임포트!

    declare module 'styled-components' {
      export interface DefaultTheme extends Theme {}
    }
    ```

    효과 : 자동완성, 오타 등을 미리 검열해주어서 프로젝트의 안정성을 높임 === 정적 프로그래밍의 장점
