# useSyncExternalStore

`useSyncExternalStore`는 외부 저장소를 구독할 수 있는 React Hook입니다.

```tsx
const snapshot = useSyncExternalStore(subscribe, getSnapshot, getServerSnapshot?)
```

저장소에 있는 데이터의 스냅샷을 반환합니다. 두 함수를 인수로 전달해야 합니다.

- 함수 `subscribe`는 스토어를 구독하고 구독을 취소하는 함수를 반환해야 합니다.
- 함수 `getSnapshot`는 저장소에서 데이터의 스냅샷을 읽어야 합니다.

## Parameters

### `subscribe callback`

단일 인수를 가져와 저장소에 구독하는 함수입니다 . 스토어가 변경되면 제공된 를 호출해야 합니다 callback. 이로 인해 구성 요소가 다시 렌더링됩니다. **`subscribe`함수는 구독을 정리하는 함수를 반환**해야 합니다.

### `getSnapshot`

저장소에서 구성 요소에 필요한 데이터의 스냅샷을 반환하는 함수입니다. 저장소가 변경되지 않은 동안 에 대한 반복 호출은 `getSnapshot` 동일한 값을 반환해야 합니다. 저장소가 변경되고 반환된 값이 다른 경우(`Object.is`를 비교) `React`는 구성 요소를 다시 렌더링합니다.

### `optional getServerSnapshot`

저장소에 있는 데이터의 초기 스냅샷을 반환하는 함수입니다. 서버 렌더링 동안과 클라이언트에서 서버 렌더링 콘텐츠의 수화 중에만 사용됩니다. 서버 스냅샷은 클라이언트와 서버 간에 동일해야 하며 일반적으로 직렬화되어 서버에서 클라이언트로 전달됩니다. 이 인수를 생략하면 서버에서 구성 요소를 렌더링하면 오류가 발생합니다.

## 예제

`useSyncExternalStore` Hook을 사용해서 `navigator.onLine`을 구독해 브라우저가 실시간으로 온라인인지 오프라인인지 확인할 수 있습니다.

```tsx
import { useSyncExternalStore } from 'react';

function ChatIndicator() {
  const isOnline = useSyncExternalStore(subscribe, getSnapshot);
  // ...
}
```

`getSnapshot`에 브라우저 API에서 현재 값을 넣습니다.

```tsx
function getSnapshot() {
  return navigator.onLine;
}
```

`subscribe` 함수를 구현해야 하는데, 예를 들어 `navigator.onLine` 변경 시 브라우저는 `window` 개체에서 온라인 및 오프라인 이벤트를 실행합니다. 콜백 인수를 해당 이벤트에 구독한 다음 `subscribe`을 정리하는 함수를 반환해야 합니다.

```tsx
function subscribe(callback) {
  window.addEventListener('online', callback);
  window.addEventListener('offline', callback);
  return () => {
    window.removeEventListener('online', callback);
    window.removeEventListener('offline', callback);
  };
}
```

### App.jsx

```tsx
import { useSyncExternalStore } from 'react';

export default function ChatIndicator() {
  const isOnline = useSyncExternalStore(subscribe, getSnapshot);
  return <h1>{isOnline ? '✅ Online' : '❌ Disconnected'}</h1>;
}

function getSnapshot() {
  return navigator.onLine;
}

function subscribe(callback) {
  window.addEventListener('online', callback);
  window.addEventListener('offline', callback);
  return () => {
    window.removeEventListener('online', callback);
    window.removeEventListener('offline', callback);
  };
}

```