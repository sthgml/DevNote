# Global Style & Theme

## 👉 [강의 보기-1]

## 👉 [강의 보기-2]

## 학습 키워드

- Reset CSS
- `box-sizing` 속성
- `word-break` 속성
- Theme
- ThemeProvider

### GlobalStyle

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

#### ThemeProvider
