# props와 attrs

## props

스타일이 지정된 컴포넌트의 템플릿 리터럴에 함수에 넘기면 prop 기반으로 사용할 수 있습니다.

```tsx
const Button = styled.button<{ $primary?: boolean; }>`
  /* Adapt the colors based on primary prop */
  background: ${props => props.$primary ? "#BF4F74" : "white"};
  color: ${props => props.$primary ? "white" : "#BF4F74"};

  font-size: 1em;
  margin: 1em;
  padding: 0.25em 1em;
  border: 2px solid #BF4F74;
  border-radius: 3px;
`;

render(
  <div>
    <Button>Normal</Button>
    <Button $primary>Primary</Button>
  </div>
);
```

## attr

렌더링된 컴포넌트 또는 요소에 일부 `props`만 전달하는 불필요한 래퍼를 피하려면 .`attrs` 생성자를 사용할 수 있습니다. 이 생성자를 사용하면 컴포넌트에 추가 프로퍼티(또는 "속성")를 첨부할 수 있습니다.

여기서는 입력 컴포넌트를 렌더링하고 몇 가지 동적 및 정적 type을 첨부합니다.

```tsx
const Input = styled.input.attrs(props => ({
  // we can define static props
  type: "text",

  // or we can define dynamic ones
  $size: props.$size || "1em",
}))<{ $size?: string; }>`
  color: #BF4F74;
  font-size: 1em;
  border: 2px solid #BF4F74;
  border-radius: 3px;

  /* here we use the dynamically computed prop */
  margin: ${props => props.$size};
  padding: ${props => props.$size};
`;

render(
  <div>
    <Input placeholder="A small text input" />
    <br />
    <Input placeholder="A bigger text input" $size="2em" />
  </div>
);
```