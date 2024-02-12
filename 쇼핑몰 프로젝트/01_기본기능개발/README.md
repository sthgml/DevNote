# 온라인 쇼핑몰 기본 기능 개발

## 0. 개발 환경 세팅

### 01. 개발 세팅

#### 001. E2E TEST

1. 정의: End 2(to) End Test
    1. application의 흐름을 처음부터 끝까지 테스트 하는 것
1. 필요성:
    1. 유닛 테스트나 통합 테스트(JEST)는 '모듈'의 무결성을 증명
    1. but '모듈'의 무결성 !== 'app'의 무결성
    1. 실제 사용자의 시나리오를 테스트
1. 주의할 점:
    1. 테스트 과정이 길고
    1. 경우의 수가 매우 많음
    1. == 비용이 많이 든다.
    1. ==> 꼭 필요한 TEST만 추려서 전체 테스트안에서 비중을 10% 정도로 조절
1. 걸림돌:
    1. 유닛, 통합 == 개발자의 의도 테스트
    1. E2E == 사용자 동작 테스트
    1. == QA 팀 업무와 중복
    1. 코드가 길고 시간 많이 듦
    1. == 이후 유지 보수에서 후순위가 될 가능성이 높음
    1. 억지로 (husky, github action) E2E Test를 통과한 경우에만 merge 될수 있게 설정
    1. == 의미 퇴색, 시간만 잡아먹는 과정

1. CodeceptJS : 인간 친화적 TEST 도구
    1. npm codeceptjs init
    1. codeceptjs.conf.ts 생성된 파일 확인
    1. tests/~~_test.ts 파일 생성

#### 002. Styles

1. defaultTheme 정의
    1. const defaultTheme = {...}
1. type Theme 정의
    1. type Theme = typeof defaultTheme
    1. defaultTheme에서 정의하는 key의 개수가 변할 수 있음 => 그 때마다 두 군데에서 type을 수정하는 것이 아닌, default 설정만 해주면 정의된 key에 따라 type을 따올 수 있음.
1. styles.d.ts 작성, interface DefaultTheme 내보내기
    1. import styled-component
    1. module declare interface DefaultTheme extends Theme {}
1. GlobalStyles.ts 작성
    1. import createGlobalStyles...;
    1. const GlobalStyles = createGlobalStyles`
    ... css 처럼 스타일 정의`
1. main.tsx 에서 사용하기
    1. 혹은 App.tsx

    ```tsx
    render((<ThemeProvider theme={defaultTheme}>
      <Reset />
      <GlobalStyles />
      <RouterProvider router={router}/>
    </ThemeProvider>));
    ```

#### 003. routes 객체를 활용한 routing

1. Layout.tsx 작성
1. routes.ts 작성
1. main.ts 에서 사용
1. main.test.ts 에서 사용

#### 004. TestHelper

1. 기능 및 역할
    1. '@testing-library/react'의 render 덮어쓰기
    1. render 하면서 ThemeProvider, MemoryRouter 등의 세팅을 함께 하기 위함
1. 사용법

    ```tsx
    export function render(element: React.Element) {
      return originalRender(
        <MemoryRouter initialEntries={['/']}>
          <ThemeProvider theme={defaultTheme}>
            {element}
          </ThemeProvider>
        </MemoryRouter>
      )
    }
    ```

#### 005. Types

1. 기능 및 역할
    1. 용어 정리, api 스펙을 기준으로 작성
    1. BE가 이미 잘 정리되어 있거나, BE와 소통이 원활하다는 전제

#### 006. MSW (Mock Service Worker)

1. 기능 및 역할
    1. api 통신 사용하기 전에
    1. 외부로 보내는 요청을 가로채고 관찰하여, 가짜 데이터를 반환해줄수 있음
1. 사용법

    1. 'mocks/server.ts', 'mocks/handler.ts'
        1. fixtures.categories 를 respond 에 담아 보내기

        ```ts
        const handlers = [
          rest.get(`${BASE_URL}/categories`,(req, res, ctx) => (
            res(ctx.json({categories: fixtures.categories}))
          )),
          rest.get(...),
          ...
        ]
        ```

    1. 'fixtures/...'
        1. 영단어 의미 : 고정물
            1. 사용되는 객체들의 고정된 상태
            1. 결과를 반복 가능하도록,
            1. 고정된 환경에서 테스트 할 수 있음을 보장
        1. index.ts에서 다른 객체들도 내보내기

        ```tsx
          import categories from './categories';
          import products from './products';

          export {
            categories,
            products,
            ...
          }
        ```

## 07. 레퍼런스

[E2E 테스트 도입 경험기](https://fe-developers.kakaoent.com/2023/230209-e2e/)