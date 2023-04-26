# 일급 객체(First Class Object)

일급 객체란 다른 객체들에 일반적으로 적용 가능한 연산을 모두 지원하는 객체를 가르키며 아래 3가지 조건만 충족하면 1급 객체라고 할 수 있다.

## 1. 변수에 데이터를 할당 할 수 있어야한다

```tsx
function sayHello() {
   return "Hello, ";
}
function greeting(helloMessage, name) {
  console.log(helloMessage() + name);
}

greeting(sayHello, "JavaScript!"); // Hello, JavaScript!
```

변수에 함수를 저장하기 위해 const 키워드를 사용하여 함수를 정의합니다. 여기서 익명 함수로 사용되지만 원하는 경우 명명 함수로도 사용할 수 있습니다.

```js
const foo = function() {
   console.log("foobar");
}

foo(); // 변수 foo로 호출
```

## 2. 객체의 파라미터로 전달할 수 있다.

```js
function sayHello() {
   return "Hello, ";
}
function greeting(helloMessage, name) {
  console.log(helloMessage() + name);
}
// `sayHello`를 `greeting` 함수 파라미터로 전달
greeting(sayHello, "JavaScript!"); // Hello, JavaScript!
```

## 3. 객체의 리턴값으로 리턴할 수 있어야한다

```js
function sayHello() {
   return function() {
      console.log("Hello!");
   }
}
```
