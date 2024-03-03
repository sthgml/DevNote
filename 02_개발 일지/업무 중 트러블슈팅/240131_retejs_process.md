# retejs 사용 중 겪은 어려움

## 불필요한 process 함수 실행

💡 렌더 노드 수 많아지면서 Uncaught Error 로 인해 서비스 멈추는 문제 해결

1. Uncaught Error: cancelled 10만 번 호출
    1. 캔버스 누를 때마다: 
        1. update (process 함수 = dataflow  engine reset후 노드 간 data 전달 (fetch) ) → onChange (control 외관 update) 외관이 바뀐 게 없어서 onChange를 할 필요가없는데 setData에 넣어줬던 onChange 함수에서 오류가 남
    2. 처음에 렌더 될 때:
        1. 노드 렌더할 때 커넥션이 100+ 개 생겨나는데 그거 생길 때마다 process()가 실행되면서 process가 에디터 전체에서 한 번만 생기면 되는데, 노드 마다 개별적으로 실행되니까 이미 실행되고 있어서 cancelled 되는 것 같음 

## 임의로 만든 데이터 구조로 부터 노드를 생성하는 함수 제작

💡 createByDataStructure 함수 에러 원인 파악

![Untitled](/99_images/createByDatastructure_01.png)

- 노드를 모두 연결한 후에 데이터 구조를 viewer노드에서 받아서 mockDataStructure에 저장한 다음에 버튼으로 뽑았더니 제대로 렌더 됨
- 모든 노드가 순서대로 렌더됨을 확인함

![Untitled](/99_images/createByDatastructure_02.png)

![Untitled](/99_images/createByDatastructure_014.png)

- BE에서 받은 데이터구조는 중간의 cat layer가 datset위치에 가있고, cat layer에 또 앞의 노드들이 input으로 담겨있음을 확인

1. 전 모델 플로우랑 비교 - (12:30pm)
    1. 목표: 모델이 달라졌는지 확인
        1. prevModelFlow를 node에 따로 저장해놓던지
        2. api 통신 두번 해서 같은지 비교하던지 (너무 통신낭비 아닌가?)
    2. 문제 원인:
        1. 그냥 setState(prev⇒any)로 못하는 이유 : 노드 작업하려면 다른 노드 클릭해야됨 → 선택된 노드 바뀜 → 패널 바뀜→ 뷰어패널 리렌더링 됨 → setState 초기화 된 다음에 노드에 저장된 값 갖고 옴. → 노드에는 이미 변화된 modelFlow가 저장되어 있음 → 바뀌었는지 알 수 없음;
    3. 의문
        1. ctrl.nodeId 는 의존성배열에서 work (O)
        2. ctrl.modelflowId 는 doesn’t work
            1. ++ 노드 아이디가 바뀐건 알 수 잇음 왜냐면 노드를 선택하면서 ctrl 이 바뀌어서 전달되기 때문
            2. 하지만 노드 아이디도 바뀌지 않고 리렌더링도 되지않은 상태 즉 모델플로우가 변경되었다는 이벤트는 감지할 수가 없음 
            3. 이미 ctrl은 그게 바뀌기 전에 전달 되고 다시 전달되지 않기 때문에!
            4. props로 전달되고 있긴 하지만 객체라서 메모리값을 참조해서 비교하기 때문에 바뀌었다고 감지하지못함
2. data 함수 setValue 할때마다 실행돼서 panel 렌더링 될때마다 input 개수 * n 번 실행됨 
    1. 근디 첨 실행되는거 말고 나머지는 다 input값을 이전 것을 가지고 있음 호출되었던 시점이 언제지 ???
3. MlopsCodeEditor
    1. React.memo() 남용으로 인한 props 전달 오류남
    2. 한 번 정리할 필요가 있어보임 ;
    3. update code api가 안됨