
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

#### Note

컨벤션으로써, async trasitions을 사용하는 함수들은 Actions라고 부르기로 했습니다.

Actions는 자동으로 여러분을 위해 제출하는 데이터를 관리합니다.

- 펜딩상태: Actions는 펜딩 상태라는 것을 제공하는데요. 이것은 요청의 시작에서 시작해서 자동으로 마지막 상태 업데이트가 커밋 되었을 때 리셋됩니다.
- 낙관적 업데이트: Actions는 새로운 useOptimistic이라는 훅을 제공합니다. 이걸로 여러분들은 요청이 제출되었을 때, 사용자의 즉각적인 피드백을 확인할 수 있습니다.
- 에러 핸들링: Actions는 에러 관리를 제공해서 여러분들로 하여금 에러 경계를 표시하고 요청이 실패되었을 때, 그리고 revert합니다 낙관적인 업데이트를 그들의 원래 값으로 자동으로
- Forms: 폼태그 요소가 이제 제공됩니다 함수를 액션과 폼액션 프롭스로 전달할 수 있습니다. 함수를 액션 프롭스로 전달하는 것은 액션을 기본으로 사용합니다. 그리고 폼을 자동으로  제출 이후에 초기화 합니다.

Actions의 맨 이를 지음으로써, 리액트19는 useOptimistic을 도입합니다. 낙관적인 상태를 다루고, 새로운 훅인 useActionState를 액션들을 위한 일반적인 경우를 다루기 위해서 도입됩니다. 리액트 돔에서는 우리는 폼태그 액션을 추가합니다. 자동으로 폼을 다루고 form의 상태를 다루기 위해서. 일반적인 케이스들을 폼안의 액션들을 통해서 

리액트 19에서, 위의 예시는 아래와 같이 단순화 시킬 수 있습니다.

```jsx
function ChangeName({name, setName}) {
  const [error, submitAction, isPending] = useActionState(
    async (previousState, fromData) => {
      const error = await updateName(formData.get('name'));
      if (error) {
        return error;
      }
      redirect("/path");
    }

    return (
      <form>
        <input type="text" name="name" />
        <button type="submit" disabled={isPending}>
        Update
        </button>
        {error && <p>{error}</p>}
      </from>
    )
  )
}
```

다음 섹션에서, 우리는 각각의 새로운 액션 기능들을 쪼개보겠습니다.

