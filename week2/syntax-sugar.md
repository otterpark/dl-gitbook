# Syntax Sugar란?

한국어로 문법적 설탕입니다. JavaScript 뿐만 아니라 다른 프로그래밍 언어 전반적으로 적용되는 개념이며, `읽는 사람 또는 작성하는 사람이 편하게 디자인 된 문법` 입니다.
> 직관적이고 간결한 문법을 가지고 있다.

## 1. 변수 단축 선언

같은 선언 타입을 가진 변수를 한줄로 선언하는 방법이다.

```js
let a,
    b = 0; // a = undifined, b = 0;

const c = 0,
      d = 0;  // c = 0, d = 0;
/*
  const 단축 선언 시 초기값 할당을 하지 않으면 Const 성질로 인해 SyntaxError가 발생합니다.
*/
```

## 2. 단축 평가 값

논리 연산자가 왼쪽에서 오른쪽으로 평가를 실행합니다. 더이상 `평가가 필요하지 않을 시 실행을 중단` 하는 것을 단축 평가라고 합니다. 논리 연산자는 `||(OR)`, `&&(AND)` 연산자를 사용합니다.

```js
let arr = [];
console.log(arr.length || '빈 배열입니다.'); // '빈 배열입니다.'

arr.push(1); // arr = [1]
console.log(arr.length && '배열에 값이 있습니다.') // '배열에 값이 있습니다.'
```

- `AND 연산자`는 arr.length가 truthy 값인 것을 확인 후 다음 값을 추가로 평가하여, '배열에 값이 있습니다.'를 출력한다. (마지막 평가 값을 출력)
- `OR 연산자`는 arr.length가 falsy 값인 것을 확인 후 다음 값을 추가로 평가하여 '빈 배열입니다.'를 출력한다.

## 3. 널 별합 연산자

널 병합 연산자는 `||(첫 번째 truthy 값을 반환)` 또는 `??(첫 번째 정의된(defined) 값을 반환)` 값을 사용하여 `null`, `undifined`인지를 확인합니다.

```js
let width = 0;

alert(width || 100); // 100
alert(width ?? 100); // 0
```

- `width || 100`은 `width`가 `0`이라 falsy 한 값으로 취급했기에 `null` 이나 `undifined`를 할당한 것과 동일하게 처리합니다.
- `width ?? 100`은 `width`가 `null` 이나 `undifined`일 경우에만 `100`이 됩니다. 하지만 `width`는 `0` 이므로 `0`이 출력됩니다.

## 4. 삼항 조건 연산자

if 문의 단축 형태로 실행 방식은 동일합니다.

### if 방식

```js
if(true) {
  return true;
} else {
  return false;
}
```

### 삼항 조건 연산자 방식

```js
(true) ? true : false;
```

## 5. 전개 구문

`Iterable 객체`에 모두 전개 구문을 사용할 수 있습니다,.

```js
// Function
function myFunction(x, y, z) { }
var args = [0, 1, 2];
myFunction(...args);

// Array
const abcArr = ['a', 'b', 'c'];
const spreadArr = [ ...abcArr, 'e', 'f' ]; // ['a', 'b', 'c', 'e', 'f']
```

## 6. 나머지 매개변수

`할당되지 않은 매개변수를 배열로 받는 기능`이며, 항상 `마지막 파라미터`에서만 사용 가능합니다.

```js
function fn(name, age, ...arg) {
    // name = 'jinwoo'
    // age = 29
    // arg = [ 'ugly', 'bright', 'kind'];
}
fn('jinwoo', 29, 'ugly', 'bright', 'kind');
```

## 7. 템플릿 리터럴

템플릿 리터럴의 `백틱(``)`과 `${} 표기법`을 사용하여 표현식을 허용하는 문자열 리터럴입니다.

```js
const message = 'World!';
console.log(`Hello, ${message}`);

```

## 8. String을 Number 형태로 변환

문자열을 아래의 방법으로 넘버 형태로 변환할 수 있습니다.

- `+`
- `parseInt()`
- `Number()`

```js
console.log(typeof +'100'); // number
console.log(typeof parseInt('100')); // number
console.log(typeof Number('100')); // number
```

## 9. 구조분해할당

배열 또는 객체 속성을 해체하여 각 개별 변수에 담을 수 있게 표현한 식이다.

```js
// Object
({ a, b } = { a: 10, b: 20 });
console.log(a); // 10
console.log(b); // 20

// Array
let [c, d] = [1, 2, 3]; // c: 1, d: 2
let [e, f, ...g] = [1, 2, 3, 4, 5]; // e: 1, f: 2, g: [3, 4, 5]
```
