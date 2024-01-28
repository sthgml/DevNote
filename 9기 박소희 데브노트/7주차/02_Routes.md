# Routes

## 학습 키워드

- 라우터란?
- React Router
  - Browser Router
  - Route
  - Memory Router

### 라우터란?

원시적으로 구현했던 방식을 react-router-dom으로 구현하는 것

```js
<>
  <Routes>
    <Routes path='/' element={}>
  </Routes>
</>
```APP.tsx

에서 현재 path랑 Route의 path props를 비교해야 하는데 어떻게 비교하는 걸까?
이 컴포넌트의 상위에 BrowserRouter를 감싸줘야 함!

```js
render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
)
```index.tsx

이런 식으로!

test코드에서는 어떻게 해야 될까?
테스트코드는 브라우저에서 돌아가는 것이 아니고 메모리에서 돌아가는 건데 url이 바뀌는 건 브라우저에서
제공하는 것이기 때문에 메모리용 라우터로 동작을 구현해줘야함.
마찬가지로 render할 때 MemoryRouter로 감싸면 됨

```jsx
import MemoryRouter from 'react-router-dom';
...
render(
  <MemoryRouter initialEntries={['/']}>
    <App/>
  </MemoryRouter>
)
```
