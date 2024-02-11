# 온라인 쇼핑몰 기본 기능 개발

## 학습 목표

이번주부터 쇼핑몰을 만들면서 지금까지 배웠던 모든 걸 종합해보는 시간을 갖습니다. 강의과 교재를 보며 그동안 놓친 부분이 있다면 데브노트에 스스로 정리해보세요. 강의를 그대로 따라서 쇼핑몰을 구축하는 것 또한 시간이 상당히 걸릴 겁니다.

## 용어

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

## 기능

1. 상품 목록 확인
2. 상품 상세 정보 확인
3. 장바구니에 상품 담기
4. 주문하기 → 배송지 입력, 결제
5. 주문 목록 확인
6. 주문 상세 확인
7. 로그인
8. 회원 가입

## 화면

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

## REST API

> [REST API](https://docs.google.com/document/d/1bGYl3IDoX53cNBbZHNlsRhPLZQ3Qiu-Jm3gpqyu_xI0/view)

## 개발 환경 세팅

- [개발 환경 세팅하기 가이드](https://github.com/megaptera-kr/textbook/tree/main/start-megaptera-shop-client)
- [프로젝트 다운로드](https://drive.google.com/file/d/1ewCgoFt7ItXujopPbubgn_tdMRU7MXRj/view?usp=drive_link) [](https://drive.googlhttps://drive.google.com/drive/folders/1q43YrCnn1BRpYWqPyAeJOduA57WuJua4)(다운로드 받아서 그대로 사용하시면 됩니다)

### 사용하는 라이브러리

1. [React Router](https://github.com/remix-run/react-router)
2. [styled-components](https://github.com/styled-components/styled-components)
3. [styled-reset](https://github.com/zacanger/styled-reset)
4. [usehooks-ts](https://github.com/juliencrn/usehooks-ts)
5. [Axios](https://github.com/axios/axios): REST API 사용을 위한 HTTP 클라이언트.
6. [tsyringe](https://github.com/microsoft/tsyringe)
7. [reflect-metadata](https://github.com/rbuckton/reflect-metadata)
8. [usestore-ts](https://github.com/seed2whale/usestore-ts)
9. [jest-dom](https://github.com/testing-library/jest-dom): React Testing Library에서 활용할 수 있는 DOM 확인용 Matcher 모음.
10. [MSW](https://github.com/mswjs/msw)

## E2E Test

CodeceptJS로 E2E 테스트 준비하고, 여기 있는 기능 테스트를 모두 통과시키는 걸 목표로 삼는다.

1. 상품 목록
    1. 모든 상품 보기
    2. 특정 카테고리의 상품 보기
2. 상품 상세
3. 장바구니
    1. 장바구니가 비어있는 경우
    2. 장바구니에 상품을 담은 경우
4. …

## Styles

styles-components를 사용하기 위해 defaultTheme과 GlobalStyles를 준비.

기본 코드는 기존과 크게 다르지 않음.

## Routes

React Router로 여러 페이지를 표현하기 위해 routes와 Layout을 준비.

기본 코드는 기존과 크게 다르지 않음.

## Test Helper

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

## Types

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

## MSW 세팅

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

## 상품 목록

상품 목록을 얻어서 표시하는 화면을 만들자. 말 그대로 다음과 같이 두 가지로 나눌 수 있다:

1. 상품 목록 얻기
2. 상품 목록 보여주기

전자는 useFetchProducts 훅으로, 후자는 Products 컴포넌트로 구현하고, ProductListPage에선 이 둘을 조합한다.

```tsx
import Products from '../components/product-list/Products';

import useFetchProducts from '../hooks/useFetchProducts';

export default function ProductListPage() {
  const { products } = useFetchProducts();

  return (
    <div>
      <h2>Products</h2>
      <Products products={products} />
    </div>
  );
}
```

일단 훅을 간단히 구현하고, Products 컴포넌트에 집중하자.

```tsx
const apiBaseUrl = 'https://shop-demo-api-01.fly.dev';

export default function useFetchProducts() {
  type Data = {
    products: ProductSummary[];
  };

  const { data } = useFetch<Data>(`${apiBaseUrl}/products`);

  return {
    products: data?.products ?? [],
  };
}
```

Products 컴포넌트를 만든다.

```tsx
const Container = styled.div`
  ul {
    display: flex;
    flex-wrap: wrap;
  }

  li {
    width: 20%;
    padding: 1rem;
  }

  a {
    display: block;
    text-decoration: none;
  }
`;

type ProductsProps = {
  products: ProductSummary[];
}

export default function Products({ products }: ProductsProps) {
  if (!products.length) {
    return null;
  }

  return (
    <Container>
      <ul>
        {products.map((product) => (
          <li key={product.id}>
            <Link to={`/products/${product.id}`}>
              <Product product={product} />
            </Link>
          </li>
        ))}
      </ul>
    </Container>
  );
}
```

Product 컴포넌트도 만든다.

```tsx
const Thumbnail = styled.img.attrs({
  alt: 'Thumbnail',
})`
  display: block;
  width: 100%;
  aspect-ratio: 1/1;
`;

type ProductProps = {
  product: ProductSummary;
}

export default function Product({ product }: ProductProps) {
  return (
    <div>
      <Thumbnail src={product.thumbnail.url} />
      <div>{product.name}</div>
      <div>
        {numberFormat(product.price)}
        원
      </div>
    </div>
  );
}
```

숫자를 읽기 좋게 보여주도록 numberFormat 유틸리티 함수를 준비한다.

```tsx
export default function numberFormat(value: number) {
  return new Intl.NumberFormat().format(value);
}
```

지금은 큰 의미가 없지만, 상품 목록을 Store로 관리할 수 있다.

```tsx
@singleton()
@Store()
export default class ProductsStore {
  products: ProductSummary[] = [];

  async fetchProducts() {
    this.setProducts([]);

    const { data } = await axios.get(`${apiBaseUrl}/products`);
    const { products } = data;

    this.setProducts(products);
  }

  @Action()
  setProducts(products: ProductSummary[]) {
    this.products = products;
  }
}
```

이제 useFetchProducts 훅을 변경한다.

```tsx
export default function useFetchProducts(): {
  products: ProductSummary[];
} {
  const store = container.resolve(ProductsStore);

  const [{ products }] = useStore(store);

  useEffectOnce(() => {
    store.fetchProducts();
  });	

  return { products };
}
```

## 카테고리 목록

헤더에 카테고리 목록을 보여주자.

```tsx
const Container = styled.header`
  margin-bottom: 2rem;

  h1 {
    font-size: 4rem;
  }

  nav {
    padding-block: 2rem;

    ul {
      display: flex;
    }

    li {
      margin-right: 2rem;
    }

    .active {
      color: ${(props) => props.theme.colors.primary};
    }
  }
`;

export default function Header() {
  const { categories } = useFetchCategories();

  return (
    <Container>
      <h1>Shop</h1>
      <nav>
        <ul>
          <li>
            <Link to="/">Home</Link>
          </li>
          <li>
            <Link to="/products">Products</Link>
            {!!categories.length && (
              <ul>
                {categories.map((category) => (
                  <li key={category.id}>
                    <Link to={`/products?categoryId=${category.id}`}>
                      {category.name}
                    </Link>
                  </li>
                ))}
              </ul>
            )}
          </li>
          <li>
            <Link to="/cart">Cart</Link>
          </li>
        </ul>
      </nav>
    </Container>
  );
}
```

바로 Store를 준비한다.

```tsx
@singleton()
@Store()
export default class CategoriesStore {
  categories: Category[] = [];

  async fetchCategories() {
    this.setCategories([]);

    const categories = await apiService.fetchCategories();

    this.setCategories(categories);
  }

  @Action()
  setCategories(categories: Category[]) {
    this.categories = categories;
  }
}
```

API 호출을 모아주는 ApiService를 만든다. API의 base URL을 지정하기 위해 환경변수를 활용한다.

```tsx
const API_BASE_URL = process.env.API_BASE_URL
                     || 'https://shop-demo-api-01.fly.dev';

export default class ApiService {
  private instance = axios.create({
    baseURL: API_BASE_URL,
  });

  async fetchCategories(): Promise<Category[]> {
    const { data } = await this.instance.get('/categories');
    const { categories } = data;
    return categories;
  }

  async fetchProducts(): Promise<ProductSummary[]> {
    const { data } = await this.instance.get('/products');
    const { products } = data;
    return products;
  }
}

export const apiService = new ApiService();
```

마지막으로, useFetchCategories 훅을 만든다.

```tsx
export default function useFetchCategories() {
  const store = container.resolve(CategoriesStore);

  const [{ categories }] = useStore(store);

  useEffectOnce(() => {
    store.fetchCategories();
  });

  return { categories };
}
```

## 카테고리별 상품 목록

ProductListPage 컴포넌트에서 categoryId를 얻는다.

```tsx
export default function ProductListPage() {
  const [params] = useSearchParams();

  const categoryId = params.get('categoryId') ?? undefined;

  const { products } = useFetchProducts({ categoryId });

  return (
    <div>
      <h2>Products</h2>
      <Products products={products} />
    </div>
  );
}
```

카테고리 ID를 쓰도록 훅을 변경.

```tsx
export default function useFetchProducts({ categoryId }: {
  categoryId: string;
}): {
  products: ProductSummary[];
} {
  const store = container.resolve(ProductsStore);

  const [{ products }] = useStore(store);

  useEffect(() => {
    store.fetchProducts({ categoryId });
  }, [store, categoryId]);

  return { products };
}
```

Store도 변경.

```tsx
async fetchProducts({ categoryId }: {
  categoryId?: string;
}) {
  this.setProducts([]);

  const products = await apiService.fetchProducts({ categoryId });

  this.setProducts(products);
}
```

API Service도 변경.

```tsx
async fetchProducts({ categoryId }: {
  categoryId?: string;
} = {}): Promise<ProductSummary[]> {
  const { data } = await this.instance.get('/products', {
    params: { categoryId },
  });
  const { products } = data;
  return products;
}
```

사실 강의를 준비할 때는 처음부터 이렇게 만들기는 했다. 처음부터 고민해서 바로 만들어도 되고, 일단 만들고 이렇게 고쳐나가도 된다. 테스트 코드가 있으면 이런 변경 작업을 할 때 더 자신감을 얻을 수 있다.

## 상품 상세

상품 상세 정보를 얻어서 보여주는 페이지를 준비한다. 여기서는 단순하게 처리하기 위해, 상품을 찾을 수 없는 경우를 따로 구분해서 표현하지 않고 그냥 일반 에러로 표시한다(당연히 구분해주는 게 더 좋다).

```tsx
export default function ProductDetailPage() {
  const params = useParams();

  const { loading, error } = useFetchProduct({
    productId: String(params.id),
  });

  if (loading) {
    return (
      <p>Loading...</p>
    );
  }

  if (error) {
    return (
      <p>Error!</p>
    );
  }

  return (
    <ProductDetail />
  );
}
```

장바구니 담기 기능 때문에 prop drilling 문제가 발생할 수 있어서, Page에서 product를 내려주지 않게 했다. ProductDetail 컴포넌트에서 product만 얻어서 활용하자.

```tsx
const Container = styled.div`
  display: flex;
  justify-content: space-between;

  aside {
    width: 38%;
  }

  article {
    width: 60%;
  }
`;

export default function ProductDetailView() {
  const [{ product }] = useProductDetailStore();

  return (
    <Container>
      <aside>
        <Images images={product.images} />
      </aside>
      <article>
        <h2>{product.name}</h2>
        <AddToCartForm />
        <Description value={product.description} />
      </article>
    </Container>
  );
}
```

Fetch 작업으로 준비가 된 Store를 활용하기 위해 useProductDetailStore 훅을 만든다.

```tsx
export default function useProductDetailStore() {
  const store = container.resolve(ProductDetailStore);
  return useStore(store);
}
```

ProductDetailStore를 만든다.

```tsx
@singleton()
@Store()
export default class ProductDetailStore {
  product: ProductDetail = nullProductDetail;

  loading = true;

  error = false;

  async fetchProduct({ productId }: {
    productId: string;
  }) {
    this.startLoading();

    try {
      const product = await apiService.fetchProduct({ productId });
      this.setProduct(product);
    } catch {
      this.setError();
    }
  }

  @Action()
  private startLoading() {
    this.product = nullProductDetail;
    this.loading = true;
    this.error = false;
  }

  @Action()
  private setProduct(product: ProductDetail) {
    this.product = product;
    this.loading = false;
    this.error = false;
  }

  @Action()
  private setError() {
    this.product = nullProductDetail;
    this.loading = false;
    this.error = true;
  }
}
```

적당한 Null Object도 만든다([참고](https://refactoring.com/catalog/introduceSpecialCase.html)).

```tsx
export const nullProductDetail: ProductDetail = {
  id: '',
  category: { id: '', name: '' },
  images: [],
  name: '',
  price: 0,
  options: [],
  description: '',
};
```

이제 useFetchProduct 훅을 만들 수 있다.

```tsx
export default function useFetchProduct({ productId }: {
  productId: string;
}): {
  loading: boolean;
  error: boolean;
} {
  const [{ loading, error }, productDetailStore] = useProductDetailStore();

  useEffect(() => {
    productDetailStore.fetchProduct({ productId });
  }, [productDetailStore, productId]);

  return { loading, error };
}
```

Images 컴포넌트를 만든다.

```tsx
const Thumbnail = styled.img.attrs({
  alt: 'Product Image',
})`
  display: block;
  width: 100%;
  aspect-ratio: 1/1;
`;

type ImagesProps = {
  images: Image[];
}

export default function Images({ images }: ImagesProps) {
  const [image] = images;

  if (!image) {
    return null;
  }

  return (
    <Thumbnail src={image.url} />
  );
}
```

Description를 만든다. 임의로 key를 잡아주기 위해 꼼수를 사용했다.

```tsx
function key(value: string, index: number) {
  return `${index}-${value}`;
}

const Container = styled.div`
  li {
    min-height: 1rem;
    line-height: 1.4;
  }
`;

type DescriptionProps = {
  value: string;
}

export default function Description({ value }: DescriptionProps) {
  if (!value.trim()) {
    return null;
  }

  const lines = value.split('\n');

  return (
    <Container>
      <ul>
        {lines.map((line, index) => (
          <li key={key(line, index)}>
            {line}
          </li>
        ))}
      </ul>
    </Container>
  );
}
```

## 장바구니 보기

장바구니에 상품 담기 기능을 만들기 전에, 비교적 쉬운 장바구니 보기 작업을 먼저 끝내보자.

```tsx
export default function CartPage() {
  const { cart } = useFetchCart();

  if (!cart) {
    return null;
  }

  return (
    <div>
      <h2>장바구니</h2>
      <CartView cart={cart} />
    </div>
  );
}
```

Hook을 만든다.

```tsx
export default function useFetchCart() {
  const store = container.resolve(CartStore);

  const [{ cart }] = useStore(store);

  useEffectOnce(() => {
    store.fetchCart();
  });

  return { cart };
}
```

Store도 만든다.

```tsx
@singleton()
@Store()
export default class CartStore {
  cart: Cart | null = null;

  async fetchCart() {
    this.setCart(null);

    const cart = await apiService.fetchCart();

    this.setCart(cart);
  }

  @Action()
  setCart(cart: Cart | null) {
    this.cart = cart;
  }
}
```

여기서는 그냥 null을 썼는데, ProductDetail처럼 Null Object를 만들어서 쓰면 더 좋다.

API Service에 fetchCart 추가.

```tsx
async fetchCart(): Promise<Cart> {
  const { data } = await this.instance.get('/cart');
  return data;
}
```

다시 컴포넌트로 돌아와서 보면, Cart 타입과 Cart 컴포넌트의 이름이 겹치는 문제가 있다. 이 문제에 대한 쉬운 해법으로는 다음 두 가지를 고려할 수 있다:

1. Cart 타입을 가져올 때 as CartType을 써서 타입의 이름을 바꾼다.
2. Cart 컴포넌트를 CartView 등 다른 이름으로 바꾼다.

여기서는 컴포넌트 이름을 바꿔서 만들어 보자.

```tsx
const Container = styled.div`
  table {
    width: 100%;
  }

  th, td {
    padding: .5rem;
    text-align: left;
  }
`;

type CartViewProps = {
  cart: Cart;
};

export default function CartView({ cart }: CartViewProps) {
  if (!cart.lineItems.length) {
    return (
      <p>장바구니가 비었습니다</p>
    );
  }

  return (
    <Container>
      <table>
        <thead>
          <tr>
            <th>제품</th>
            <th>단가</th>
            <th>수량</th>
            <th>금액</th>
          </tr>
        </thead>
        <tbody>
          {cart.lineItems.map((lineItem) => (
            <LineItemView
              key={lineItem.id}
              lineItem={lineItem}
            />
          ))}
        </tbody>
        <tfoot>
          <tr>
            <th colSpan={3}>
              합계
            </th>
            <td>
              {numberFormat(cart.totalPrice)}
              원
            </td>
          </tr>
        </tfoot>
      </table>
    </Container>
  );
}
```

LineItem도 마찬가지로 LineItemView란 컴포넌트로 만든다.

```tsx
type LineItemViewProps = {
  lineItem: LineItem;
};

export default function LineItemView({ lineItem }: LineItemViewProps) {
  return (
    <tr>
      <td>
        <Link to={`/products/${lineItem.product.id}`}>
          {lineItem.product.name}
        </Link>
        <Options options={lineItem.options} />
      </td>
      <td>
        {numberFormat(lineItem.unitPrice)}
        원
      </td>
      <td>{lineItem.quantity}</td>
      <td>
        {numberFormat(lineItem.totalPrice)}
        원
      </td>
    </tr>
  );
}
```

Options 컴포넌트는 그냥 이 이름 그대로 가도 될 것 같다.

```tsx
const Container = styled.div`
  margin-top: .5rem;
  font-size: 1.4rem;
`;

type OptionsProps = {
  options: OrderOption[];
}

export default function Options({ options }: OptionsProps) {
  if (!options.length) {
    return null;
  }

  const text = options
    .map((option) => `${option.name}: ${option.item.name}`)
    .join(', ');

  return (
    <Container>
      (
      {text}
      )
    </Container>
  );
}
```

cURL을 이용해서 임의로 장바구니에 상품 담기

```bash
curl -X POST https://shop-demo-api-01.fly.dev/cart/line-items \
  -H "Content-Type: application/json" \
  --data '
    {
      "productId": "0BV000PRO0001",
      "options": [
        {
          "id": "0BV000OPT0001",
          "itemId": "0BV000ITEM001"
        },
        {
          "id": "0BV000OPT0002",
          "itemId": "0BV000ITEM005"
        }
      ],
      "quantity": 1
    }
  '
```

## 장바구니에 상품 담기

장바구니에 상품을 담는다는 게 어떤 의미일까? 정확히는 Product가 Cart로 들어가는 게 아니라, Product와 관련된 Option 정보, 수량 등 다양한 값이 조합돼 Cart의 Line Item을 구성하는 게 “장바구니에 상품을 담는다”는 말의 진짜 의미다.

실제로는 조금 복잡한 도메인 로직이 들어갈 수 있는데, 이런 처리는 백엔드에서 담당하기로 하고, 여기서는 상품과 관련된 옵션, 수량 등을 컨트롤하는데 집중해 보자.

AddToCartForm 컴포넌트에선 다음과 같은 요소를 포함한다:

1. 옵션을 보여주고, 선택할 수 있게 한다.
2. 수량을 정하게 한다. (기본값: 1)
3. 수량에 맞는 비용을 보여준다.
4. 장바구니에 담기 버튼이 있고, 이걸 누르면 장바구니에 담았다는 메시지로 바뀐다.

컴포넌트를 만들자.

```tsx
export default function AddToCartForm() {
  return (
    <div>
      <Options />
      <Quantity />
      <Price />
      <SubmitButton />
    </div>
  );
}
```

Prop Drilling을 피하기 위해 전부 개별 컴포넌트에서 Store를 가져다 쓰게 했다.

제일 쉬운 Quantity 컴포넌트부터 시작하자.

```tsx
export default function Quantity() {
  const [{ quantity }, store] = useProductFormStore();

  const handleClickDecrease = () => {
    store.changeQuantity(quantity - 1);
  };

  const handleClickIncrease = () => {
    store.changeQuantity(quantity + 1);
  };

  return (
    <Container>
      <Button onClick={handleClickDecrease}>
        -
      </Button>
      <input type="text" value={quantity} readOnly />
      <Button onClick={handleClickIncrease}>
        +
      </Button>
    </Container>
  );
}
```

공통으로 사용할 Button 컴포넌트를 간단히 만든다. 참고로, 이 디자인은 끔찍하다. 😆

```tsx
import styled from 'styled-components';

const Button = styled.button.attrs({
  type: 'button',
})`
  border: .1rem solid #888;
  background: transparent;
  color: ${(props) => props.theme.colors.primary};
  cursor: pointer;
`;

export default Button;
```

Hook을 만들자.

```tsx
export default function useProductFormStore() {
  const store = container.resolve(ProductFormStore);
  return useStore(store);
}
```

Store도 만들자.

```tsx
@singleton()
@Store()
export default class ProductFormStore {
  quantity = 1;

  @Action()
  changeQuantity(quantity: number) {
    if (quantity <= 0) {
      return;
    }
    if (quantity > 10) {
      return;
    }
    this.quantity = quantity;
  }
}
```

사소한 비즈니스 로직이지만, 테스트 코드를 통해 검증하자.

```tsx
describe('ProductFormStore', () => {
  let store: ProductFormStore;

  beforeEach(() => {
    store = new ProductFormStore();
  });

  describe('changeQuantity', () => {
    context('with correct value', () => {
      it('changes quantity', () => {
        store.changeQuantity(3);

        expect(store.quantity).toBe(3);
      });
    });

    context('with incorrect value', () => {
      it("doesn't changes quantity", () => {
        store.changeQuantity(-1);
        store.changeQuantity(11);

        expect(store.quantity).toBe(1);
      });
    });
  });
});
```

금액을 계산해 보자.

```tsx
export default function Price() {
  const [{ product }] = useProductDetailStore();
  const [{ quantity }] = useProductFormStore();

  return (
    <Container>
      {numberFormat(product.price * quantity)}
      원
    </Container>
  );
}
```

만약 ProductFormStore에 수량에 따른 금액을 계산하는 메서드 또는 Getter가 있다면 다른 형태로 접근할 수도 있다.

```tsx
export default function Price() {
  const [{ product }] = useProductDetailStore();
  const [{ price }, productFormStore] = useProductFormStore();

  // TODO: product 변경에 따른 setProduct 호출은 여기가 아니라 page 등에서 처리할 것!
  useEffect(() => {
    productFormStore.setProduct(product);
  }, [productFormStore, product]);

  return (
    <Container>
      {numberFormat(price)}
      원
    </Container>
  );
}
```

SubmitButton도 간단히 준비하자.

```tsx
export default function SubmitButton() {
  const [{ done }, store] = useProductFormStore();

  const handleClick = () => {
    store.addToCart();
  };

  if (done) {
    return (
      <p>장바구니에 담았습니다</p>
    );
  }

  return (
    <Button onClick={handleClick}>
      장바구니에 담기
    </Button>
  );
}
```

Store에 addToCart를 추가한다.

```tsx
async addToCart() {
  this.resetDone();

  await apiService.addProductToCart({
    productId: this.productId,
    options: this.options.map((option, index) => ({
      id: option.id,
      itemId: this.selectedOptionItems[index].id,
    })),
    quantity: this.quantity,
  });

  this.complete();
}
```

장바구니에 상품을 담기 위해 관리해야 할 여러 상태가 필요하다. 이와 관련된 코드를 마저 넣어주자.

```tsx
@singleton()
@Store()
export default class ProductFormStore {
  productId = '';

  options: ProductOption[] = [];

  selectedOptionItems: ProductOptionItem[] = [];

  quantity = 1;

  done = false;

  async addToCart() {
    // …(중략)…
  }

  @Action()
  setProduct(product: ProductDetail) {
    this.productId = product.id;
    this.options = product.options;
    this.selectedOptionItems = this.options.map((i) => i.items[0]);
    this.quantity = 1;
    this.done = false;
  }

  @Action()
  changeQuantity(quantity: number) {
    // …(중략)…
  }

  @Action()
  resetDone() {
    this.done = false;
  }

  @Action()
  complete() {
    this.quantity = 1;
    this.done = true;
  }
}
```

API Service에 addProductToCart 추가.

```tsx
async addProductToCart({ productId, options, quantity }: {
  productId: string;
  options: {
    id: string;
    itemId: string;
  }[];
  quantity: number;
}): Promise<void> {
  await this.instance.post('/cart/line-items', {
    productId, options, quantity,
  });
}
```

거의 다 왔다. Options 컴포넌트를 만든다.

```tsx
export default function Options() {
  const [{ options, selectedOptionItems }, store] = useProductFormStore();

  const handleChange: ChangeFunction = ({ optionId, optionItemId }) => {
    store.changeOptionItem({ optionId, optionItemId });
  };

  return (
    <div>
      {options.map((option, index) => (
        <Option
          key={option.id}
          option={option}
          selectedItem={selectedOptionItems[index]}
          onChange={handleChange}
        />
      ))}
    </div>
  );
}
```

Option 컴포넌트를 만든다.

```tsx
type OptionProps = {
  option: ProductOption;
  selectedItem: ProductOptionItem;
  onChange: ChangeFunction;
}

export default function Option({
  option, selectedItem, onChange,
}: OptionProps) {
  const handleChange = (item: ProductOptionItem | null) => {
    if (!item) {
      return;
    }

    onChange({
      optionId: option.id,
      optionItemId: item.id,
    });
  };

  return (
    <ComboBox
      label={option.name}
      selectedItem={selectedItem}
      items={option.items}
      itemToId={(item) => item.id}
      itemToText={(item) => item.name}
      onChange={handleChange}
    />
  );
}
```

범용 ComboBox 컴포넌트도 추가한다.

```tsx
const Container = styled.div`
  label {
    margin-right: .5rem;
  }
`;

type ComboBoxProps<T> = {
  label: string;
  selectedItem: T;
  items: T[];
  itemToId: (item: T) => string;
  itemToText: (item: T) => string;
  onChange: (item: T | null) => void;
}

export default function ComboBox<T>({
  label, selectedItem, items, itemToId, itemToText, onChange,
}: ComboBoxProps<T>) {
  const id = useRef(`combobox-${Math.random().toString().slice(2)}`);

  const handleChange = (event: React.ChangeEvent<HTMLSelectElement>) => {
    const { value } = event.target;
    const selected = items.find((item) => itemToId(item) === value);
    onChange(selected ?? null);
  };

  return (
    <Container>
      <label htmlFor={id.current}>
        {label}
      </label>
      <select
        id={id.current}
        onChange={handleChange}
        value={itemToId(selectedItem)}
      >
        {items.map((item) => (
          <option key={itemToId(item)} value={itemToId(item)}>
            {itemToText(item)}
          </option>
        ))}
      </select>
    </Container>
  );
}
```

이제 Store에 changeOptionItem만 추가하면 끝난다.

```tsx
@Action()
changeOptionItem({ optionId, optionItemId }: {
  optionId: string;
  optionItemId: string;
}) {
  this.selectedOptionItems = this.product.options.map((option, index) => {
    const item = this.selectedOptionItems[index];
    return option.id !== optionId
      ? item
      : option.items.find((i) => i.id === optionItemId) ?? item;
  });
}
```

- [Array를 Immutable하게 변경하기](https://github.com/ahastudio/til/blob/main/javascript/immutable-array.md)
