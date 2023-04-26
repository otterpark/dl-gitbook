# React Component Props

React 컴포넌트는 `Props`를 사용하여 단방향 바인딩으로 서로 통신합니다. 부모 컴포넌트에서 자식 컴포넌트로 `Props`를 통해 전달할 수 있으며, `Props`는 HTML 속성을 떠올리게 할 수 있지만 객체, 배열, 함수 등 모든 JavaScript 값을 `Props`를 통해 전달할 수 있습니다.

## Familiar props(기존에 정의된 props)

`Props`는 JSX 태그에 전달하는 정보입니다. 각 태그안에 기존에 정의된 HTML 속성들을 `Props`로 전달할 수 있습니다.

```tsx
function Avatar() {
  return (
    <img
      className="avatar"
      src="https://i.imgur.com/1bX5QH6.jpg"
      alt="Lin Lanying"
      width={100}
      height={100}
    />
  );
}

export default function Profile() {
  return (
    <Avatar />
  );
}
```

## Passing props to a component

아래와 같이 부모 컴포넌트에서 `Props`를 전달하여 자식 컴포넌트서 받아 사용할 수 있습니다.

```jsx
export default function Profile() {
  return (
    <Avatar
      person={{ name: 'Lin Lanying', imageId: '1bX5QH6' }}
      size={100}
    />
  );
}
```

`Profile`은 부모 컴포넌트이며, 자식 컴포넌트 `Avatar`에 `Props`로 데이터를 전달합니다.

```jsx
function Avatar({ person = '', size = 100 }) {
  // person and size are available here
}
```

자식 컴포넌트에서 `Props`를 위처럼 받아 사용할 수 있습니다. React 컴포넌트 함수는 하나의 인자인`Props` 객체를 받고 `person = ''` 나 `size = 100`처럼 `Props`에 기본값을 부여할 수 있습니다.

```jsx
function Avatar(props) {
  let person = props.person;
  let size = props.size;
  // ...
}
```

위처럼 절대로 사용하지 말자!

## Forwarding props with the JSX spread syntax

우리는 아래처럼 `Props`로 받은 인자들을 아래 같이 똑같이 자식 컴포넌트로 전달하는 경우가 있습니다.

```jsx
function Profile({ person, size, isSepia, thickBorder }) {
  return (
    <div className="card">
      <Avatar
        person={person}
        size={size}
        isSepia={isSepia}
        thickBorder={thickBorder}
      />
    </div>
  );
}
```

위를 자세히 보면 Profile로 받은 Props를 Avatar에 전체를 그대로 넘겨주고 있습니다. 가독성은 좋아보이지만 간결함이 중요할 때도 있습니다. 아래처럼 `Props` 전체를 넘겨주는 방법도 있습니다.

```jsx
function Profile(props) {
  return (
    <div className="card">
      <Avatar {...props} />
    </div>
  );
}
```

> 단 Spread 구문은 절제해서 상황에 맞게 사용해야한다.

## Passing JSX as `children`

```jsx
<Card>
  <Avatar />
</Card>
```

만약 위와같이 JSX 태그 안에 컨텐츠를 중첩하면 부모 컴포넌트는 해당 컨텐츠를 `children`이라는 `Props`로 받습니다.

```jsx
function Card({ children }) {
  return (
    <div className="card">
      {children}
    </div>
  );
}

export default function Profile() {
  return (
    <Card>
      <Avatar
        size={100}
        person={{ 
          name: 'Katsuko Saruhashi',
          imageId: 'YfeOqp2'
        }}
      />
    </Card>
  );
}
```

## How props change over time(Don't try to `Change Props` Using `State`)

만약 `Clock` 컴포넌트는 부모 컴포넌트로부터 `color`와 `time`의 두 가지 `Props`를 받는다라고 가정해보자

```jsx
export default function Clock({ color, time }) {
  return (
    <h1 style={{ color: color }}>
      {time}
    </h1>
  );
}
```

이 예시는 컴포넌트가 시간이 지남에 따라 다른 `Props`를 받을 수 있음을 표현할 수 있습니다. `Props`는 항상 고정되어 있지 않습니다. 컴포넌트의 데이터를 처음에만 반영하는 것이 아닌 모든 시점에 반영합니다.

근데 `Props`는 변경할 수 없는 `불변성(immutable)`인데 어떻게 변경이 되나?

컴포넌트가 사용자 상호작용이나 새로운 데이터에 대한 응답으로 `Props`를 변경해야 하는 경우 부모 컴포넌트에 다른 `Props`, 즉, 새로운 객체를 전달하도록 `요청`해야합니다. 그럼 이전 `Props`는 버려지고 JavaScript 엔진은 `Props`가 차지했던 메모리를 회수하게 됩니다.

절대 `Props`를 변경하려고 시도하지 마세요. 선택한 색상을 변경하는 등 사용자 입력에 응답해야하는 경우 `State` 설정을 해야하며 자세한 내용은 `State`에서 다뤄보도록 하자.
