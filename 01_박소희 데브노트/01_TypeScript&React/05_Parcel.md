# 5. Parcel

- parcel이란?

  - 빌드란?
    - 가장 큰 것은 번들러
    - 번들러, 모듈, zero configuration
    - 브라우저들이 지원을 안해서 하나의 파일로 합쳐주는 것을 번들러, 합치는 행동을 빌드 라고 함
    - 최신 JS를 지워하지 않는 브라우저를 위해 JS를 변환 시켜준다거나, TS를 JS로 변환시켜 준다거나,
    - 파일 합치는 것 뿐만 아니라 그런 도구까지 포함
  - SWC: rust로 만든 TS compiler 를 사용해서 기존의 것보다 빠름 (한국인이 만들)
    - ES Module을 적극 활용하는 Vite도 엄청 빠름

- 설정 바꿀 것 딱 하나, 방법 두가지
  - 1. 소스 - package.json => "source": "./index.html"
  - 2. 패키지 - `npm i parcel-reporter-static-files-copy`
    - 그 후 .parcelrc 파일작성
    - .parcelrc에 들어갈 내용

      ```JSON
      {
        "extends": ["@parcel/config-default"],
        "reporters":  ["...", "parcel-reporter-static-files-copy"]
      }
      ```

    - => static 폴더의 파일을 정적 파일로 Serving 할 수 있다.

- 명령어
  - npx parcel
  - npx parcel index.html
    - package.json에서 source를 index.html로 바꿈
  - npx parcel index.html --port 8080
  - npx parcel build (/ npm run build)
    - dist 폴더가 만들어짐 (사실 원래 있었음 npm start해도 만들어 놓고 활용함 )
  - npx servor ./dist
    - config가 없는 서버임
    - 배포되었을 때를 보고싶다면
    - serv0r (zero configuration)
  - rm -rf dist
    - 개발환경으로 다시 돌아오려면

# 5-2. ESLint

## 1. 목적

- 스타일 통일
- 잠재적 문제 발견
- 베스트 프랙티스 추천 -> 최신 트렌드를 학습하는데 활용 가능

## 2. 개요

- lint : 보풀?
- 소스코드를 분석하여 의심스러운 곳에 flag달아놓기
- 정적 프로그램 분석: 실행되는 시간이 비교적 짧고 프로그램을 분석함
- 동적 프로그램: 막 실행을 하다가 메모리를 반환하지 않느 게 잇다. 이러면 동적
- TSlint도 따로 있었는데 그것까지 커버를 해주게 되었다..

## 3. 사용법

- npx eslint --ext .tsx
- npm eslint --fix --ext .js,.jsx,.ts,.tsx . 하면 바로 고쳐줌
  - 이 명령어를 "lint"에 저장해놓으면 앞으로 npm run lint하면 사용가능~!
- 신경쓰일때마다 터미널에 가서 저걸 쳐서 고쳐주는 것은 너무 번거롭기 때문에,
  - eslint 확장프로그램 esLint 설치 (install)
  - .vscode 폴더 안에 settings.json 만들어서

    ```JSON
    {
      "editor.codeActionsOnSave": {
          "source.fixAll.eslint": true
      },
      // 여기까지가 자동 fix
      "editor.rulers": [
        80
      ],
      "trailing-spaces.trimOnSave": true,
    }
    ```

  - npm run lint & npm run check

## 4. 추천하는 연습 방법

지금까지의 모든 과정을 매일 아침 한 번씩 해보는 것!
