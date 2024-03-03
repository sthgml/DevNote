# 장바구니 보기

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

이제 지금까지 한걸 test로 확인해보자.

1. src/routes.test.tsx

    1. Unit Test
    1. path가 바뀌었을 때 컴포넌트를 잘 렌더해주나?

```tsx
describe('Router',()=>{

  // template
  context('', ()=>{
    it('', ()=>{
      render()

      screen.getByText()
      // or
      expect.toBe~~()
    }
  })

  context('when the current path is "/cart"', () => {
    it('renders the cart page', async () => {
      renderRouter('/cart');

      await waitFor(() => {
        screen.getByText('/CartView/');
      });
    });
  });
})
```

1. tests/features/cart_test.ts

E2E Test
backdoor라는 특이한 유틸이 보임

```ts
Feature('Cart');

Before(({ backdoor, I }) => {
  backdoor.setupDatabase();

  I.login();
});

Scenario('Empty cart', ({ I }) => {
  I.amOnPage('/cart');

  I.see('장바구니가 비었습니다');
});

Scenario('Add to cart', ({ I }) => {
  I.amOnPage('/products');

  I.click('CBCL 하트자수맨투맨');

  I.selectOption('컬러', 'blue');
  I.seeElement('//button[contains(., "+")]');

  I.click('장바구니에 담기');

  I.waitForText('장바구니에 담았습니다');

  I.amOnPage('/cart');

  I.see('CBCL 하트자수맨투맨\n(컬러: blue');
  I.see('합계\t128,000원');
});
```

backdoor.ts
이는 database를 초기화하는 util로써
유저에게 제공되는 기능은 아니지만, test 환경에서만
cart를 비운다든지 하는 함수가 필요할 때 쓰는 함수임.
예를 들어서 test에서 아이템이 없을 때 '장바구니가 비었습니다'가 뜨는지 확인할 때에 필요

이건 백엔드 개발자랑 약속을 하고 만들면 돼요. 이건 나만 쓸게 테스트 할 때!
실제 환경에서는 비공개정도가 아니라 실행이 안되어야 합니다.

```ts
const { I } = inject();

const BACKDOOR_BASE_URL = process.env.BACKDOOR_BASE_URL
                          || 'http://localhost:3000';

export = {
  setupDatabase() {
    I.amOnPage(`${BACKDOOR_BASE_URL}/setup-database`);
    I.see('OK');
  },
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

끝에 \ 는 여러줄일때

- create url -X : method
-H : header
--data : reqbody

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
