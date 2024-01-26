# External Store (외부 상태관리)

## 학습 키워드

- 관심사의 분리
- Layered Architecture
- Flux Architecture
- useReducer
- useCallback

### 관심사의 분리

1. 용어정리

    1. SOC, Seperation of Concerns
    1. 관심사
        1. 코드에 영향을 미치는 정보의 집합
        1. ex. 응용프로그램을 위한 하드웨어 세부사항(일반적)
        1. ex. 인스턴스화 하는 클래스의 이름(구체적)
    1. 모듈러 프로그램
        1. SOC를 잘 구현하는 프로그램
        1. 모듈러리티 = 관심사의 분리
    1. 캡슐화
        1. 정보를 잘 정의된 인터페이스가 있는 코드 안에 숨기는 것
        1. 정보 시스템의 계층화된 디자인
            1. presentation 계층, 비즈니스 로직 계층, 데이터 접근 계층, 영속성 계층
        1. 잘 정의된 인터페이스
    1. 추상화
        1. 인터페이스의 추가 필수
        1. 실행에 쓰이는 더 순수한 코드가 있는 것이 일반적
        1. 실행에 따른 불이익 있음

1. 장점 (사용하는 이유)
    1. 자유도
        1. 설계, 배포, 이용의 일부 관점에서
        1. 코드의 단순화 및 유지보수의 더 높은 수준의 자유. => 코드를 더 잘 정리할 기회가 생김
        1. 독립적인 개발과 업그레이드
        1. 모듈 재사용을 위함

1. 실행
    1. 모듈러나 객체지향 프로그래밍과 관련된 매커니즘은 개발자들이 SOC를 제공할수 있게 해준다. 예를 들어서 객체지향 프로그래밍언어인 C#, C++, Java와 같은 언어들은 관심사를 객체로 분리할 수 있다. 디자인 패턴 MVC나 MVP가 컨텐츠로부터 프레젠테이션과 데이터 프로세싱모델을 분리할 수 있는 것처럼. 서비스 지향 디자인은 관심사를 서비스로 분리할 수 있다. 절차 지향 프로그래밍언어 C나 파스칼 같은 것들은 관심사를 절차나 함수로 분리할 수 있다. aspect 지향 프로그래밍 언어는 aspect나 객체로 나눌 수 있다.
    1. 관심사의 분리는 중요한 디자인 원칙이다 많은 다른 영역에서도 예를 들어 도시계획, 건축, 정보디자인고 ㅏ같은.
    1. 목표는 더 효율적으로 복잡하고 상호의존적인 시스템을 이해하고, 설계하고, 관리함으로써 함수들이 재사용되고 다른 함수에 독립적으로 최적화하여 다른 함수의 잠재적인 실패로부터 단절되는 것이다.
    1. 일반적인 예시는 방으로 공간을 나눔으로써 하나의 방 안의 활동이 다른 방의 사람들에게 영향을 미치지 않도록 하여 하나의 회로에 있는 스토브를 지키고 다른 곳의 전구를 지켜 스토브의 과로가 전구를 끄지 않도록 하는 것을 포함한다.
    1. 방으로 든 예시는 캡슐화를 보여준다. 방 안의 정보, 얼마나 어지러운지, 다른 방에서는 이용할 수 없다. 즉 문과 같은 인터페이스를 통해서를 제외하고.
    1. 회로로 든 예시는 하나의 모듈 안에서의 활동은, 전기의 소비자가 함께하는 회로가 붙은 (?), 다른 모듈의 활동에 영향을 미치지 않아서 각각의 모ㅇ듈이 다른 곳에서 어떤 일이 일어나는지 신경쓰지 않는다.

이상적으로 개발자들은 집중할줄 알아야 한다 세가지 업무 중에서 첫 번째 것에. ( 무엇이 계산되어져야 하는가 ). 그 뒤에 작은걸로 쪼개는 것, 연산 중에 메모리를 관리하는 것, 등에 주의를 빼앗기지 말고, 더 administrative한 업무. 명확히 administration은 중요하지만 주요 업무로부터 그것을 분리함으롰?ㅓ 우리는 더 신뢰할 수 있는 결과를 얻을 수 있다. 또한, 우리는 프로그래밍 문제를 더 쉽게 만들 수 있다. admin의 많은 것을 자동화 함으로써.

