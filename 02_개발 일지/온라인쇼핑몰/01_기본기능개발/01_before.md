# 개발 하기 전

## 1. CheckList

- [] 용어정리
- [] 기능정리
- [] 화면정리
- [] api 기능 명세 확인
- [] 개발환경 세팅

## 2. 용어

- Product: 상품
  - Summary: 상품에 대한 요약 정보
  - Detail: 상품에 대한 상세 정보
  - Image: 상품 이미지
  - Option: 상품에 대한 상세 옵션 종류 (색상, 크기 등)
    - OptionItem: 옵션에 대한 상세 옵션 값 (옵션이 색상이라면 이건 Blue, Red 같은 걸 의미함)
- Category: 상품에 대한 분류
- Cart: 장바구니
  - LineItem: 장바구니에 담긴 것 (상품, 옵션, 수량 등을 동시에 다룸)
    - 여기서도 Option과 OptionItem을 사용한다.
    - 용어는 동일하지만 Product와 다른 구성을 갖기 때문에, 여기서는 Product와 Order라는 접두어를 활용한다.
    - 시스템을 분리할 수 있다면, 근본적으로 나누는 걸 추천(상품 정보 확인 / 장바구니 / 주문).
- Order: 주문
  - 여기서도 동일한 LineItem 활용.
- User: 사용자

## 3. 기능

1. 상품 목록 확인
2. 상품 상세 정보 확인
3. 장바구니에 상품 담기
4. 주문하기 → 배송지 입력, 결제
5. 주문 목록 확인
6. 주문 상세 확인
7. 로그인
8. 회원 가입

## 4. 화면

1. 홈 페이지 - `/`
2. 상품 목록 페이지 - `/products`
3. 상품 상세 페이지 - `/products/{id}`
4. 장바구니 페이지 - `/cart`
5. 주문 페이지 - `/order`
6. 주문 완료 페이지 - `/order/complete`
7. 주문 목록 페이지 - `/orders`
8. 주문 상세 페이지 - `/orders/{id}`
9. 로그인 페이지 - `/login`
10. 회원 가입 페이지 - `/signup`
11. 회원 가입 완료 페이지 - `/signup/complete`

## 5. REST API 명세

### 5.1. POST /session

로그인

Request

```json
{
  "email": "tester@example.com",
  "password": "password"
}
```

#### 5.1.2. Response

HTTP Status Code

| HTTP Status Code | 설명 |
| --- | --- |
| 201 Created | 로그인 성공 |
| 400 Bad Request | 로그인 실패 |

성공했을 때 Body (JSON)

```json
{
  "accessToken": "Header.Payload.Signature"
}
```

### 5.2. DELETE /session

Access Token 무효화.

### 5.3. POST /users

회원 가입.

Request

```json
{
  "email": "tester@example.com",
  "name": "테스터",
  "password": "password"
}
```

Response

HTTP Status Code

HTTP Status Code
설명
201 Created
회원 가입 성공
400 Bad Request
회원 정보가 잘못됨. (이메일 중복 등)
422 Unprocessable Content
회원 정보가 올바르지 않음.

성공했을 때 Body (JSON)

```json
{
  "accessToken": "Header.Payload.Signature"
}
```

### 5.4. GET /users/me

로그인한 회원 정보 얻기.

Response

HTTP Status Code

HTTP Status Code
설명
200 OK
Access Token이 올바름.
403 Forbidden
Access Token이 올바르지 않음.

성공했을 때 Body (JSON)

```json
{
  "id": "0BV000USR0001",
  "name": "테스터"
}
```

### 5.5. GET /categories

카테고리 목록을 얻는다.

Response

HTTP Status Code

```json
{
  "categories": [
    {
      "id": "0BV000CAT0001",
      "name": "top"
    },
    {
      "id": "0BV000CAT0002",
      "name": "outer"
    }
  ]
}
```

### 5.6. GET /products

상품 목록을 얻는다. 상품 목록에는 간소화된 정보만 포함된다.

특정 카테고리를 지정해서 해당 카테고리에 속한 상품 목록만 얻을 수도 있다.

Request

Query Parameters

항목
필수 여부
설명
categoryId
Optional
카테고리 ID

카테고리 ID를 지정하면 해당 카테고리에 속한 상품 목록을 돌려준다.

카테고리 ID를 지정하지 않으면 카테고리와 무관하게 모든 상품 목록을 돌려준다.

Response

```json
{
  "products": [
    {
      "id": "0BV000PRO0001",
      "category": {
        "id": "0BV000CAT0001",
        "name": "top"
      },
      "thumbnail": {
        "url": "https://example.com/products/01.jpg"
      },
      "name": "맨투맨",
      "price": 128000
    },
    {
      "id": "0BV000PRO0002",
      "category": {
        "id": "0BV000CAT0001",
        "name": "top"
      },
      "thumbnail": {
        "url": "https://example.com/products/02.jpg"
      },
      "name": "셔츠",
      "price": 118000
    }
  ]
}
```

