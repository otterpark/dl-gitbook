# usestore-ts

`React state management library` 이다.

> 기본적인 `Typescript`에 대한 이해가 있으면 좋다.

만약, `usestore-ts`를 사용한다면 내부적으로 어떤 동작을 하는지와 어떤 방식으로 작동하는지에 대해 설명할 수 있어야 한다.

## 설치

```bash
npm install usestore-ts
```

## TypeScript Config 설정

`tsconfig.json`에 아래 설정을 활성화 해준다.

```json
"experimentalDecorators": true,
"emitDecoratorMetadata": true,
```

## 예시

```tsx
import { Store, Action, useStore } from 'usestore-ts';

@Store()
class CounterStore {
  count = 0;

  @Action()
  increase() {
    this.count += 1;
  }

  @Action()
  reset() {
    this.count = 0;
  }
}

const counterStore = new CounterStore();

export default function Counter() {
  const [{ count }, store] = useStore(counterStore);

  return (
    <div>
      <p>
        Count:
        {' '}
        {count}
      </p>
      <p>
        <button type="button" onClick={() => store.increase()}>
          Increase
        </button>
        <button type="button" onClick={() => store.reset()}>
          Reset
        </button>
      </p>
    </div>
  )
}
```