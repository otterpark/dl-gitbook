# React Element

React Element에 대해 알아보자!

## React Element란?

Element는 React의 가장 작은 단위이며, Browser DOM Element와 달리 일반 객체이며, React DOM은 React Element와 일치하도록 DOM을 업데이트 합니다.
> React Component와 헷갈리면 안 되는데, Element는 Component의 `구성 요소` 입니다. 

## React createElement(Element 생성)

React의 Element를 `Type`, `props`, `children` 값과 함께 생성하는 함수이다.

```jsx
import { createElement } from 'react';

function Greeting({ name }) {
  return createElement(
    'h1',
    { className: 'greeting' },
    'Hello'
  );
};
```

### 1. `파라미터`

#### `Type`

`Type` 인수는 유효한 React component 타입이어야 합니다.

예) `div`, `span` 또는 `React Component`(함수, 클래스, Fragment)

#### `props`

`props` 인자는 객체이거나 `null`이어야 합니다. React는 전달한 프로퍼티와 일치하는 프로퍼티를 만든 엘리먼트를 생성합니다. `props` 객체의 `ref`와 `key`는 특수한 것이므로 반환된 엘리먼트에서 `element.props.ref`와 `element.props.key`로 사용할 수 없습니다. (`element.ref`와 `element.key`는 사용 가능)
> 만약 값을 주지 않을 시 `null`을 전달하게 되며 빈 객체와 동일하게 처리 됩니다.

#### `...children`(optional)

자식 노드를 선택적으로 넣을 수 있으며, React nodes, elements, strings, numbers, empty nodes(null, undefined, true, false), 배열을 포함한 React nodes를 포함할 수 있다.

### 2. `Return`

`createElement`는 프로퍼티인 `type`, `props`, `ref`, `key`를 반환합니다.

- `type` - `props`로 넘긴 type을 반환
- `props` - `props`로 넘긴 프로퍼티 중 `ref`와 `key`를 제외한 프로퍼티입니다.

  >`type.defaultProps`를 설정하면, `undefined`로 인해 생기는 오류를 방지할 수 있다.

- `ref` - `ref`로 넘긴 값(값이 없을 시 `null`)
- `key` - `key`로 넘긴 값(값이 없을 시 `null`)

### `주의사항`

- React 엘리먼트와 프로퍼티는 `불변(immutable)`으로 취급해야하며, 생성 후 절대 그 값이 변경되어서는 안 됩니다. `React`에서는 이를 강제하기 위해 `return` 된 엘리먼트와 그 프로퍼티를 고정합니다.

- JSX를 사용 시 태그를 모두 대문자로 시작해야 사용자 정의 컴포넌트를 렌더링할 수 있습니다.
  > `createElement(Something)` => `<Something />`

- 만약 `파라미터` 중 `...children` 부분에서 자식을 여러 개 넘길 때 하나의 전체 배열로 묶어서 전달해야합니다.
  > createElement('div', {}, `child1, child2, child`3) => createElement('div', {}, `childList`) \
  >  여기서 `childList` = [child1, child2, child3]
