# Fetch API & CORS

## 학습 키워드

- Fetch API 란
- Promise
- ReableStream
- Unicode
- CORS 란

## fetch api

fetch() => 반환값은 promise 객체
promise 객체는 .then으로 사용 가능!

```ts
const response = awiat fetch("http://localhost:3000");
```

을 했을 때, `response.body`가 `ReadableStream`입니다.
ReadableStream은 Reader를 반환해주는 getReader()를 가지고 있습니다.

```ts
const reader = response.getReader();
chunk = reader.read(); 
```

를 해주면

```js
{done: false, value: Uint8Array(475)}
```

이런 형태의 데이터가 전달되는데 이때 475의 의미는 475 byte입니다. 데이터의 길이
원래는 계속 돌면서 done: true 가 될때까지 돌아야됩니다.

```js
chunk.value = {
  123, 34, ...
}
```

이런 byte array는 text로 디코딩을 해주어야 합니다.

```js
const body = new TextDecoder().decode(chunk.value);
const data = JSON.parse(body);
```

JSON을 기본 지원합니다.
얻은 다음에 리스폰스에서 바디 어쩌구 해했잖아요. 이걸 이렇게 바꿔줍미다.

```js
const response = await fetch("http://localhost:3000/products");
cosnt data = await response.json();

// or
const response = fetch(url, {
  method: 'POST',
});
```

그 외에도 다양한 JS 함수가 있습니다.

```JS
const response = fetch(url, {
  method: 'POST',
  headers: {
    "Content-Type": 'application/json',
  },
  body: {
    JSON.stringify(data); 
  }
});
```

그런데 이걸 다른 웹앱 ip(?)에서 실행하려고 하면 CORS 에러가 납니다.
이것은 브라우저의 정책으로, Same Origin Policy 에 따라 웹페이지와 리소스를 요청한 곳의 출처가 서로 다를 경우 (ip + port)
%% 서버에서 얻은 결과를 사용할 수 없게 막는다. 서버에 요청하고 응답을 받아오는 것 까지는 이미 진행이 다 된 상황

REST API 서버에서 Headers에 "Access-Control-Allow-Origin" 속성을 추가하면 된다.

Expressdㅔ서는 CORS 미들웨어를 설치해서 사용하면 됨.

http://expressjs.com/en/resources/middleware/cors.html

패키지 설치

```node
npm i cors
npm i -D @types/cors
```

끝
