# React

## React란?

리엑트는 페이스북에서 제공해 주는 JavaScript 라이브러리(프레임워크 X)이며, 작은 UI 컴포넌트 퍼즐들을 구성 및 조합하여 복잡한 UI를 구성할 수 있게 도와준다.

여기서 잠깐! ✋
라이브러리와 프레임워크의 간단한 설명
-> 프로그램을 쉽게 만들 수 있게 하는 공통적 목적을 가지고 있으며, 중요 차이점으로는 코드 흐흠의 제어권이 누구에게 있냐로 볼 수 있다.

|종류|**라이브러리**|**프레임워크**|
|:--:||:--:||:--:|
|흐름|내가 만든 코드를 내가 컨트롤 할 수 있음|누군가가 만들어 놓은 규칙에 맞춰 만들어야함|
|코드|활용 가능한 특정 기능에 대한 코드(스티커처럼 붙였다 떼었다가 필요에 따른 코드 사용)|일정한 형태의 틀을 가지고 있어 틀에 맞추어 코드 설계 및 구현|
|비유(집)|집을 꾸미기 위한 완성품(컴퓨터, 티비, 소파, 의자, 책상 등)|도면과 설계가 완성된 집|
|언어 종류|React, Jquery|Angular, Vue, Spring, Django|

## React Component

`React`에 대해서 앞서 설명할 때, `작은 UI 컴포넌트 퍼즐들을 구성 및 조합하여 복잡한 UI를 구성`에 대해서 설명을 했었는데, 화면에서 UI 요소를 구분할 때 컴포넌트라는 조각으로 구성됩니다. 이 조각들을 구성 및 조합하여 하나의 퍼즐을 만들어 복잡한 UI를 구성합니다. 한 마디로 표현하면 React Component는 `리엑트에서 앱을 이루는 최소 단위` 입니다. React Component에는 `함수형 컴포넌트`와 `클래스형 컴포넌트`가 있습니다.

