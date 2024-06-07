# Router

## 학습 키워드

- ReactRouter - RouterProvider

## 객체를 활용해서 좀 더 깔끔하게 라우터를 만드는 방법

사용 이유: SOC 가능

- App: UI
- Layout
- Routing
  - routes: 라우팅의 정보

App.tsx

```tsx
  const router = createRouter(routes);
  ...
  return <RouterProvider router={router}>
```

routes.ts

```ts
  const routes = [
    {
      element: <Layout />,
      children: [ // == 작은 routes
        {
          path: '/',
          element: <HomePage />
        }, {
          path: '/about',
          element: <AboutPage />
        } // ... routes
      ]
    }
  ]
```

Layout.tsx

```tsx
function Layout() {
  return (
    <Header />
    <Outlet />
    <Footer />
  )
}
```

### 테스트 코드

createMemoryRouter() 와 <RouterProvider /> 를 활용해서 rednerRouter함수 만들기

```tsx
function renderRouter = () => {
  const router = createMemoryRouter(routes, {initialEntries:['/']}); 
  render(<RouterProvider router={router}>)
}
```
