# MSW

## 학습 키워드

- Service worker
- MSW(Mock Service Worker)
- polyfill(폴리필)

## 개념

1. Mock Service Worker 의 약자고요.

express보다 조금 불편함

원래는 Service Worker 라는 게 있거든요. 브라우저에서 쓸 수 있는.
요거는 Service Worker를 통해서, offline 일 때 쓰는 거, 뭐 그런 것들 지원할 때 많이 써요.
그 여러가지로 쓸 수 있는데, offline 이에요 그러면은, offline이라는 거는 인터넷이 연결이 안된 거죠.
그러면은 우리가 뭔가를 요청하면은 제대로 된 걸 얻을 수 없잖아요. 그쵸? 그런데 어떤 주소로 요청을 하면은
내가 중간에 가로채서, proxy라고 하죠? 그게 어떤 결과를 돌려 주게 하거나. 그런 거 만들 때 쓸 수가 있어요.

우리가 지금까지 했던 거는 코드 레벨에서 가로채거나 모킹하거나 한 거잖아요. 근데 그게 아니라, 네트워크 레벨을
실제로, 그냥 브라우저나, 아니면 우리 노드에서도 얘를 쓸 수 있게 되어있는데, 이 친구가 노드랑 둘 다 지원을 하거든요.
노드랑 이런 곳에서 네트워크 레벨에서 프록시를 이용해서 가짜로 막 해주는 거예요. 이거는.
원래는 오프라인 작업을 지원하기 위해서 많이 쓰이는 서비스 워커, 요거를 잘 활용한 거예요.
그래서 mock service worker 이렇게 되어있는 친구죠.

서빗 워커에 대해 궁그마시면 mdn을 읽어보시면 도움이 될 것 같구요. 꼭 보셔야 하는 것은 아니지만~ 예제도 있고 하니까 살펴보셔도 되고, 궁금하잖아요.
restAPI 어떻게 해주느냐. 이런 식으로 하세요 하고 이런식으로 post login하면 이렇게 결과 돌ㄹ려주면 되고, get user하면 

실제 잡아준 거 외에 node나 이런것에서 사용할 수 있거든요.

=> 오프라인, 즉 인터넷 연결 없이도 url을 사용해서 api로 통신을 하고, 응답을 받아올 수 있도록 해주는 도구.
=> 지금까지는 가짜 api를 만들고 가짜 url로 통신을 했지만, 진짜 url로 요청을 해도, 그걸 가로채서 가짜 응답을 보내줄 수 있게 한다~(는 의미인듯)

## 사용법

1. msw 패키지 설치

개발용으로 설치를 하면 devDependencies ! - 일반적인 package(소스코드)를 import할 때처럼 사용하면 typeError가 뜹니다.
그래서 mocks 안에다가 .eslintrc.js를 따로 만들어주거나,
// eslint-disable-next-line import/no-extraneous-dependencies
위의 주석을 문제의 코드 바로 위에 추가를 해주면 오류가 나지 않습니다.
더 좋은 건 파일을 따로 만들어주는 것임 (근데 어떻게 만들라는 건지 안알려줌)

```node
npm i -D msw
```

추가하는 게 있는데요. setup file의 내용이 여기에 없네요.
setupTests.js 를 검색해서 찾아보기!
beforeAll(()=>server.listen) test마다 서버를 리슨
끝날때마다 지워요
쓸때마다 넣을거라고 해서 이걸 추가해줍시다.

jestconfig 에 setupFilesAfterEnv키의 배열에 <rootDir>/src/setupTests.ts를 추가
setupTests.ts의 내용은?

- 서버를 얻고, 서버에서 ...
- (복붙): 핸들러가 없으면 빼먹었을 수 있으니까 error 표시하도록 해주고요.
- 핸들러라는 것을 잡아주거든요. 원래 문서에서는 핸들러를 먼저 잡아주고 이걸 해주는데 역으로 해보죠.
- 소스에 목스에 touch src/mocks/server.ts, handler.ts를 생성해주세요.
- 요청하는 주소가 어떻게 됐었죠? 
- localhost:3000/products였죠. 그 요청을 가로채보자.
- handlers.ts

```ts
// eslint-disable-next-line import/no-extraneous-dependencies
import { rest } from 'msw';

const handlers = [
  rest.get('http://localhost:3000/products', (req, res, ctx) => {
    // response로 리턴을 해줘요.
    const { products } = fixtures;

    return res(
      ctx.status(200),
      ctx.json({ products })
    );
  })
];

export default handlers;
```

express랑 비슷한데 express가 더 간단하죠.
렌더링을 한 다음에 페치를 해오는데, 로딩하는데 시간이 걸리는데 바로 체크를 하거든요. 시간 안에만 나오면 되게 하는 @testing-libarary/react 안에 있는 waitFor(함수 안에 기다린다. 될 때 까지 확인한다!)를 사용합시다. App.test.tsx에 가서 아래 내용을 추가하세요.

```tsx
test('App', asnyc () => {
  render(<App />);

  await waitFor(() => {
    screen.getByText('Apple!!!');
  })
});
```

useFetch에 Error 나면 빈 [] 을 넘겨주게 되어있는 걸 확인해봅시다.
fetch가 없대요. 최신 노드에는 fetch가 있어요. 여태까지는 mock에서 pass를 했기 때문에 됐는데 이제 안되는 거예요.
github에서 만든건데, fetch는 window에 있는 거라서 node에서 쓸 수 없는 건데, 그걸 처리해주 기 위해서 

```node
npm i -D whatwg-fetch
```

해준다.

## 목 서비스 워커를 사용하는 목적

- JEST 테스트 코드에서 jest.mock(""); / jest.mock("./hooks/useFetchProducts",()=> ()=> fixtures.products);
- 이제 더이상 jest.mock 필요 없다!
- 주소를 다르게 표현하고 싶을 때도. BASE_URL = process.env.API_BASE_URL이렇게 할 수도 있음!
- 본격까지는 아니지만 ㅈ금더 수준이 높은거다. api까지 나왔는데 spec이 구현되지 않은 경우, 간단해보여도 오래걸릴 수 있거든요. 그럼 백엔드 안나왔으니까 놀고 있냐가 아니고 이렇게 임시서버를 만들거면 express가 낫지만, 그냥 겸사겸사 작동하는 정도로는 msw를 만들어 좋은 선택임요.
- 하지만 어디까지나 흉내를 내는 거죠. 진짜 api가 구현되면 그것도 test를 해줘야 해요.
- E2E 테스트라고 하죠. End to End 의 줄임말인데, 테스트의 끝판왕이죠. 그걸 할 수 있는 도구가 바로 playwright다!

끝
