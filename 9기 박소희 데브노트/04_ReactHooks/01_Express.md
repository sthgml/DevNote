# Express

## 학습 키워드

- Express 란
- URL 구조
- REST API
- HTTP Method(CRUD)

여러모로 저희가 완전히 백엔드에 대한 이해 없이 프론트만 작업하는 건 불가능ㅎ ㅏ구요 Test에서도 이런 ㅂ분을 모킹을 한다거나 하기 때문에 잏가 필요합니다

Express는 TJfㅏ는 분이 만드셨고, 그 분은 더이상 개발을 아나고 계시지만 다른 분들이 ㅏㄷ아서 쓰고 있죠. Connect는 HTtp의 기본 모듈을 감싼거고 express는 그걸 다시 한 번 더 감싼 겁니다.

NExt, 외의 다른 Framework들도 어쨋든 간의 거의 표준적인 Nodejsfㅗ 뭔가를 만든다고 하면 Express를 기본적으로 사용한다고 생각하시면 돼요. 그리고 굉장히 오래됐고, 한국어로도 문서들이 있고요.

일단은 간단한 서버의 npm 패키지를 만들어 볼게요. 시작하기 에서 설치하기 누르면 나오는 가이드가 있지만 저희는 ts 쓸거기 때문에 차이점이 조금 잇어서 교재에 추가된게 좀 있어요.

결국 새로운 프로젝트를 만들어줘야 해요. mkdir express-demo-app > cd mk~~ 처음부터 .gitignore파일을 만들어주면 좋기 때문에 ㅎㅎ echo는 화면에 보여주는 걸 이야기 해요. echo "/node_modules/"라고 하면 터미널에 내용을 띄워주고, 파이프라인을 파일로 설정을 해주면 해당 파일에 이 내용이 들어가게 돼요. 파일에 직접 써주셔도 되지만, 터미널에서 작업 끝내고 싶은 분들은 이렇게 해보세요.

개발환경설정 그대로 진행 후에~

ts-node라는 걸 진행을 할거라서 이걸 깔아줄게요. 이건 일반 TS에서 let a = 1; a = "one"하면 타입 안맞는다고 나던 오류가 노드로 한 번 컴파일을 해줘야함. 그럴 필요없이 바로바로 실행이 가능합니다. (???이게 뭔소리임?) 개발할 때 편하기 때문에 사용할 겁니다.

ts-node는 express module import해와서 port 지정해주고, 그런데 코드가 수정되어도 서버를 껐다가 다시 켜야지 이게 반영이 되는 불편함이 있습니다! 그래서 nodemon 이라는 툴을 써서 서버를 자동으로 껐다 켜주는 툴로 관리해줄 거예요!

```node
npm i -D nodemon

```

근데 노드몬은 ts-node에 대한 의존성이 있어서 이게 미리 깔려있어야함

** cannot use import outside a module 이게 뭘까?
package.json에서 "type": "module"을 설정해주지 않으면 모듈 바깥에서 import 문을 사요할 수 없다는 뜻
import는 모듈식이고, commonJS에서는 require을 쓰니까. 이걸 명시해주지 않으면 뜨는 듯.
근데 이걸 쓰면 nodemon에서 .ts 확장자를 알 수 없다고 뜬다. 그래서 nodemon 사용할 때는 빼줘야함!

-- 여기 까지 한 것 localhost:3000 에서 Hello, world 띄우기 (이거 그냥 npm start하면 되던 거 아닌가? 왜 parcel이니 뭐니 이런걸 사용하는 걸까?)
-- vercel? 그것도 써봐야되는데 깃에 푸시만 하면 deploy되는 그그그 (근데 애초에 이걸 왜 하느닞 알아야 될거같음 일단 수업 듣자.)

REST API
http 표준을 만드는 데 참여한 Roy Fielding 님이 박사과정 논문으로 낸 것, 리처드슨 성숙도 모델이라고 부르는.. 이르케 해야된다 REST하게 하려면... resource를 도입하면 level1, http verbs를 포함하면 level2, 3, 4까지 있지만 2까지만 충족시키는 정도로 사용함.

As-is: /write-post
To-be: /posts

이 주소로 접속하면 머가 된다.
-> 이 리소스에 대해서 먼가 한다.

CRUD에 대해 ?HTTP Method를 대입했고, Collection(복수)와 Item(Element, 단수)로 나뉨
기본 리소스 URL: /products

1. Read (Collection) => GET /products => 상품 목록 확인
2. Read (Item) => GET /products/{id} => 특정 상품 정보 확인
3. Create (Collection Pattern 활용) => POST /products
4. Update (Item) => PUT 또는 PATCH /products/{id} => 특정 상품 정보 변경 (% fetch api통해서만 처리할 수 있다. 브라우저 기본동작은 아님!)
5. Delete (Item) => DELETE /products/{id} => 특정 상품 삭제 (% 진짜로 DB에서 지울 필요는 없음 브라우저에서 안보이게 처리한다거나 하는 방법을 사용할 수 있음.)

이걸 Thinking in React 예제에 활용해봅시다.

끝
