# Style Basics

## className

엘리먼트 인터페이스에 `className` 속성은 지정된 엘리먼트의 클래스 속성 값을 가져온 후 설정한다.

### Value

현재 엘리먼트의 클래스를 나타내는 문자열 변수

```js
const el = document.getElementById("item");
el.className = el.className === "active" ? "inactive" : "active";
```

### React에서는 어떻게 사용할까?

위와 같이 JavaScript 문법 그대로 사용하여 넣는다.

```jsx
<p className={'active'}>
```

## 의미있는 마크업

HTML Element 들의 어떤 의미를 가지고 있는지 정확하게 알고 있는지와 HTML 마크업에 대해 정확하게 이해하는 것이 중요합니다.

[mdn html 참고서](https://developer.mozilla.org/ko/docs/Web/HTML/Reference)
