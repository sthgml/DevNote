# Hook

## 학습 키워드

- React Hook 이란
- Hooks
  - useState
  - useEffect
  - useContext
  - useRef
  - useLayoutEffect
- React StrictMode 란

## hook 소개

hoc= 재활용 할 때 많이 씀
Higher order componets function = 컴포넌트,
props로 내려주는 skill 이게 굉장히 복잡해여.
영상 보시면, react devtools에서 컴포넌트 있잖아요.
불필요한 wrapper 같은게 많이 들어가고, 컴포넌트 자체가 복잡해지고 커지는 문제도 있고, 자바스크립트에서 이 경우에 this는 어떻게 될까요 퍼즐처럼 내는 경우가 있다. 얼마나 JS를 잘 이해하나 이런 문제를 낼 수는 잇음 , You don't know JS라는 책도 있음. 굉장히 혼란스러운게 있는데, 객체지향적으로 짜는 것도 아니에요 컴포넌트라는게, 객체지향이랑 상관이 없는 거거든요. 그래서 hooks가 들어와서 react를 쓰는 방법을 완전히 바꿔요. 그래서 function 컴포넌트 + hook으로 바꾼거예요. (클래스 컴포넌트에서)

React를 쓰는 방식을 완전히 바꿈

기존 사용법:
클래스 컴포넌트 vs 함수형 컴포넌트

- 상태를 가진 컴포넌트 vs props 만으로 사용되는 컴포넌트
- Redux에도 비슷한 구분이 존재했음.
- Container vs Presentational

현재:

- 함수형만 사용
- 상태 관리 유무를 바로 알기 어려움 == 신경쓰지 않아도 됨 (전에는 클래스면 상태 있겠거니) (하지만 여전히 신경써주면 좋음 ex. memoize props가 완전히 같으면 함수 자체가 실행되지 않게 하는 등)
- 복잡한 요소는 전부 Hook으로 격리 및 재사용 가능 (전에는 컴포넌트 안에 이것저것 들어갔었는데.. 격리하는거 재사용하는게 너무 쉬워요)

대표적인 훅

- useState => stateHooke = react State
- useEffect => side-effect = component did mount랑 같은 것처럼 사용하지만 사실은 syncronization와 더 유사함 (동기화), 의존배열 비워둘거면 useCallback, useReducer의 사용법을 배워라. useEffect는 mount됐을 때 뿐만아니라 update 될때도 실행된다. effect의 의미는 side-effect니까 의존배열이 바뀌면 그 부산물로 실행되는 함수인거임,
useEffect안의 함수는 useEffect 이후에 선언한 다음에 hoisting되게 하는 것을 추천합니다. 단, 컴포넌트 밖에서 props나 상태를 전달받지 않아야 합니다. 
useEffect는 그것이 만들어진 render()에서 값을 받아옵니다. 예를 들어 다음과 같은 html코드가 있다고 했을 때

<button onClick(()=>{/* 클릭할 때마다 count++ */})>
<button onClick(()=>{/* 클릭하면 3초뒤에 count를 보여줌*/})>

두 번째 버튼을 누르고 3초 안에 첫 번째 버튼을 10번 눌렀다고 했을 때, 3초뒤에 뜨는 count == 0 입니다.

렌더링 이후에 해야할 일 - 화면에 그리는 거냐, react element dom tree를 그리는 거냐. 확실하게 돔트리 떨어지고, 그린ㄴ 것도 자바줌. 객체 떨어짐 돔으로 확실히 나간 다음에 거기있는 요소들을 끌어다 쓰고싶다. useEffect test해보시면 알 수 있다. rㅣ본적으로 렌더링때마다 실행됨.

- useContext =>
- useRef
--- 여기까지는 알아야되고 나머지는 문서 보면서 사용하기
- useLayoutEffect != useEffect
