# 01. 개발 환경 세팅
## 1. 오늘의 강의 요약
### 1-1. 환경
- node.js 설치
- shell 등 cli 사용하기
### 1-2. 프로젝트 구조
- 프로젝트 폴더에 필요한 파일들
### 1-3. npm/ npx로 패키지 설치하기
- 설치한 패키지 사용하기
- 명령어 세팅하기

## 2. 오늘 배운 것
### 2-1. cli 명령어
#### 생성
- mkdir 폴더이름
- touch 파일이름
#### 삭제
- rm 폴더혹은파일이름
### 2-2. 프로젝트 폴더 구조
- .gitignore: gitignore.io 에서 생성하거나 github에서 복붙
- .eslintignore: 위의 코드 복붙가능
### 2-3. npm/ npx로 패키지 설치하기
#### npm
- npm --init  ->  package.json
- npm i 패키지이름 -> package.json내에 dependencies에 생성
- npm i -D 패키지 이름 -> package.json내에 devDependencies에 생성 (build할 때 제외) = ( npm install --save-dev 의 단축어임)
- npx (= node_modules/.bin/에 이미 설치되어 있거나 캐시되어있던 데이터로 설치하는 명령어 = 성능이 굉장히 좋다.)
### 패키지
- tsc : TypeScript Compiler
- parcel : 
  - 노드 : main: "index.js"
  - 웹서버: source: "./index.html"
- eslint : 정적분석기
  - --init :하면 초기설정 가능
    - 이때 뭐 많이 물어봄 
    - import/exprot (ES module - parcel이라는-bundler로 사용할 것) vs require/exprots (commonJS)
  - 사용법: npx eslint --fix . 하면 빨간줄 다 고쳐줌 
    - package.json에 "scripts" : {여기에서 명령어 만들어주기 가능}
      ``` "start": "parcel --port 3000",
      "build": "parcel build",
      "check": "tsc --noEmit",
      "lint": "eslint --fix --ext .js,.jsx,.ts,.tsx .",
      "test": "jest",
      "coverage": "jest --coverage --coverage-reporters html",
      "watch:test": "jest --watchAll" ```