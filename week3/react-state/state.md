# React State

일반적으로 컴포넌트의 내부에서 변경 가능한 데이터를 관리해야할 때 사용한다. `Props`의 특징은 컴포넌트 내부에서 값을 바꿀 수 없다는 것인데, 값을 바꿔야 하는 경우가 존재하며 이럴 때 `State`를 사용한다. 값을 저장하거나 변경할 수 있는 객체로 보통 이벤트와 함께 사용된다.

- 컴포넌트에서 동적인 값을 상태(`State`)라고 부르며, 동적인 데이터를 다룰 때 사용된다.

```tsx
import { useState } from "react";

const App = () => {
    const [value, setValue] = useState(초기값);
    return ...
}
```

- `State` 값을 변경하기 위해서는 무조건 `setState` 함수를 이용한다.
- `State` 값을 임의로 변경해서는 안 된다.