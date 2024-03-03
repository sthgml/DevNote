# Modal Open에 따른 이 외 컴포넌트 리렌더링 최소화

1. 문제가 되는 현상:
    1. template Modal 이 열릴때마다 화면 내 모든 component가 리렌더링
    2. Memoized를 한 CanvasHeader, menu 모두 포함
2. 문제 원인 파악:
    1. modal이 열리는 것은 templateModal: boolean 상태로 control
    2. 하지만, 해당 jsx 파트를 주석처리해도 리렌더링
    3. ⇒ 모달이 열리는 상위 컴포넌트가 아니라 클릭할 때마다 실행되는 함수에 문제가 있다고 판단
    4. onClick 함수가 적용된 컴포넌트는 button이 아니라 Link 즉 anchor 태그 였고 recommended Model List를 띄우는 경우에 타겟 url이 빈 문자열로 설정되어 리렌더링이 아닌 페이지 전체가 리로드 되는 것이었음
    5. ⇒ anchor 태그를 modal open button겸 link로 사용한 것이 문제 원인
3. 해결:
    1. modal open과 link로 사용할 경우 분기를 만들어
    2. setState함수가 실행되는 분기에는 e.preventDefault()실행해 anchor기능이 실행되는 것을 막음