---
description: node - html과 인터넷이 무엇인지
---

# Node.js

### 탄생 배경

1990 - html의 탄생 종이로 담겨져있던 정보들이 웹페이지로 이동. 종이로부터의 엑소더스의 시작 웹이 등장한 직후에 수많은 불만이 쏟아져나옴&#x20;

사람이 html코딩해서 하나하나 수정해야했음, 방문자들이 직접 글을 올리도록 하고 싶었지만, 웹페이지가 담긴 파일을 마음대로 수정하게 하는 거슨 너무 위험한 일이었ㅇ습니다.

html 성장의 한계 직접 작성하기 귀찮아. 기계에게 시키고 싶었다.&#x20;

JS에 익숙한 개발자들이 활용할 수 있도록 만들고 싶었다.

1995 -&#x20;

2008 - 구글 크롬 브라우저 V8 엔진 오픈소스로 공개

node.js - JS를 이용해 브라우저가 아닌 컴퓨터 자체를 제어

### Node.js의 필요성

* 생산성
* 홈페이지, + 세페이지가 있다 글 목록이 숫자로 되어있는 ol 태그라면 순서가 없는 목록으로 만들고 싶다면 ol 태그를 ul태그로 바꾸면 됩니다.
* 1억개의 페이지가 있다면 같은 작업을 1억번 반복해야하므로 한계를 갖게됨.

```javascript
// template.js
module.exports = {
    html: function(list, articleTag, navTag = ""){
        var i = 0;
        while (i < list.length) {
            listTag = listTag + `<li><a href="/?id=${list[i]}"></li>`
            i++;
        }
        return `
            <>...</>
        `
    }
}

```

node js - 웹 브라우저 뿐만아니라 컴퓨터 자체를 제어할 수 있게 됨으로써, ㅂ컴퓨터 자체 즉 서버에 읽기, 쓰기, 수정, 삭제가 가능해짐 => 내 컨텐츠를 서버에 올리고, 수정하고, 삭제할 수 있게 됨

### 목표: Node.js로 웹 applicaion 만들어보기

* node.js application
* node.js runtime: nodejs가 가진 기능을 실행시켜야 함
* javascript: node js 기능을 실행시키기 위한 조작장치

### nodejs로 웹서버 만들기

* 웹서버 기능을 내장하고 있음
* apache web server는 할 수 없는 일을 시킬 수 있어용

```javascript
var http = require('http'); // http요청을 주고받는 모듈
var fs = require('fs'); // file을 읽는 모듈
var app = http.createServer(function (request,response) {
    var url = request.url;
    if (url == '/') { // '/' url이면 아래 경로를 저장합니다.
      url = '/index.html'; 
    }
    if (url == '/favicon.ico') {
      response.writeHead(404);
      response.end();
      return;
    }
    response.writeHead(200);
    response.end(fs.readFileSync(__dirname + url));// 아래 링크의 file을 읽으며 종료
});
app.listen(3000);
```

### url이란?

구성

* http//: 통신규칙 protocol
* opentutorials.org : host 도메인 이름
* :id : 포트 번호 (웹서버가 쓰겠다고 약속한 정보 = 80)
* /main: 경로
* ?id=adsfa : queryString

위의 웹서버를 구현한 코드에서 queryString을 이용해서 다르게 값을 보여주도록 조장하는 방법은?
