# REPL(Read-eval-print-loop)란?

- `Read` 입력
- `Eval(evaluation)` 처리
- `Print` 출력
- `Loop` 반복

풀어서 정리하면 사용자가 특정 코드를 입력 시 그 코드를 처리하고 결과가 바로 출력되는 과정을 반복하는 것이다. 이것을 예제로 대입해보자.

1. `Read`: 값을 입력 받아 JavaScript 데이터 구조로 메모리에 저장합니다.
2. `Eval(evaluation)`: 데이터를 처리 합니다.
3. `Print`: 결과를 출력합니다.
4. `Loop`: 반복합니다.

# TypeScript

## Interface vs Type

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

[TypeScript 핸드북 나만의 패러프레이징(Everyday Types)](https://otterbox.notion.site/Everyday-Types-775ef96c4a964d0fa298024627659174)

## 타입 추론

명시적인 타입 표기가 없을 때 타입 정보를 제공하기 위해 사용되는 것이다. 즉, `TypeScript`는 자동적으로 타입을 추론하여 알맞는 타입을 결정한다.

```typescript
let boolean = true; // type: boolean
let x = 3; // type: number
const arr = [1, 2, 3] // type: number[]
const tuple = [true, 10] // type: (boolean | number)[]
```

위 예제 처럼 만약 각자의 타입에 맞지 않게 값을 할당하려고 하면 에러가 발생한다. 타입은 보통 몇 개의 표현식(코드)를 바탕으로 타입을 추론하는데, 가장 근접한 타입을 `Best Common Type(최적 공통 타입)` 이라고 부릅니다.

위 예제 중 tuple을 사용한 예제로 `Best Common Type(최적 공통 타입)` 예를 들어보겠습니다.

```typescript
const tuple = [true, 10];
```

위 변수 `tuple`의 타입을 추론하려면 각 배열 요소의 타입을 봐야하는데, 타입은 크게 `number`와 `boolean`으로 구분됩니다. 여기에서 배열에 사용된 요소들의 타입을 각각 추론하여 유니온 타입으로 만들어 내는 방식을 `Best Common Type(최적 공통 타입)`라고 부릅니다.

## Union Type vs Intersection Type

### Union Type

서로 다른 두 개 이상의 타입들을 사용하여 만드는 것으로 조합에 사용된 타입 중 무엇이든 하나의 타입을 가질 수 있습니다.

```jsx
function printId(id: number | string) {
  console.log("Your ID is: " + id);

 /*
  위에서 유니언 타입으로 number와 string을 지정하였는데,
  string에서만 유효한 메서드를 사용할 수 없습니다.
 */
 console.log(id.toUpperCase()); // 오류

 /*
  만약 억지로 쓰고 싶다면 typeof 연산을 사용하여 체크 후 사용할 수 있습니다.
 */
 if (typeof id === "string") {
    // 이 분기에서 id는 'string' 타입을 가집니다
    console.log(id.toUpperCase());
  } else {
    // 여기에서 id는 'number' 타입을 가집니다
    console.log(id);
  }
}

printId(101); // 성공
printId("202"); // 성공
printId({ myID: 22342 }); // 오류
```

### Intersection Type

`interface` 를 사용하면 다른 유형을 확장하여 새로운 유형을 만들 수 있습니다. 기존 객체 유형을 결합하는데 사용되는 `교차 유형`으로 보면 되며 `&` 연산자를 사용하여 정의합니다. (**`교집합 타입 설정`**)

```tsx
interface Colorful {
  color: string;
}
interface Circle {
  radius: number;
}
 
type ColorfulCircle = Colorful & Circle;

function draw(circle: ColorfulCircle) {
  console.log(`Color was ${circle.color}`);
  console.log(`Radius was ${circle.radius}`);
}

draw({ color: "blue", radius: 42 }); // Success
```

### 💡 `Union Type`, `Intersection Type` 둘의 차이점

A타입과 B타입이 있을 때를 가정하면,

#### `Union Type`

`A | B` 또는(`or`)으로 A 타입, B 타입 둘 중 하나

#### `Intersection Type`

`A & B` 합집합(`And`)으로 A 타입이면서 B 타입

## Optional Parameter

`?` 로 표시함으로 선택적 매개변수를 만들 수 있다.

```tsx
function f(x?: number): void {
  // ...
}
f(); // OK
f(10); // OK
f(undefined); // OK

/*
 매개변수 타입이 number로 지정되어 있지만 명시되지 않은 매개변수는 undefiend가
 되기 때문에, x 매개변수는 실질적으로 number | undefiend 타입이 될 것이다.
*/
```

**콜백 함수에서 선택적 매개변수**

선택적 매개변수 및 함수 타입 표현식에 대해 알게 되면, 콜백을 호출하는 함수를 작성할 때 잦은 실수들이 발생한다.

```tsx
function myForEach(arr: any[], callback: (arg: any, index?: number) => void) {
  for (let i = 0; i < arr.length; i++) {
    // 오늘은 index를 제공하고 싶지 않아
    callback(arr[i]);
  }
}

myForEach([1, 2, 3], (a) => console.log(a));
myForEach([1, 2, 3], (a, i) => console.log(a, i));

/*
 위 함수의 의도는 위 두 호출 모두 유효하기를 바래서 사용했지만,
 의미하는 바는 callback이 하나의 인수로 호출될 수 있다 라는 이유가 되기 때문에
 TypeScript는 이러한 의미를 강제하여 실제로 일어나지 않게 에러를 발생시킨다.
*/
```

위 이야기는 즉 기존 JavaScript에서 매개변수로 지정한 것보다 많은 인수를 전달하여 호출 시 남은 인수들은 단순히 무시된다. TypeScript도 마찬가지 방식으로 동작한다고 보면 된다. 같은 타입을 가진 매개변수가 더 적은 함수는 더 많은 매개변수가 있는 함수를 대체할 수 있다.

> 💡 콜백에 대한 함수 타입을 작성할 때, 해당 인수 없이 호출할 의도가 없는 한, 절대로
선택적 매개변수를 사용하지 말자!

[TypeScript 핸드북 나만의 패러프레이징(More on Functions)](https://otterbox.notion.site/More-on-Functions-f5087afe3f884f2f8f873ea4e89699f3)
