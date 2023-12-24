# JSX
## 1. 개념: JSX란????!
- XML처럼 생긴,
- JS를 확장한 문법이다.
- React의 부산물
- 꼭 React에서만 쓰는 것은 아님 Vue JS에서 컴포넌트를 만들때 사용하면 더 복잡한 것도 만들 수 있다.
  - 다만 React자체가 잘나가면서 한 몸처럼 여겨지고 있다.
  - (VSC가  아톰의 부산물이었던 것처럼)
- 일종의 Syntax Sugar임
- html을 그대로 쓸 수 있고, JS코드와 1:1로 매칭된다.
  ```JSX
  (
    // 안에는 <> html 코드인데
    { /*를 쓰먼 이 안에는 JS를 쓸 수 있다.*/}
  )
  ```

## 2. 사용해보기
https://babeljs.io/repl 에서 예시로 사용해보기 좋다.
- 왼편에서 `Presets react`를 체크하거나
- Add Plugin 에서 react-jsx를 검색해서 `@babel/plugin-transform-react-jsx`를 추가하면 JSX를 사용해볼 수 있다. 
- ++) /* @jsx 어쩌구~ */ 라는 주석을 추가하면 React.createElement 부분이 어쩌구~함수로 대체된다!

### Example #1
JSX 코드
```html
<p>hello world</p> 
```
JS로 변환
```JS
React.createElement(
  "p", // 태그 종류
  null,  // 클래스 이름이나 id등 속성이 객체형태로 들어감 {className: "", id: ""}
  "Hello world" // 태그 안의 내용
);
```

### Example #2
JSX 코드
```html
<>
  <p>hello world</p> 
  <p>hello world</p> 
</>
```
JS로 변환
```JS
React.createElement(
  "div", 
  null, 
  React.createElement(
    "p", 
    null,  
    "Hello world" 
  );,
  React.createElement(
    "p", 
    null,  
    "Hello world" 
  );
);
```
JSX automatic runtime으로 설정을 바꾸면
```JS
(0, _jsxRuntime.jsxs)(
  "div", 
  null, 
  children: [(0, _jsxRuntime.jsxs)(
    "p", 
    null,  
    children: "Hello world" 
  ),
  (0, _jsxRuntime.jsxs)(
    "p", 
    null,  
    children: "Hello world" 
  )]
);
```
이렇게 바뀌는데 이게요새 JSX의 방식이긴 함

JSX로 쓸수 있는 모든 것은 JS로 만들어줄수 있다.
```JavaScript
const div = document.createElement("div");
div.className = "division";
const children = document.createElement("p");
children.innerHTML = "hello, world!";
children.className = "children";
div.append(children);
// same as... 
React.createElement("div", {className: "division"}, 
  React.createElement("p",{className: "division"}, "hello, world!" )
);
```

## 3. VDOM, Virtual Document Object Model
React는 DOM을 직접적으로 만드는게 아니라 Virtual DOM트리를 만드는 것.
실제 DOM과 이 VDOM을 계속적으로 비교를 하면서 다른게 생기면 그 트리만 새롭게 렌더링 함. 그렇기 때문에 효율적인 것!

```typescript
function Image({src, alt = "", width}: {
  src: string;
  alt?: string;
  width?: number;
}) {
  return (
    <img src={src} alt={alt} width={width ?? 'auto'} />
  )
}
```

### 선언적 api
- 컴포넌트: 새로운 트리노드 리액트 엘리먼트 주는 것 뿐임
- 그냥 <> <> 이런 형식으로 쓸 수 있다.
- <-> 서술형 api : 
  - React.createElement("div", {className:"sohee"}, "hello world") 
  - 
    ``` 
    (React creates elements of div tag, classified as sohee and it will have children of p tag with "hello world" string.)
    ```

### key 를 써주는 이유
Dom을 비교할 때 순서만 바뀌었는데 다 바뀌었다고 생각하고 다 리렌더링하는 불상사를 막기 위해 
```
ex) dom: 123456 vs vdom: 234567
keyX: 어 다바뀌엇네 => 다 리렌더
keyO: 어 23456은 키가 같네 => 2개만 리렌더
```
