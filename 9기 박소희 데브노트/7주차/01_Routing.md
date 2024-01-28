# Routing

## 학습 키워드

- HTML DOM API
- Location
- pathname

### Location

Location

- 인터페이스
- 객체가 연결된 장소를 표현
- 이 인터페이스 변경 => 연결된 객체에 반영
- 아무 속성도 상속하지 않지만 URLUtils의 속성을 구현합니다.
- Document와 Window 인터페이스가 이런 Location을 가지고 있습니다.
  - Document.location
  - Window.location

Window.location

- Window 객체의 속성인 객체 중 하나
- 문서 내에서 현재 위치와 관련된 정보를 제공
- read-only속성을 가졌음에도 불구하고 마치 새로운 할당을 하는 것처럼 사용할 수도 있음
  - ex. location = 'https://google.com' == location.assign('https://google.com');
  - 위의 두 문장이 같은 동작을 함

사용법

```js
// Create anchor element and use href property for the purpose of this example
// A more correct alternative is to browse to the URL 
// and use document.location or window.location
var url = document.createElement("a");
url.href =
  "https://developer.mozilla.org:8080/en-US/search?q=URL#search-results-close-container";
console.log(url.href); // https://developer.mozilla.org:8080/en-US/search?q=URL#search-results-close-container
console.log(url.protocol); // https:
console.log(url.host); // developer.mozilla.org:8080
console.log(url.hostname); // developer.mozilla.org
console.log(url.port); // 8080
// 요거~! //
console.log(url.pathname); // /en-US/search
// 요거 ~! //
console.log(url.search); // ?q=URL
console.log(url.hash); // #search-results-close-container
console.log(url.origin); // https://developer.mozilla.org:8080
```

위의 객체를 이용해서 현재 url을 받아올 수 있고,
받아온 url에 맞는 컴포넌트를 렌더링 함으로써 페이지를 이동한 것 같은 효과를 낼 수 있다!

```js
const {pathname} = window.location();
...
{pathname === '/' && <Home />}
```
