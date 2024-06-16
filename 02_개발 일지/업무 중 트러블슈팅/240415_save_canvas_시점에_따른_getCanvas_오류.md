# trainer 노드가 생기는 문제

## 문제 상황 (현상)

0. unprocessable entity 오류가 뜨길래 saveCanvas 시점을 바꿈 - loading 상태가 변경되고 그게 false이면 1초 뒤에 5초 간격으로 저장하는 interval을 설정하도록 함

1. 의문의 trainer 노드 하나가 저장된 workspace에 추가되어 렌더됨
2. 이미 저장된 workspace를 다시 들어가보면 trainer 노드 하나만 남아있음

3. interval로 저장되는 params, title, settings가 setInterval 시점에 머물러있음 (실시간 반영 안됨)
4. setInit 함수가 두 번 실행됨

## 원래 의도

1. saveCanvas를 interval로 5초에 한 번씩 진행
1. 첫 workspace 정보 받아오고 (get캔버스 든, createBy데구 든) 난 직후에 save한 번 진행되도록

## 원인

1. saveCanvas가 컴포넌트가 언마운트 된 이후에도 실행됨
    1. setInterval이 clear가 안되었음
    1. return함수는 unmount되면 실행되는게 아니고, deps 파람의 값이 변경 되기 전에 실행되는 함수임. 근디 로딩 값이 바뀌지 않으니까 cleanup함수가 실행되지 않았던것
    1. unmount가 되어도!
    1. cleanup 함수는 react가 다음 차례의 effect를 실행하기 전에 이전의 렌더링에서 파생된 effect 또한 정리하는 것
    1. [reference 블로그](https://wnsdufdl.tistory.com/454)

## 의문점

1. setInterval을 하더라도 이걸 set 한 시점의 state와 props는 변하지 않아서 반복 실행될 때 실시간 데이터가 반영되지 않는다고 예측했는데 값이 아예 없을 때는 오류가 떴는데 이전에는 실시간 데이터가 반영 되었음 (의존배열을 의도한거였는지?? 잘 설정해놓았었음..!!!)
2. useEffect의 의존성배열에 editor랑 editable이랑 두개 넣은 이유가 뭐였는지? (setInit함수에서 editor를 사용하는 코드가 있어서 editor?. 를 사용하는 경우를 줄이고 싶어서 사용했음)
3. getCanvas실패하고 location.state로 데이터구조 기반으로 노드 생성하도록 분기가 나뉘어 있는데, 여기 분기가 왜 성공하는건지? 왜 실패하는 건지? (undefined가 뜨면 아예 작동을 멈추는데, null이 들어가면 if문은 통과하되, generateNodeByDataStructure 이부분에서 error 뜸)
4. setInit의 useEffect의 의존배열에 editable들어가있음, setInit 안에 setCanvas안에 setEditable있음, setCanvas안에 getCanvas에 setEditable있음, 근데 왜 무한루프 안돌음?? (=> editable이 초기 설정도 true고 setEditable로 바꿔주는 함수도 다 true로 설정하는 함수들이기 때문에 상태가 변경되지를 않음)

## 개선점

1. save를 setInterval한 useEffect의 의존배열을 params, title, settings로 설정 => params, settings, title이 바뀔 때마다 setInterval이 실행되고, 바뀌기 직전에 clearInterval이 실행됨!
1. setInit을 하는 useEffect의 의존배열에 editor와 editable 두 가지가 있는데, editor는 rete가 불러와지면 바로 바뀌기 때문에 저게 설정되는 시점으로 하면 너무 빠르며, 처음 렌더링 된 시점(1), editor가 설정된 시점(2)으로 두 번 실행 됨 (editable은 처음 렌더링 될 때도 true 바꿀 때도 true이기 때문에 렌더링 이후에 바뀌지 않음 => 리렌더링을 유발하지 않음 => editable로 설정한 의존 배열 = 빈 배열로 설정한 것과 마찬가지)