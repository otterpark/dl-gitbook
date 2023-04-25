# JSON(JavaScript Object Notation)

데이터를 저장하거나 전송할 때 많이 사용되는 `경량의 DATA 교환 형식`

- JavaScript 객체의 형식을 기반으로 만들어졌다.
- JavaScript에서는 `parse()`, `stringify()`를 사용하여 구문을 분석하고 JavaScript 값이나 객체를 생성하거나 JSON 문자열로 변환합니다.
- 사람, 기계 모두 이해하기 쉬우며 용량이 작아서 최근에는 JSON이 XML을 대체해서 데이터 전송 등에 많이 쓰입니다.

## JSON.parse()

JSON 문자열의 구문을 분석하고, 그 결과에서 JavaScript 값이나 객체를 생성합니다.

```js
const json = '{"age": 30, "height": 171}';
const obj = JSON.parse(json);

console.log(obj.age); // 30
```

## JSON.stringify()

JavaScript 값이나 객체를 JSON 문자열로 변환합니다.

```js
console.log(JSON.stringify({ age: 30, height: 171 }));
```