[happycording 개인 블로그(클래스형 컴포넌트와 함수형 컴포넌트 특징)](https://happycording.tistory.com/entry/React-%ED%81%B4%EB%9E%98%EC%8A%A4%ED%98%95-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8%EC%99%80-%ED%95%A8%EC%88%98%ED%98%95-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8-%ED%8A%B9%EC%A7%95)

### React Component 특징

- `property(props)` \
부모 컴포넌트에서 자식 컴포넌트에 전달되는 데이터이며, 자식 컴포넌트에서는 프로퍼티 값을 수정할 수 없습니다.
- `state` \
컴포넌트 상태를 저장하고 수정 가능한 데이터이다.
- `context` \
부모 컨포넌트에서 생성하여 모든 자식 컴포넌트에게 전달하는 데이터이다.

## React 리렌더링

앞서 리렌더링에 대해 알아보기 전에 렌더링에 대해 알아보자!
`렌더링`이란 `React Component`가 현재 props와 state의 상태에 맞춰 UI를 어떻게 구상할지를 컴포넌트에 작업을 요청하는 것을 의미한다.

React는 자동적으로 어떠한 액선(리렌더링의 조건에 충족할 시)이 일어날 시 컴포넌트를 리렌더링한다.

> 무분별하게 렌더링이 일어날 경우 성능 저하가 일어날 수 있기 때문에 최대한 코드를 작성할 때 무분별하게 렌더링이 일어나지 않도록 짜야한다.

### React 리렌더링 조건

- `state(상태) 변경이 있을 시` \
React는 state(상태) 변경이 감지되면 리렌더링 한다.
- `새로운 props가 들어올 때` \
React는 부모 컴포넌트로부터 새 props가 들어오면 자식 컴포넌트는 재렌더링 한다.
- `기존 props가 업데이트 되었을 때` \
React는 부모 컴포넌트로부터 받은 `props`가 변경되면 `props` 값을 받은 자식 컴포넌트도 리렌더링 한다.
- `부모 컴포넌트가 리렌더링 될 때` \
React는 부모 컴포넌트가 업데이트 되어 리렌더링 시 자식 컴포넌트도 리렌더링 한다.

## IoC(Inversion of Control)

왜 갑자기 `IoC(Inversion of Control)`가 `React`에 나왔을까를 찾아보니 아래와 같은 문제들이 있었다.

```text
만약 React내에 원래 사용하고 있던 기능에 새로운 기능을 추가해달라는 요청이 왔다고 가정하면,

- 리엑트 컴포넌트에 props를 추가
- 리엑트 훅에 argument를 추가

등의 엑션을 취한다. 바쁘다고 가정하면 더욱 더 코드가 난잡해진다.
```

위 같은 내용들이 반복 시 구현 로직은 복잡해지게 되며, 아래와 같은 문제점들이 발생한다.

- `"성능이 급격히 저하된다"`: 코드 사이즈의 증가
- `"유지보수적으로 좋지 않다"`: 개발자가 props에 대해 어떤 역할을 하는지 파악하기 힘듦
- `요구사항이 복잡해 질 수록 다양한 props명이 출현할 가능성이 높아진다.`

이러한 이유로 코드 변경에 두려움을 겪게 됩니다.

### 그럼 IoC에 대해 알아보자!

IoC에 대해 Wikipedia에서는 아래와 같이 정의를 내립니다.

```text
`제어의 반전(역제어)는 프로그래머가 작성한 프로그램이 재사용 라이브러리의 흐름 제어를 받게 되는 소프트웨어 디자인 패턴입니다.
```

이를 간단하게 정리해보면, 전통적인 프로그래밍에서 흐름은 프로그래머가 작성한 프로그램이 외부 라이브러리 코드를 호출하여 이용한다.

하지만 IoC 구조가 적용된 구조에서는 외부 라이브러리 코드가 프로그래머가 작성한 코드를 호출하게 합니다.

여기서 부터 추상화라는 개념이 들어가게 되는데 `추상화에서 할 일을 줄이고 사용자가 그 할 일을 하도록해라` 로 생각하면 됩니다. 추상화의 장점 중 `복잡하고 반복적인 작업을 모두 처리할 수 있다` 때문에 나머지 코드를 짧고 간결하게 만들 수 있다는 점이기에 직관적이지 않은 것처럼 보일 수 있습니다.

말로만 설명하면 개념적으로 너무 어려운 것 같아 코드로 한번 이야기를 해보려고 합니다. 실제 우리가 자주 쓰는 `Array.prototype.filter()`가 현재 없다는 가정하에 `추상화` filter 함수를 만들어 보겠습니다.

```javascript
function filter(array) {
  let newArray = []
  for (let index = 0; index < array.length; index++) {
    const element = array[index]
    if (element !== null && element !== undefined) {
      newArray[newArray.length] = element
    }
  }
  return newArray
}

filter([0, 1, undefined, 2, null, 3, 'four', '']) // [0, 1, 2, 3, 'four', '']
```

위 `추상화`에 조금 더 다양한 사례를 추가해 보겠습니다.

```javascript
function filter(
  array,
  {
    filterNull = true,
    filterUndefined = true,
    filterZero = false,
    filterEmptyString = false,
  } = {},
) {
  let newArray = []
  for (let index = 0; index < array.length; index++) {
    const element = array[index]
    if (
      (filterNull && element === null) ||
      (filterUndefined && element === undefined) ||
      (filterZero && element === 0) ||
      (filterEmptyString && element === '')
    ) {
      continue
    }

    newArray[newArray.length] = element
  }
  return newArray
}

filter([0, 1, undefined, 2, null, 3, 'four', ''])
// [0, 1, 2, 3, 'four', '']

filter([0, 1, undefined, 2, null, 3, 'four', ''], {filterNull: false})
// [0, 1, 2, null, 3, 'four', '']

filter([0, 1, undefined, 2, null, 3, 'four', ''], {filterUndefined: false})
// [0, 1, 2, undefined, 3, 'four', '']

filter([0, 1, undefined, 2, null, 3, 'four', ''], {filterZero: true})
// [1, 2, 3, 'four', '']

filter([0, 1, undefined, 2, null, 3, 'four', ''], {filterEmptyString: true})
// [0, 1, 2, 3, 'four']
```

여기서 사용한 예제는 6가지에 불과하지만, 실제로 이 기능들을 조합하면 더 많은 케이스들이 존재합니다.

위 예제는 일반적인 `추상화`입니다. 만약 위 예제에서 {filterZero: true, filterUndefined}를 수행한다고 가정하면 어떨까요? 추상화를 해당 기능을 제거 또는 사용하는데 방해될 될까 두려워집니다. 이는 테스트 코드를 작성할 때에도 부정적인 영향을 끼치는데 실제 존재하지 않은 사례(필요할지도 모른다)를 테스트 코드를 작성하게 됩니다. 이후 스노우볼을 굴려 이 코드가 이후에 필요없어져도 나중에 필요할지도 모른다는 생각을 하거나 코드를 건드리는 것이 두렵다는 이유로 건드지 않게 되는 상황이 만들어집니다.

그럼 조금 더 신중하게 추상화를 적용하고 IoC를 적용하여 모든 사용 사례를 지원하게 해보겠습니다.

```javascript
function filter(array, filterFn) {
  let newArray = []
  for (let index = 0; index < array.length; index++) {
    const element = array[index];
    if (filterFn(element)) {
      newArray[newArray.length] = element;
    }
  }
  return newArray
}

filter([0, 1, undefined, 2, null, 3, 'four', ''], el => el !== undefined)
// [0, 1, 2, null, 3, 'four', '']

filter([0, 1, undefined, 2, null, 3, 'four', ''], el => el !== null)
// [0, 1, 2, undefined, 3, 'four', '']

filter(
  [0, 1, undefined, 2, null, 3, 'four', ''],
  el => el !== undefined && el !== null && el !== 0,
)
// [1, 2, 3, 'four', '']

filter(
  [0, 1, undefined, 2, null, 3, 'four', ''],
  el => el !== undefined && el !== null && el !== '',
)
// [0, 1, 2, 3, 'four']
```

위 예제를 보면 `새 배열에 어떤 요소가 들어갈지 결정하는 책임을 filter 함수에서 filter 함수를 호출하는 함수로 변경` 우리는 제어의 반전을 이용해 더 다양한 사례들을 지원할 수 있게 되었습니다.

만약 아래 예제를 이전 filter 함수에 적용한다고 생각하면 벌써부터 끔찍합니다.

```javascript
filter(
  [
    {name: 'dog', legs: 4, mammal: true},
    {name: 'dolphin', legs: 0, mammal: true},
    {name: 'eagle', legs: 2, mammal: false},
    {name: 'elephant', legs: 4, mammal: true},
    {name: 'robin', legs: 2, mammal: false},
    {name: 'cat', legs: 4, mammal: true},
    {name: 'salmon', legs: 0, mammal: false},
  ],
  animal => animal.legs === 0,
)
// [
//   {name: 'dolphin', legs: 0, mammal: true},
//   {name: 'salmon', legs: 0, mammal: false},
// ]
```

이후에 조금 더 React를 배우며, 리엑트 예제에 대해서 추가 예정입니다.
