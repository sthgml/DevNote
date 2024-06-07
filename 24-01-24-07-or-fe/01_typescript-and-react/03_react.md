# 03. React

## 1. 오늘의 강의 요약

- 리액트 = 상태를 잘 골라내는 것이 핵심
- 상태가 변하는 특정 컴포넌트만 부분적으로 리렌더링
- 상태란?
  - 변화, 계산, 주입여부

## 2. 오늘 배운 것

### 2-1. 상태란

state as a snapshot
useState는 비동기인줄 알았지?
엄밀히 말하자면 동기!
함수 컴포넌트 안에서 선언된 함수 중 외부 변수에 대한 접근이 필요한 함수들은 모두 클로져!

### 2-2. 렌더링?

루트노드부터 변화된 거 뭔지 파악 - diffing
재조정 reconciliation


### 2-3. 리렌더링은 언제?
동일한 위치에서 동일한 노드 (이 기준은 타입, props, 상태)가 렌더링 요청이 오면,
새로 그리는 게 아니라 원래 있던걸 "유지" 함
부모노드가 리렌더링 되면 같이
안되게 하려면 react.memo
key = props가 안바뀌었는데 리렌더링 되는 것 방지

### 2-4. 리액트 성능 최적화

리렌더링 횟수를 줄이기 = 안해도 되는 애들은 적절히 건너 뛰기

- React.memo: props가 변경되었는지 확인하고, 아니라면 건너뜀 
  - 이 때, 변경되었다의 기준은 === (얕은 비교)
  - 서로 다른 두 객체의 개별 필드를 모두 확인하고, 객체의 내용이 서로 다른 값인지 확인
- props로 children이 전달되었을 때 
  - 이전과 정확히 동일한 요소의 참조를 반환하면 내용이 바뀌어도 주소값이 같기 때문에 props의 변화를 인식할 수 없습니다.
- useMemo 사용하기: 의존배열에 들어간 변수들이 바뀌지 않으면 useMemo에러 반환된 요소는 리렌더링 되지 않음 

  ```JS 
  const memoizedElement = useMemo(() => {
    return < ExpensiveChildComponent/>
  }, [counter1]) 
  ```

- useLayoutEffect: state가 여러번 변해도 최종값만 적용시켜서 렌더링함
- React.Component.shouldComponentUpdate(): 콜백함수로써 리렌더링 여부를 커스텀 하는 함수
- React.PureComponent:
