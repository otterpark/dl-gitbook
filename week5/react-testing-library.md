# React Testing Library

**Facebook에서 공식적으로 사용을 권장하는 리엑트 테스트 도구**이다. 이 라이브러리를 통해 실제 사용자가 사용하는 것처럼 테스트를 작성할 수 있도록 설계되어있다.

React Testing Library의 주요 목적은 사용자가 사용하는 방식으로 컴포넌트를 테스트하여 테스트에 대한 신뢰도를 높이는 것이다.

자주 사용되는 API에 대해 간단히 알아보자.

## render

`document.body`에 추가되는 컨테이너에 렌더링합니다.

```tsx
function render(
  ui: React.ReactElement<any>,
  options?: {
    // 잘 사용안되니 사용 유의
  },
): RenderResult
```

## `render` Result

`render` 메소드는 몇 가지 프로퍼티를 가진 객체를 반환합니다.

### `...queries`

렌더링의 가장 중요한 기능은 DOM 테스팅 라이브러리의 쿼리가 기본값이 `document.body`인 `baseElement`에 바인딩된 **첫 번째 인수와 함께 자동으로 반환**된다는 점입니다.

```tsx
const {getByLabelText, queryAllByTestId} = render(<Component />)
```

### `container`

렌더링된 React Element의 포함하여 DOM 노드(`ReactDOM.render`를 사용하여 렌더링됨) div입니다. 이것은 일반 DOM 노드이므로`container.querySelector` 등을 호출하여 자식들을 검사할 수 있습니다.

- 렌더링된 React Element의 루트 엘리먼트를 가져오려면 `container.firstChild`를 사용한다.
- `RootElement`가 `Fragment`인 경우 컨테이너 안에 `container.firstChild`는 첫 번째 자식만 가져오고 `Fragment`는 가져오지 않는다.

### `baseElement`

`container`에서 React 엘리먼트가 렌더링되어 포함되는 DOM 노드입니다. 렌더링 옵션에서 `baseElement`를 지정하지 않을 시 기본 값은 `document.body`가 됩니다.

### `debug`

이 메서드는 `console.log(prettyDOM(baseElement))`의 간단한 표현이다.

> 💡 `screen.debug`를 사용하는 것을 권장!

### `rerender`

`Props` 업데이트를 수행하는 컴포넌트를 테스트하여 `Props`가 잘 업데이트 되었는지 확인하는 것이 좋습니다. 하지만 테스트에서 렌더링된 컴포넌트의 `Props`를 업데이트하고 싶다면 이 함수를 이용해 렌더링된 컴포넌트 `Props`를 업데이트할 수 있습니다.

### `unmount`

렌더링된 컴포넌트의 마운트가 해제됩니다. 페이지에서 컴포넌트가 제거되었을 때 어떤 일이 발생하는지 테스트할 때 유용하다.

### `cleanup`

렌더링으로 마운트된 React 트리를 마운트 해제합니다.
