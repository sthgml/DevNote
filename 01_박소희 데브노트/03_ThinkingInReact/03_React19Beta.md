
# 1. 리액트 19 BETA

## 1-1. 리액트 19에서 새로워진 것

### 1-1-1. Actions

React apps에서의 일반적인 사용법은 데이터 변형을 실행시키고 나서 그 반응으로 상태를 업데이트 시키는 것입니다. 예를 들어서, 그들의 이름을 변경하기 위해서 사용자가 form을 제출할 때, 당신은 API요청을 만들고나서 응답으로 온 것들을 다룰 것입니다. 과거에는 여러분은 대기중인 상태, 에러, 낙관적인 업데이트 그리고 일련의 요청을 수동으로 관리해야 했습니다. 

예를 들어서, 대기 혹은 에러 상태를 useState로 다룰 수 있었습니다.

```jsx
// As-is
function UpdateName({}) {
  const [name, setName] = useState('');
  const [error, setError] = useState(null);
  const [isPending, setIsPending] = useState(false);

  const handleSubmit = async () => {
    setIsPending(true);
    const error = await updateName(name);
    setIsPending(false);
    if (error) {
      setError(error);
      return;
    }
    redirect("/path");
  }

  return (
    <div>
      <input value={name} onChange={(e)=>{setName(event.target.value)}}/>
      <button
        onClick={handleSubmit}
        disabled={isPending}
      >
        Update
      </button>
      {error && <p>{error}</p>}
    </div>
  )
}
```

React 19 에서, 우리는 상태 변경 과정에서 pending 상태, 에러, form, 그리고 낙관적 업데이트를 자동으로 다루기 위해 async 함수를 사용하기 위한 보조를 추가하고 있습니다.

예를 들어서, pending 상태를 다루기 위해서 useTransition을 사용할 수 있습니다.

```jsx
function UpdateName({}) {
  const [name, setName] = useState('');
  const [error, setError] = useState(null);
  const [isPending, startTransition] = useTransition();

  const handleSubmit = async () => {
    startTransition(async () => {
      const error = await updateName(name);
      if (error) {
        setError(error);
        return;
      }
      redirect("/path");
    })
  }

  return (
    <div>
      <input value={name} onChange={(e)=>{setName(e.target.value)}} />
      <button onClick={handleSubmit} disabled={isPending}>
      Update
      </button>
    </div>
  )
}
```

async 변경은 즉각적으로 isPening state를 true로 만들고, async 요청을 만듭니다 그리고 어떤 transition 이든 그것이 끝난 뒤에 ispending 을 false로 만듭니다. 이것은 데이터가 변경이 되는 동안에도 현재 UI를 반응적이고 상호작용적으로 유지하도록 만들어줍니다.
