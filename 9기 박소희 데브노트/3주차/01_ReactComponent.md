# 1. React Component

## 1. 아토믹 디자인 시스템

1. 개념 및 정의
    1. 디자인 시스템 방법론 중의 하나
    1. 주기율표 상의 원자(atom)들이 어떻게 결합하느냐에 따라서 세상 모든 것들을 생성할 수 있듯이
    1. 웹페이지의 컴포넌트를 5가지 레벨로 나눠 체계화하는 방법
1. 필요성 및 의의
    1. 규칙을 제각각으로 만들면, 관심사가 너무 많거나
    1. 재사용이나 확장할 수 없는 컴포넌트가 생기는 문제를 해결하기 위해
1. 특징
    1. atom - molecule - organism - Template - page으로 컴포넌트를 쪼개는 방법
    1. atom: 더이상 쪼갤 수 없는 단일요소 (ex. 태그, 글꼴, 컬러팔레트, 레이아웃 등)
    1. molecule: 여러 atom을 결합, 고유의 특성을 가짐, 한가지 동작을 함(SRP, Single Responsibility Principle) - 테스트하기 쉽고, 재사용성 높음
    1. organism: 특정 컨텍스트를 가짐, 상대적으로 구체적, 재사용성 낮음 (ex. header)
    1. Template: 컴포넌트를 배치하고 구조를 잡는 와이어프레임, 컨텐츠가 없는 page (스켈레톤)
    1. Page: 유저가 보는, 실제 컨텐츠를 담은 요소, template의 인스턴스라고 볼 수 있음.
1. 방법
    1. Molecule vs Organism
        1. SRP, Single Responsibility Principle을 지킬 수 있느냐
        2. Context가 없어도 컴포넌트의 역할이 설명이 되느냐
        3. 그래도 모호하면 일단 Organism
    2. 중복 컴포넌트
        1. compound 컴포넌트 (합성 컴포넌트)로 해결하기
        2. UI 제어하는 상태 이런거는 다 외부에서 주입하기 (스토리북 유용)
        3. 마진, 패딩과 같은 레이아웃 관련 스타일도 외부에서 주입하기
    3. UI 모델링
        1. 하나의 컴포넌트의 단위를 쪼개고 네이밍 하는 과정을 피그잼을 통해 함께 진행하기
1. 개인적인 생각(추가적인 질문 또는 인사이트)
1. 레퍼런스 모음
    [아토믹 디자인을 활용한 디자인 시스템 도입기](https://url.kr/tkcou6)

1. 목업의 개념

    ```plain
    어떻게 작업을 할 것이냐..
    대략적인 모습
    완성은 아니지만
    그렇다고 큰 변화가 있을 것도 아닌 결과물
    ```

1. RestAPI

Get, Post, Put, Patch;

1. GraphQL

query에서 얻고자 하는 걸 스키마처럼 넣어주거든요. 쿼리 자체에서 지정을 해줘요.
쿼리 랭귀지라서 SQL이랑 비슷해요.
Query(Read), Mutation(Command: Create, Update, Delete), Subscription(Event)

지금은 key로 쓸 수 있는게 없어서 전체를 하나의 문자열로 만든다거나 하는 방법으로 고유의 key를 만들어줘야해요.

1. JSON

JavaScript Object Notation : 경량의 데이터 교환형식이다.

json.org
더글라스 어쩌구님이 js를 제대로 쓰는 방법에 대한 ..

문자열과 오브젝트 사이의 데이터

문자열 -> 오브젝트: parse
오브젝트 -> 문자열: stringify

1. 컴포넌트 계층구조

자동차 조립하듯

1. 나누는 기준

    1. SRP (Single Responsibility Principle)

        1. SOLID
        1. 캡슐화된 컴포넌트
        1. 하나의 책임만 갖도록
        1. 컴포넌트가 너무 길어져 -> 쪼개줘야됨

    1. CSS 클래스 선택자 참고하기

    1. Design's Layer 디자이너가 짜놓은 그룹, 컴포넌트 기준 참고하기

    1. Information Architecture: JSON의 스키마 활용 => 바로 활용할 수 없다면 백엔드한테 요청 (아샬's pick)  => 자연스럽게 SRP가능 / 혹은 받은 데이터를 한 번 더 가공

    장점: 만들고 나면 조립 방식을 쉽게 변경 가능해짐

1. 아토믹디자인 => 계층형 구조를 몇 가지 카테고리로 묶은 방법

1. 정적인 ui먼저 구현 (ex. html 구조)

- DSL(Domain-Specific Language)
- 선언형 프로그래밍
- 명령형 프로그래밍
- React component 와 props

1. map 사용 -> 이름이 겹치지 않는다는 전제하에 이름을 키로 잡는다.

1. Extract Function
    1. Refactoring.com
    1. 코드를 함수로 뺀다 = 이 코드가 어떤 의도를 갖고 작성된 코드인지, 어떤 동작을 하는지 설명을 하겠다
    1. useRef
    1. selectCategories... 어쩌구.. 계속계속 쪼개고 쪼개고..

1. 여기까지가 정적인것 작동하게 하려면 어떻게 해야할까?