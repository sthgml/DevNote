---
description: node - html과 인터넷이 무엇인지
---

# Node.js

## 1. 탄생 배경

1. 1990 - html의 탄생
   1. 종이로부터의 엑소더스의 시작
   2. 종이로 담겨져있던 정보들이 웹페이지로 이동.
   3. 웹이 등장한 직후에 수많은 불만이 쏟아져나옴
   4. 개발자 사람이 html 코딩해서 하나 하나 수정해야 했음
   5. 방문자들이 직접 글을 올리도록 하고 싶었지만, 웹페이지가 담긴 파일을 마음대로 수정하게 하기는 너무 위험
   6. JS에 익숙한 웹개발자들이 활용할 수 있는 자동으로 웹페이지를 만드는 서버사이드앱을 만들다
2. 1995 - Netscape의 브랜든 아이크가 JS를 개발을 의뢰받음
3. 2008 -
   1. 구글 크롬 브라우저 V8 엔진 개발 및 오픈소스로 공개
   2. node.js - v8 엔진을 기반으로 개발
      1. JS를 이용해 웹브라우저가 아닌 컴퓨터 자체를 제어
      2. JS의 인생역전
      3. html 코딩은 컴퓨터에게, 컨텐츠를 생산하는 창의적인 일은 인간에게

## 2. 공부방법

node js 앱 만들기 ← 노드 js runtime : 노드 js 가 가진 기능을 활용하기 ← JS 문법 알기

## 3. 웹 서버 만들기

