# React Hook

`React` 혹은 `React 클래스형 컴포넌트`에서 이용하던 코드를 작성할 필요없이 `함수형 컴포넌트`에서 **다양한 기능을 사용할 수 있게 만들어준 라이브러리**이며, `함수형 컴포넌트`에 맞게 만들어진 것으로 `함수형 컴포넌트`에서만 사용 가능하다.

> React 16.8 버전부터 추가되었다.

## React Hooks

### useState()

`useState`는 `컴포넌트에 상태 변수를 추가`할 수 있는 React Hook입니다.

```tsx
const [state, setState] = useState(initialState);
```

### useEffect()

`useEffect`는 `컴포넌트를 외부 시스템과 동기화`할 수 있는 React Hook입니다.

```tsx
useEffect(setup, dependencies?)
```

- 렌더링 이후 해야 할 일, 즉 React의 외부와 관련된 일을 정해줄 수 있다.

- 기본적으로 렌더링 때마다 실행되므로, 의존성 배열을 통해 언제 이펙트를 실행할지 지정할 수 있다(= 불필요한 경우에 건너뛸 수 있다).

- 함수를 리턴함으로써 종료 처리를 할 수 있다.

### useContext()

`useContext`는 **컴포넌트에서 컨텍스트를 읽고 구독**할 수 있는 React Hook입니다.

```tsx
const value = useContext(SomeContext)

<AppContext.Provider value={넘겨줄 value}>
  <넘겨줄 component />
</AppContext.Provider>
```

일반적으로 부모 컴포넌트에서 자식 컴포넌트로 `Props`를 통해 데이터를 전달하는데, 그 깊이가 깊어질수록 거쳐가야 하는 컴포넌트들이 많아지고 코드를 반복적으로 작성하며, 변수명이 바뀔 시 모든 거쳐간 컴포넌트에서 변수명을 수정해야하는 일들이 많았습니다.

이를 위해 `Redux`를 많이 사용했으나, React에서 공식으로 전역적으로 데이터를 공유할 수 있게 바로 사용가능하게 Hook을 만들었습니다.

### useRef()

`useRef`는 **렌더링에 필요하지 않은 값을 참조**할 수 있는 React Hook입니다.

```tsx
const ref = useRef(initialValue)

// 아래 처럼 current를 사용하여 참조값을 선택가능
ref.current
```

- **컴포넌트의 생애주기 전체에 걸쳐서 유지되는 객체**. 즉, 컴포넌트가 없어질 때까지 동일한 객체가 유지된다.
- **객체 자체가 값은 아니고, 값을 참조하기 위한 객체**. 즉, 언제든지 값을 변경할 수 있다.
- `상태(state)`가 변경되면 해당 컴포넌트와 하위 컴포넌트를 다시 렌더링하지만, 레퍼런스 객체의 현재 값(current)이 바뀌더라도 렌더링에 영향을 주지 않는다.

#### `주요 용도`

1. 컴포넌트가 사라질 때까지 동일한 값을 써야 하는 경우. ⇒ input 등의 ID 관리.
2. (특히 useEffect 등과 함께 쓰면서 만나게 되는) 비동기 상황에서 현재 값을 제대로 쓰고 싶은 경우.

### useLayoutEffect()

`useLayoutEffect`는 **브라우저가 화면을 다시 칠하기 전에 실행되는** `useEffect` 버전입니다.

```tsx
useLayoutEffect(setup, dependencies?)
```

렌더링 이후 `layout`과 `paint` 전에 동기적으로 실행된다. 이로 인해 DOM을 조작하는 코드가 존재해서 사용자는 깜박임을 볼 수 없다.

## React Hook의 규칙

### 💡 최상위에서만 Hook을 호출해야한다

반복문, 조건문 혹은 중첩된 함수 내에세 Hook을 호출하면 안된다.

> `early return`이 실행되기 전에 항상 React 함수의 최상위에서 Hook을 호출해야한다.

이를 따르면 컴포넌트 렌더링될 때마다 항상 동일한 순서로 Hook이 호출된다.

### 💡 React 함수 내에서 Hook을 호출해야 합니다

Hook을 일반적인 JavaScript 함수에서 호출하면 안됩니다.

- Hook은 React 함수 컴포넌트에서 호출해야한다.
- Custom Hook에서 Hook을 호출해야한다.

## React StrictMode

React에서 제공하는 React strictMode이며, 애플리케이션 내의 잠재적 문제를 알아내기 위한 도구입니다.

### 검사항목

1. 잘못 사용한 생명주기 메서드
2. 레거시 문자열 ref 사용 여부
3. findDOMNode 사용 여부
4. 예상치 못한 부작용(side effect)
5. 레거시 컨택스트 사용 여부
