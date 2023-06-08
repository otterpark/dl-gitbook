# 상품 목록

쉽게 숫자에 천 단위에 콤마를 넣는 방법

1. `Intl.NumberFormat()`

```ts
export default function numberFormat(value: number) {
  return new Intl.NumberFormat().format(value);
}
```

2. `number.toLocalString()`

```ts
export default function numberFormat(value: number) {
  return value.toLocalString();
}
```
