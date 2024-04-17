# createNode 함수에 try Catch 사용 시 cancelled 누적 에러

새로고침 할 때마다 cancelled error가 딱 두 배씩 늘어 
나갓다 들어오면 다시 돌아옴

왜지? 단순히 try catch가 문제가 아닐 것 같아


![맨 처음](/99_images/240417_try_catch_cancelled_누적/image-2.png)
![새로 고침 한 번](/99_images/240417_try_catch_cancelled_누적/image-3.png)
![새로 고침 두 번](/99_images/240417_try_catch_cancelled_누적/image-4.png)
![새로 고침 세 번](/99_images/240417_try_catch_cancelled_누적/image-5.png)
![새로 고침 네 번](/99_images/240417_try_catch_cancelled_누적/image-1.png)

와..진짜 감도 안잡혀 뭐지............??

일단 try catch에 대해서 공부..

try catch는 run-time error만 잡아낼 수 있음. (예외)
아예 런이 되지 않는 에러는 try catch가 잡아낼 수 없음
이를 parse-time error라고 함.

try catch는 동기적으로 동작하여 schecule 된 코드에서 발생한 예외는 try catch에서 잡아낼 수 없음
ex. 

```js
try { 
  setTimeout(function() {
  noSuchVariable;
}, 1000)
} catch {

}
```

엔진이 try catch를 떠난 다음에야 익명함수가 실행되므로 예외를 잡아낼 수 없음

새로고침할 때마다 두 배 씩 늘어나는 걸로 봐서 노드가 누적되는 것 같아서
```js
  useEffect(() => {
    return () => {
      editor?.destroy();
    }
  }, [])
```
destroy함수로 editor가 unmount될 때 editor를 파괴시켜줬음

일단 uncaught cancelled error는 process함수에 있는 reset함수때문에 발생하는 것이기 때문에 이게 connection이 생길때마다 트리거되는 process함수와 관련된 것이라는 것을 알 수 있음.

![alt text](/99_images/240417_try_catch_cancelled_누적/image-6.png)

저장된 내역을 console로 뽑아보니, 새로고침 할 때마다 connection이 중복되어서 계속 생성되고 있었음. 그래서 딱 uncaught error도 두 배씩 늘 고 있었던 것.

근데 왜..??

try catch만 제외해봤을 때 동일한 에러가 재현되지 않는 것을 확인했다.

새로고침과 try catch의 합작 ㅠㅠ

와 이거 try catch 아닌디 ㅠㅠㅠㅠ 뭐지잉

새로 고침 -> getCanvas 분기는?

try catch에서 catch에서 이미 노드가 다 추가되었다고 뜸
그 이후에 connection을 중복해서 생성하고 있음!
=> getCavas로 들어감 (be에 저장된 json으로 만드는 코드)

setInit이 두번 실행되어서 getCanvas를 두 번 실행시키니까, BE에서 받아온 Json을 토대로 노드랑 connections을 생성하는 함수도 두 번 실행되었는데, 노드는 노드 id도 같이 전달받아가지고 이미 id가 있는 노드면 추가할 때 rete자체에서 error를 생성하여서 중복되는 것을 방지해주었지만, conns는 애초에 저장할 대 conns id 도 같이 받질 않아서 다시 생성할 때 중복인지 체크할 id가 없었음.

그래서 두 번 실행되면 두 번 실행 되는 대로 conns를 생성해주고 있었던 것!!!!

![useEffect의 의존 배열에 editor가 변함에 따라 두 번 실행되었음 (처음에 없을 때, createEditor로 생겼을 때)](/99_images/240417_try_catch_cancelled_누적/image-9.png)
![conneciton이 두 배가 됨](/99_images/240417_try_catch_cancelled_누적/image-10.png)
![editor가 생겼을 때 한 번만 실행되도록 수정](/99_images/240417_try_catch_cancelled_누적/image-11.png)
![한 번만 시행되고 난 후에도 두배가 되지 않음](/99_images/240417_try_catch_cancelled_누적/image-12.png)

![createNodesByJson, createConnsByJson 코드!!](/99_images/240417_try_catch_cancelled_누적/image-13.png)