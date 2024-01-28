# Navigation

## 학습 키워드

- Web APIs - History
- React Router - NavLink, Link, Navigate, useNavigate

### history.pushState()

url에 /#/ 혹은 /#!/ 을 하면? 이동은 하지 않지만 전체 리로드가 되게 함? (새로고침??)

NavLink ==> Link랑 같은데 해당 링크로 이동하면 이 NavLink 컴포넌트에 active 클래스가 붙음

Navigate, useNavigate를 활용해서 리디렉션 구현 가능

```tsx
function Logout() {
  useEffect(() => {
    // logout 로직 구현
  }, [])
  return <Navigate to="/" element={<HomePage />}>
}
```

or

```tsx
const navigate = useNavigation();
...
<button type="button" onClick={() => navigate("/");}> logout </button>
```
