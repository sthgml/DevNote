# useRef

컴포너늩 만들어지고 없어지고 버튜얼 돔으로 드어갔던 요소가 사라지는 그동안에 유지가 되는 객체예여 다른걸로하면 바뀔 수가 ㅇㅆ는데 얘는 유지가 돼요

객체 자체가 값은 아니에요 참조하기 위한 객체예요. 앱에서 먼가를 쓰려고해요. ㅇ리가 ㅣ런것들은 상태잖아요. 값을 유지를 하고싶어요 먼지 모륷지만 ㄱef 이렇게 만들었어요. ㄱef는 계속 유기자 된 상태에서 ㅊonstfㅗ 하면 ref를 몹사꾼다 이런 ㅇ/ㅒ기를 하지만 ㄱef의 ㅍalue 는 바꿀 수 있어요. ㅅimer controller를 여러개  만들엇다고 해바여 내것만 키우고 싶어요. 각자가 useState

useEffect 안에서 state 갖고 오려고 하면 useEffect가 호출된 그 순간의 값을 갖고 오는데, 만약 useEffect가 좀 오래 실행되고 (비동기적으로) 값은 실시간 값을 필요로 한다면 useRef 를 사용해야함! 참조하기 위한 객체니깐 실시간으로 그 값을 참조해서 가지고 올 수 있어요.

## customHook

customHook은 어떨 때 사용하냐면 함수 뽑아내는 거랑 똑같은데 fetch 를 통해서 data 를 불러온다고 했을 때,
export default useFetchAPI() {
const [products, setProducts] = useState([]);
const fetchData = async () => {
  const response = await fetch("http://localhost:3000");
  const data = await response.json();
  setProducts(data);
}
return products
}
이렇게 하면 사실 이 바깥에서는 setProducts 를 쓸일이 없기 때문에 깔끔쓰 하지만 여전히 반환받은 products값은 state이기 때문에 바뀌면 컴포넌트 리렌더링 됨!

Hook 의 규칙

1. Function 컴포넌트 안에서만 호출
1. Function 컴포넌트의 최상위에서만 호출

끝