1. 웹 브라우저와 웹서버의 관계
   1. 웹 브라우저
      1. 주소를 입력해서 요청한다.
   2.  웹 서버

       1. 요청에 따른 정보를 찾아서 응답해주는 관계
       2. 1.html, 2.html … 등등이 있는 폴더에서 server.js파일을 만들고 노드로 실행시키면
       3. [localhost:3000](http://localhost:3000) 을 통해서 브라우저에서 접근이 가능하다

       ```jsx
       var http = require('http');
       var fs = require('fs');

       // server 만들기
       var app = http.createServer((request, response) => {
         // request에 url마다 다른 response 하기
         var _url = request.url;
         if(_url == '/'){
           _url = '/index.html';
         }
         if(_url == '/favicon.ico'){
           response.writeHead(404);
           response.end();
           return;
         }
         
         // 200 response 일 때, 간단하게 __dirname(내 현재 디렉토리 경로에 요청한 url의 파일을 보여주자)
         response.writeHead(200);
         // 프로그래밍 적으로 사용자에게 전송할 데이터를 생성할 수 있다.
         response.end(fs.readFileSync(__dirname + _url));
       });

       // port 번호 지정하기
       app.listen(3000);
       ```

## 4. URL 이해하기

`http://opentutorials.org:3000/main?id=HTML&page=12`

1. protocol
   1. 통신 규칙
   2. 사용자가 서버에 접속할 때 어떤 방식으로 소통할 것인지
   3. Hyper Text Transfer Protocol: 웹 브라우저와 웹서버가 데이터를 주고받기 위해서 만든 통신 규칙
2. host(domain name)
   1. 인터넷에 접속되어 있는 각각의 컴퓨터를 가리키는 주소
3. port 번호
   1. 한 대의 컴퓨터 안에 여러 대의 서버가 있을 수 있어요.
   2. 클라이언트가 접속했을 때 그 중에 어떤 서버와 통신할 지 애매해요.
   3. 접속할 때 3000 이라고 하면 3000에 연결된 서버와 통신하게 되는거예요.
   4. 3000 포트에 우리의 노드 js 웹서버를 실행시킨 것이기 때문에 3000으로 해야돼
   5. 웹 서버는 80 번 포트를 쓴다고 전세계적으로 약속되어있음 포트번호를 생략하면 80에 접속하게됨
4. path
   1. 컴퓨터 안에 있는 어떤 폴더의 어떤 파일인지를 가리킴
5. 쿼리스트링
   1. 쿼리스트링의 값을 변경하면 앞에잇는 웹서버에게 데이터를 전달할 수 있어요
   2. 위의 예시의 경우 내가 읽고 싶은 정보는 html 이고 12 페이지다
   3. 약속
      1. 쿼리스트링의 시작은 ?
      2. 값과 값은 &로 구분
      3. 값의 이름과 값은 =으로 구분

## 5. URL에 따라 다르게 동작하는 웹앱 만들기

### 5-1. URL 파싱하기

\<aside> 💡 `http://localhost:3000/main?id=HTML&page=12` 이라는 url 이 있을 때

`main?id=HTML&page=12` (queryString) 을 어떻게 활용할 수 있을까?

\</aside>

1. `url` 모듈을 임포트
   1. `var url = require("url");`
2. `queryData` 추출하기
   1. `url.parse(request로받은url, true).query`
3. `queryData`에서 값의 이름으로 값을 추출하기
   1. `qureyData.값의이름`
   2. 위의 예시에서는 `queryData.id == “HTML”`, `queryData.page == “12”`

### 5-2. response 동적으로 변경하기

1. 파일 → text
   *   전체 코드

       ```jsx
       var http = require('http');
       var fs = require('fs');
       // require = module = 이미 구현된 기능들 중 비슷한 것들을 묶어놓은(그루핑한) 것
       var url = require('url');

       // server 만들기
       var app = http.createServer((request, response) => {
         var _url = request.url;
         var queryData = url.parse(_url, true).query;
         // 의미론적인 변수 네이밍하기
         var title = queryData.id;

         // console.log('queryData: ', queryData);
         // /?id=HTML

         // console.log('queryData.id: ', queryData.id);
         // HTML

         if( _url == '/'){
           _url = '/index.html';
           title = 'Welcome';
         }

         if(url == '/favicon.ico'){
           response.writeHead(404);
           response.end();
           return;
         }
         
         response.writeHead(200);
         
         // 프로그래밍 적으로 사용자에게 전송할 데이터를 생성할 수 있다.
         // response.end(fs.readFileSync(__dirname + _url));
         
         // response.end(queryData.id)
         
         // response 데이터를 동적으로 변경해보자
         var template = `
         <!doctype html>
         <html>
           <head>
             <title>WEB1 - ${title}</title>
             <meta charset="utf-8">
           </head>
           <body>
             <h1><a href="/">WEB</a></h1>
             <ol>
               <li><a href="/?id=HTML">HTML</a></li>
               <li><a href="/?id=CSS">CSS</a></li>
               <li><a href=/?id=JavaScript">JavaScript</a></li>
             </ol>
             <h2>${title}</h2>
             <p>
               ...
               ${/* 여기에 이제 들어갈 텍스트를 파일로 저장하고, 불러와야 함 */}
             </p>
           </body>
         </html>
         `
         response.end(template);
       });

       app.listen(3000);
       ```

   * response로 넘겨주던 파일을 template으로 활용
   * 내가 필요한 부분만 literal로 포함시키기
2. Node.js로 CRUD 구현하기
   *   전체 코드

       ```jsx
       var http = require('http');
       var fs = require('fs');
       var url = require('url');

       var app = http.createServer((request, response) => {
         var _url = request.url;
         var queryData = url.parse(_url, true).query;
         var title = queryData.id;

         if( _url == '/'){
           title = 'Welcome';
         }

         if(_url == '/favicon.ico'){
           response.writeHead(404);
           response.end();
           return;
         }
         
         response.writeHead(200);
         fs.readFileSync(
           'data/' + title + '.txt', 
           'utf8', 
           (err, data) => {
             var template = `
               <!doctype html>
               <html>
                 <head>
                   <title>WEB1 - ${title}</title>
                   <meta charset="utf-8">
                 </head>
                 <body>
                   <h1><a href="/">WEB</a></h1>
                   <ol>
                     <li><a href="/?id=HTML">HTML</a></li>
                     <li><a href="/?id=CSS">CSS</a></li>
                     <li><a href="/?id=JavaScript">JavaScript</a></li>
                   </ol>
                   <h2>${title}</h2>
                   <p>
                     ${data}
                   </p>
                 </body>
               </html>
             `
           response.end(template);
         })
       });

       app.listen(3000);

       ```

   *   파일을 읽어오는 방법

       ```jsx
       // fs 모듈 임포트 하기
       var fs = require("fs");
       ...
       fs.readSync(”경로”, “인코딩방식”, (err, data)⇒{
       	// file읽기 이후에 할 동작
       	var template = `
       	<!doctype=HTML>
       	...
       	${title}
       	...
       	${data}
       	`
       })
       ```

3. Node.js로 cli에서 입력값을 받아오기
   1. 실행시킬 때 뒤에 문자열 입력
   2. `var args = process.argv;`
   3. 전체 코드

       ```jsx
       var args = process.argv;
       console.log(args);

       /* 
       terminal 에서
       node conditional.js 
       하면 이 파일이 실행되는데 이때

       node conditional.js 어쩌구저쩌구
       이렇게 하면 어쩌구저쩌구 같은 text가 split(' ')된 것처럼 
       args[2]부터 배열로 저장됨
       */

       /* 
         >> node conditional.js sohee
         >> 출력결과 [
           '/usr/local/bin/node',
           '/Users/sohee/Documents/000000-git-repository/web1_html_internet/conditional.js',
           'sohee'
         ] 

         >> node conditional.js sohee princess
         >> 출력결과 [
           '/usr/local/bin/node',
           '/Users/sohee/Documents/000000-git-repository/web1_html_internet/conditional.js',
           'sohee',
           'princess'
         ] 
       */

       ```

4. 폴더의 변경사항 받아오기
   1. readdir.js

       ```jsx
       var testFolder = './data';
       var fs = require('fs');

       fs.readdir(testFolder, function(error, filelist) {
       	console.log(filelist);
       });
       ```

   2. 받아온 list를 토대로 \<li> 태그 만들기

       ```jsx
       function createTemplateList(fileList) {
         var list = '<ul>';
         for (i = 0; i < fileList.length; i++) {
           list += `<li><a href="/?id=${fileList[i]}">${fileList[i]}</a></li>`
         }
         list = list + '</ul>';
         return list;
       }
       ...
       fs.readdir("./data", function(error, fileList) {
         // fileList 받아오기
         const list = createTemplateList(fileList);
       }
       ```

## 6. Node.js에서의 동기와 비동기

### 6-1. Sync 적용해서 리팩토링하기

```jsx
var http = require('http');
var fs = require('fs');
var url = require('url');

function createTemplateList(fileList) {
  var list = '<ul>';
  for (i = 0; i < fileList.length; i++) {
    list += `<li><a href="/?id=${fileList[i]}">${fileList[i]}</a></li>`
  }
  list = list + '</ul>';
  return list;
}

function createTemplateHTML(title, list, body) {
  return `
    <!doctype html>
    <html>
      <head>
        <title>WEB1 - ${title}</title>
        <meta charset="utf-8">
      </head>
      <body>
        <h1><a href="/">WEB</a></h1>
        ${list}
        ${body}
      </body>
    </html>
  `
}

// server 만들기
var app = http.createServer((request, response) => {
  var _url = request.url;
  var queryData = url.parse(_url, true).query;

  // title설정
  var title = queryData.id;
  if (_url === "/" || !title) {
    title = 'Welcome';
  }

  // lsit설정
  const fileList = fs.readdirSync("./data");
  const list = createTemplateList(fileList);

  // text 설정
  const text = fs.readFileSync(`./data/${title}`, 'utf8');
  
  // 404 response 처리하기
  if (!text) {
    response.writeHead(404);
    response.end("Not Found" + list);
    return;
  }

  // 200 response 응답 생성하기
  const template = createTemplateHTML(
    title, 
    list, 
    `<h2>${title}</h2><p>${text}</p>`
  );

  response.writeHead(200);
  response.end(template);
});

// port 번호 지정하기
app.listen(3000);
```

## 7. Package Manager

1. PM2
   1. node js를 껐다 다시 실행시키는 과정을 자동화
   2. 수정할 때마다 알아서 껐다 켜줌
   3. `npm i pm2 -g` : -g = 독립적인 프로그램이라서 컴퓨터 어디서든 실행 가능해야한다

## 8. App 제작 - 글 생성 UI 만들기

1. get 해올때는 url의 queryString으로 접근해도 되지만
2. 그 외에 post, put, delete (create, update, delete)할 때는 절대 url의 query string으로 해서는 안됩니다.
   1. 왜냐하면 맥락없이 url로 접근한 사람이 우리 서버의 파일을 조작할 위험이 있기 때문이에요
3. 대신에 사람눈에 보이지 않는 데이터로 무한히 긴 데이터를 보낼 수 있는 방법이 있어용
   1. form 태그의 method를 post로 바꾸기
   2. action = form data를 submit 할 url
   3. submit 을 수행하면, (e.preventDefault()하지 않으면 생기는일)
      1. action의 url로 옮겨간다.
      2. 해당 url에서 evnet를 감지한다.
      3. request.on(”data”, () ⇒ {}) : 여기 콜백함수에서 post 로 받아오는 데이터가 많을 경우를 대비해서 조각조각 받아노는 데이터들을 수신하고, 조각을 수신할 때마다 콜백함수를 호출하도록 약속되어있음
      4. 위의 작업이 끝나면 “end” 이벤트가 발생하고
      5. 이를 다음의 함수로 감지할 수 있다.
      6. request.on(”end”, ()⇒{}) : 이벤트가 감지되면 콜백함수가 실행되고 여기서 querystring모듈을 활용해서 body내용을 parsing한다.
      7. form에서 설정했던 name이 key이고 사용자가 입력한 내용이 value로 합쳐진 하나의 객체가 반환된다!

          ```jsx
          var qs = require("querystring");
          ...
          var body = '';
          request.on("data", (data) => {
            body += data;
          });

          request.on("end", () => {
            var post = qs.parse(body);
            console.log(post);
          })
          ...
          // >> {title: "nodejs", description: "nodesjs is awesome"}
          ```