### 5.7. GET /products/{id}

상품 상세 정보를 얻는다.

Response

```json
{
  "id": "0BV000PRO0001",
  "category": {
    "id": "0BV000CAT0001",
    "name": "top"
  },
  "images": [
    {
      "url": "https://example.com/products/01.jpg"
    }
  ],
  "name": "맨투맨",
  "price": 128000,
  "options": [
    {
      "id": "0BV000OPT0001",
      "name": "컬러",
      "items": [
        {
          "id": "0BV000ITEM001",
          "name": "black"
        },
        {
          "id": "0BV000ITEM002",
          "name": "white"
        }
      ]
    },
    {
      "id": "0BV000OPT0002",
      "name": "사이즈",
      "items": [
        {
          "id": "0BV000ITEM003",
          "name": "S"
        },
        {
          "id": "0BV000ITEM004",
          "name": "M"
        }
      ]
    }
  ],
  "description": "편하게 입을 수 있는 맨투맨"
}
```

### 5.8.GET /cart

장바구니 정보를 얻는다.

Response

```json
{
  "lineItems": [
    {
      "id": "0BV000CLI0001",
      "product": {
        "id": "0BV000PRO0001",
        "thumbnail": {
          "url": "https://example.com/products/01.jpg"
        },
        "name": "맨투맨"
      },
      "options": [
        {
          "name": "컬러",
          "item": {
            "name": "black"
          }
        },
        {
          "name": "사이즈",
          "item": {
            "name": "M"
          }
        }
      ],
      "unitPrice": 128000,
      "quantity": 2,
      "totalPrice": 256000
    }
  ],
  "totalPrice": 256000
}
```

### 5.9. POST /cart/line-items

장바구니에 상품을 담는다.

Request

```json
{
  "productId": "0BV000PRO0001",
  "options": [
    {
      "id": "0BV000OPT0001",
      "itemId": "0BV000ITEM001"
    },
    {
      "id": "0BV000OPT0002",
      "itemId": "0BV000ITEM004"
    }
  ],
  "quantity": 1
}
```

### 5.10. GET /orders

주문 목록을 얻는다. 주문 목록에서는 주문 간소화된 정보만 포함된다.

Response

```json
{
  "orders": [
    {
      "id": "0BV000ODR0001",
      "title": "맨투맨",
      "totalPrice": 256000,
      "status": "paid",
      "orderedAt": "2023-01-01 00:00:00"
    }
  ]
}
```

### 5.11. GET /orders/{id}

주문 상세 정보를 얻는다.

Response

```json
{
  "id": "0BV000ODR0001",
  "title": "맨투맨",
  "lineItems": [
    {
      "id": "0BV000OLI0001",
      "product": {
        "id": "0BV000PRO0001",
        "thumbnail": {
          "url": "https://example.com/products/01.jpg"
        },
        "name": "맨투맨"
      },
      "options": [
        {
          "name": "컬러",
          "item": {
            "name": "black"
          }
        },
        {
          "name": "사이즈",
          "item": {
            "name": "M"
          }
        }
      ],
      "unitPrice": 128000,
      "quantity": 2,
      "totalPrice": 256000
    }
  ],
  "totalPrice": 256000,
  "status": "paid",
  "orderedAt": "2023-01-01 00:00:00"
}
```

### 5.12. POST /orders

장바구니에 담긴 상품을 모두 주문한다.

Request

```json
{
  "receiver": {
    "name": "홍길동",
    "address1": "서울특별시 성동구 상원12길 34",
    "address2": "ㅇㅇㅇ호",
    "postalCode": "04790",
    "phoneNumber": "01012345678"
  },
  "payment": {
    "merchantId": "ORDER-20230101-00000001",
    "transactionId": "123456789012"
  }
}
```

## 6. 개발 환경 세팅

