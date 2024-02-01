# props와 attrs

## 👉 [강의 보기-1]

## 👉 [강의 보기-2]

## 학습 키워드

- props
- attrs

```ts
type Props = {
  type: 'button' | 'submit' | 'reset';
  active: boolean;
}

const Button = styled.button.attrs<Props>(()=>{})<Props>`
  color: #fff;
  background-color: #000;
  ${//여기서 props 받아서 쓸 수 있음
    (props) => (
      props.active ? `
      border: 1px solid blue;
      ` : `
      border: none;
      `
    )
  }
`
```