관심사의 분리는 다른 장점들도 가지고 있다. 예를 들어서 프로그램이 ㅈ증명하는 것이 훨씬 더feasible하게 된다. 절차의 디테일과 메모리 관리가 프로그램에서 부재할 때. 게다가 무엇이 연산되어져야 하는가에 대하 ㄴ설명은 그러한 디테일한 스텝바이 스텝 설명 어떻게 해야되는지와 같은 것들로부터 자유로워져야한다. 만약 그것들이 다른 기계 구조와 평가되어져야 한다면.
스토어에 잇는 데이터 객체에 작은 변화의 시퀀스는 매우 평행한 기계가 기계전반에 걸쳐 분포된 수천개의 프로세서와 함께 사용될 때, 어떻게 무언가를 연산해야 하는가에 대한 부적절한 설명일 수 있다.

admin측면을 자동화하ㅡㄴㄴ 것은 언어를 실행하는 것이 그것들을 다루어야 한다는 것을 의미하지만 그 또는 그녀는 훨씬 더 많은 기회가 잇다. 매우 다른 연산의 매커니즘의 사용을 해야한다는 다른 기계 구조에서

1. 적용
    1. 레이어드 아키텍쳐
        1. 기준 : 사용자와의 거리
        1. 예시 :
            1. 스위치 - 사람이 직접 누름 (스위치 온 오프만 해여)
            1. 모터 - (전류가 흐르면 돈다)
            1. 바퀴 - 돌아가기만 해여
        1. input, process, output
        1. what's your name? => input => process "hello" + [input] => print output;
        1. greeting,
        1. MVC => Model = Process / View => Output / Controller => input
    1. Flux Architecture
        1. mvc의 대안이다. two-way binding을 하는 framework가 많았어서 생김
        1. 둘이서 왔다갔다 하지말고 단방향으로만!
        1. action - event listner 같은 객체(이벤트/메시지) dispatch event 브라우저에서 지원하는 것
        1. dispatcher - 여러 스토어 중 적절한 store로 action을 전달, 메세지 브로커와 유사하다
        1. store - 여러개 있음, 받은 Action에 따라 상태를 변경하고 상태 변경을 알린다.
        1. View - store의 상태를 반영 - action을 만듦 
    1. 리덕스는 단일 스토어를 사용함으로써 더 단순한 그림을 제안한다.
        1. action = store = value
        1. action을 어떻게 표현하느냐가 사용성에 큰 차이를 만든다 하지만 상태를 유아이에 반영하는 방법은 모두 동일하다.
        1. model = process = reducer / view = output = react / controller = input = action + dispatch

### External Store

옛날에는 forceUpdate가 있었는데 useReducer를 쓰라고 되어있음. useReducer란? => setState가 내부적으로 사용하는 함수인데, 거의 같은거라고 보시면 돼요. 어떤식으로 세부적으로 처리되는지가 정의되어있는거라고 보시면돼요. 새로운상태로 바꿔주는 이게 리듀서거든요!

```tsx
function reducer(state) {
    return {...state, x: state.x + 1 };
}

function Counter() {
    const [, forceUpdate] = useReducer(reducer, { x: 0 });
}
```

```tsx
import {useState} from 'react';

export default function useForceUpdate() {
    // Const [state, setState] = useState(0);
    const [, setState] = useState({});

    const forceUpdate = () => {
        // SetState(state + 1);
        setState({});
        // 객체는 겉보기에는 같아보이지만 사실상 새 메모리의 새 객체이기 때문에,
        // state가 바뀌었다고 인식해서 update가 일어납니다.
        // 이제 state도 필요가 없어졌죠.
    };

	return forceUpdate;
}
```

여기서 forceUpdate라는 함수가 계속 새롭게 정의됩니다. 
불필요하게 똑같은 함수가 새롭게 정의되니 useCallback으로 항상 같은 함수를 사용하도록 합시다.

```tsx
export default function useForceUpdate() {
    const [, setState] = useState({});
    return const forceUpdate = useCallback(() => setState({}); ,[/*여기가 바뀌면 새로만듦!*/]);
}
```

이렇게 분리를 해준다. 나중에 test를 수행할 때 increase라는 함수가 실행만 되면 된다.
increase라는 함수가 어떤 함수인지는 알 빠 아님

```tsx
import useForceUpdate from '../../hooks/useForceUpdate';

// Business
const state = { // External store의 기본적인 아이디어!
    count: 0,
};

const increase = () => {
    state.count += 1;
};

// Ui
export default function Counter() {
    const forceUpdate = useForceUpdate();

    const handleClick = () => {
        increase();
        forceUpdate();
    };

    return (
        <div>
            <p>{state.count}</p>
            <button type='button' onClick={handleClick}>
                increase
            </button>
        </div>
    );
}
```

끝