- [개발 환경 세팅하기 가이드](https://github.com/megaptera-kr/textbook/tree/main/start-megaptera-shop-client)
- [프로젝트 다운로드](https://drive.google.com/file/d/1ewCgoFt7ItXujopPbubgn_tdMRU7MXRj/view?usp=drive_link) [](https://drive.googlhttps://drive.google.com/drive/folders/1q43YrCnn1BRpYWqPyAeJOduA57WuJua4)(다운로드 받아서 그대로 사용하시면 됩니다)

### 6.1. 사용하는 라이브러리

1. [React Router](https://github.com/remix-run/react-router)
2. [styled-components](https://github.com/styled-components/styled-components)
3. [styled-reset](https://github.com/zacanger/styled-reset)
4. [usehooks-ts](https://github.com/juliencrn/usehooks-ts)
5. [Axios](https://github.com/axios/axios): REST API 사용을 위한 HTTP 클라이언트.
6. [tsyringe](https://github.com/microsoft/tsyringe)
7. [reflect-metadata](https://github.com/rbuckton/reflect-metadata)
8. [usestore-ts](https://github.com/seed2whale/usestore-ts)
9. [jest-dom](https://github.com/testing-library/jest-dom)
  : React Testing Library에서 활용할 수 있는 DOM 확인용 Matcher 모음.
  : test를 위한 함수의 이름이 어떤 동작을 하는지 의도를 더 잘 드러냄.
10. [MSW](https://github.com/mswjs/msw): mocking 하기 편리함

## 7. 개발 환경 세팅

### 7.1. E2E Test

CodeceptJS로 E2E 테스트 준비하고, 여기 있는 기능 테스트를 모두 통과시키는 걸 목표로 삼는다.

1. 상품 목록
    1. 모든 상품 보기
    2. 특정 카테고리의 상품 보기
2. 상품 상세
3. 장바구니
    1. 장바구니가 비어있는 경우
    2. 장바구니에 상품을 담은 경우
4. …

### 7.2. Styles

styles-components를 사용하기 위해 defaultTheme과 GlobalStyles를 준비.

기본 코드는 기존과 크게 다르지 않음.

### 7.3. Routes

React Router로 여러 페이지를 표현하기 위해 routes와 Layout을 준비.

기본 코드는 기존과 크게 다르지 않음.

### 7.4. Test Helper

테스트 코드에서 styled-components의 Theme과 React Router의 Link 등을 사용할 때 문제가 발생하지 않도록, React Testing Library의 render를 한번 감싼 테스트용 헬퍼 함수를 준비.

```tsx
import { render as originalRender } from '@testing-library/react';

import React from 'react';

import { MemoryRouter } from 'react-router-dom';

import { ThemeProvider } from 'styled-components';

import defaultTheme from './styles/defaultTheme';

export function render(element: React.ReactElement) {
  return originalRender((
    <MemoryRouter initialEntries={['/']}>
      <ThemeProvider theme={defaultTheme}>
        {element}
      </ThemeProvider>
    </MemoryRouter>
  ));
}
```

### 7.5. Types

기본적인 타입을 준비한다. 특별한 경우가 아니라면 미리 정한 용어집과 REST API 스펙에 맞추게 된다.

```tsx
export type Category = {
  id: string;
  name: string;
}

export type Image = {
  url: string;
}

export type ProductSummary = {
  id: string;
  category: Category;
  thumbnail: Image;
  name: string;
  price: number;
}

export type ProductOptionItem = {
  id: string;
  name: string;
};

export type ProductOption = {
  id: string;
  name: string;
  items: ProductOptionItem[];
};

export type ProductDetail = {
  id: string;
  category: Category;
  images: Image[];
  name: string;
  price: number;
  options: ProductOption[];
  description: string;
}

export type OrderOptionItem = {
  name: string;
};

export type OrderOption = {
  name: string;
  item: OrderOptionItem;
};

export type LineItem = {
  id: string;
  product: {
    id: string;
    name: string;
  };
  options: OrderOption[];
  unitPrice: number;
  quantity: number;
  totalPrice: number;
}

export type Cart = {
  lineItems: LineItem[];
  totalPrice: number;
}
```

### 7.6. MSW 세팅

REST API 스펙에 맞춰서 MSW 핸들러를 준비한다.

```tsx
import { rest } from 'msw';

import { ProductSummary } from '../types';

import fixtures from '../../fixtures';

const BASE_URL = 'https://shop-demo-api-01.fly.dev';

const productSummaries: ProductSummary[] = fixtures.products
  .map((product) => ({
    id: product.id,
    category: product.category,
    thumbnail: { url: product.images[0].url },
    name: product.name,
    price: product.price,
  }));

const handlers = [
  rest.get(`${BASE_URL}/categories`, (req, res, ctx) => (
    res(ctx.json({ categories: fixtures.categories }))
  )),
  rest.get(`${BASE_URL}/products`, (req, res, ctx) => (
    res(ctx.json({ products: productSummaries }))
  )),
  rest.get(`${BASE_URL}/products/:id`, (req, res, ctx) => {
    const product = fixtures.products.find((i) => i.id === req.params.id);
    if (!product) {
      return res(ctx.status(404));
    }
    return res(ctx.json(product));
  }),
  rest.get(`${BASE_URL}/cart`, (req, res, ctx) => (
    res(ctx.json(fixtures.cart))
  )),
  rest.post(`${BASE_URL}/cart/line-items`, (req, res, ctx) => (
    res(ctx.status(201))
  )),
];

export default handlers;
```
