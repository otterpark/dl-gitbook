# REPL, TypeScript

## REPL(Read-eval-print-loop)란?

- `Read` 입력
- `Eval(evaluation)` 처리
- `Print` 출력
- `Loop` 반복

풀어서 정리하면 사용자가 특정 코드를 입력 시 그 코드를 처리하고 결과가 바로 출력되는 과정을 반복하는 것이다. 이것을 예제로 대입해보자.

1. `Read`: 값을 입력 받아 JavaScript 데이터 구조로 메모리에 저장합니다.
2. `Eval(evaluation)`: 데이터를 처리 합니다.
3. `Print`: 결과를 출력합니다.
4. `Loop`: 반복합니다.

## TypeScript 

### Interface vs Type

`interface 확장하기`

```jsx
interface Animal {
  name: string
}

interface Bear extends Animal {
  honey: boolean
}

const bear = getBear()
bear.name
bear.honey
```

기존 interface에 새 필드 추가가 가능하다. (`확장 가능`)

```jsx
interface Window {
  title: string
}

interface Window {
  ts: TypeScriptAPI
}

const src = 'const a = "Hello World"';
window.ts.transpileModule(src, {});
```

`type 확장하기`

```jsx
type Animal = {
  name: string
}

type Bear = Animal & {
  honey: Boolean
}

const bear = getBear();
bear.name;
bear.honey;
```

type은 생성 된 이후 달라질 수 없다.(`확장 불가능`)

```jsx
type Window = {
  title: string
}

type Window = {
  ts: TypeScriptAPI
}

 // Error: Duplicate identifier 'Window'.
```

- 타입 별칭은 선언 병합에 포함될 수 있지만, 인터페이스는 포함될 수 있습니다.
- 인터페이스는 오직 객체의 모양을 선언하는 데에만 사용되며, 기존의 원시 타입에 별칭을 부여하는 데에는 사용할 수 없습니다.
- 인터페이스 이름은 항상 있는 그대로 오류 메시지에 나타납니다.
(인터페이스가 이름으로 사용되었을 때)

> 개인적인 선호에 따라 `interface` 또는 `type` 을 선택할 수 있지만, 코드가 조금 더 명시적이고 유연한 `interface` 를 사용하고 이후 문제가 발생 했을 시 `type` 을 사용하면 좋다.

[TypeScript 핸드북 나만의 패러프레이징](https://otterbox.notion.site/Everyday-Types-775ef96c4a964d0fa298024627659174)


    - 타입 추론
    - Union Type vs Intersection Type
    - Optional Parameter