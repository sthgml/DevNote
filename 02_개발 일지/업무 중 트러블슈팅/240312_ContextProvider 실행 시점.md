💡 api Unauthorized 오류

1. 우리 서비스는 api를 class로 저장하여 토큰 만료를 default에서 처리하고 이후에 요청을 클래스의 메서드로 처리하는데, 컴포넌트에서 api 호출하는 코드가 있는게 가독성이 안 좋아서 이를 context provider로 분리했던 것이 문제의 원인!
2. context provider는 전체 App.tsx를 감싸고 있기 때문에 로그인 후 token을 로컬 스토리지에 저장하기 전, npm start하는 순간에 api를 생성한다.
3. 즉, context provider에서 생성한 api는 로그인 api의 response로 localStorage에 setItem(’access’)을 하기 전에 getItem(’access’)를 시도했기 때문에,
4. this.acess에 null을 보관하고 있었고,
5. 이는 Expired Token이 아닌 Invalid Token이었기 때문에 token 다시 받아오기 분기에도 들어가지 못하고 아무 작동을 하지 않았던 것
