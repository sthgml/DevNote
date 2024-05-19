# 02. TypeScript

## 1. 오늘의 강의 요약

- 변수에 타입을 미리 지정
- 타입은 내가 만들 수도 있음 (객체와 클래스 그 사이 어딘가)
- interface vs Type (아샬선호)
- generic = 타입 내 타입에 대한 변수

## 2. 오늘 배운 것

### 2-1. 타입 지정

- 타입스크립트: 타입을 지정해줌
- JS에서는 타입을 지정하지 않아도 변수에 넣고싶은거 아무거나 넣을 수 있었지만,
- 보통 다른 언어에서는 변수에 넣기 전에 이 변수에 들어갈 데이터 타입을 알려줌
- 막 요런식으로 

  ```JAVA
  int number = 10
  ``` 

  이제 JS에 Type을 도입한 TS는 이렇게 써야됨

  ```TS
  let number: Number = 13;
  ```

  이제 오류나는 코드

  ```TS
  number = "열셋";
  // error TS2322: Type 'string' is not assignable to type 'Number'.
  ```

### 2-2. 함수 파라미터 지정

- ?: 로 있을수도 없을수도 한 파라미터를 만들 수 있지만 그보다는 안들어왔을 때 초기값을 설정해주는 편이 좋다.
- 예시

  ```TS
  // soso
  function add(x: number, y?: number) {
    console.log(x + (y || 0));
  }
  // better
  function add2(x: number, y: number = 0){
    console.log(x + (y || 0));
  }
  ```

- 여러개 중에 하나일 수 있다.
- 예시

  ```TS
  function add({x, y}: {
    x: number | string;
    y: number | string;
  }) {
    return {x, y};
  }
  ```

### 2-3. 타입, 인터페이스 커스텀

- interface vs Type (아샬선호)
- interface = 재선언 시 필드 추가됨

  ```TS
  interface Animal {
    species: String;
    hibernate: Boolean;
  }

  const bear:Animal = {
    species: "포유류",
    hibernate: true,
    // 밑에 선언 때문에 이제 bear 도 habitat property가 필요함
  }

  interface Animal {
    habitat: String;
  }

  const crocodile: Animal = {
    species: "양서류",
    hibernate: true,
    habitat: "늪지" // 없으면 오류남
  }
  ```

- type = & 연산자로 두 타입의 교집합 타입 만들 수 있음

  ```JS
  type Teacher = {
    school: String;
    tools: String;
  }

  type Female = {
    period: Boolean;
    size: String;
  }

  type FemaleTeacher = Female & Teacher;

  const sohee: FemaleTeacher = {
    school: "kggh",
    tools: "brush",
    period: false,
    size: "80B",
  }
  ```

### 2-4. (나를 가장 혼란스럽게 만들었던) Generic

- 일종의 변수
- 타입 내에서 타입을 지정할 때
- 외부에서 주입할 수 있게 하는 타입 변수

  ```TS
  type Data<TypeFromOut> = {
    item1: TypeFromOut;
    item2: TypeFromOut;
  }

  const dataString: Data<String> = {
    item1: "sohee",
    item2: "jeeho"
  }

  const dataNumber: Data<Number> = {
    item1: 259,
    item2: 202131,
  }
  ```

### 2-5. TS 쓰는 이유

- VSC 자동완성
- 실시간으로 오류검사 해줌
- 같은 출처의 코드보다 외부 라이브러리 사용할 때 유용
- 오래된 라이브러리의 경우, ~.d.ts 만 따로 패키지로 제공되기도 함

## 3. 오늘 느낀 것

- 회사에서 혼자 공부하느라고 빨리 공부해야 된다는 압박감에 이해도 안되고,
- 제대호 이해했는지 불안했는데 이렇게 훑어보기 강의 들으니까 안심이 된다.
- 특히 generic 부분이 이해가 안됐었는데 이제 정리가 된다.
- 한 번 더 정리하자면, 커스텀 타입 내에서 사용되는 타입 들을 한 꺼번에 외부에서 통제하는 일종의 변수임.
