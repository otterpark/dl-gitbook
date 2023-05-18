# Reflect

`Reflect`는 중간에서 가로챌 수 있는 `JavaScript` 작업에 대한 메서드를 제공하는 내장 객체입니다. 메서드의 종류는 **프록시 처리기와 동일**합니다. `Reflect`는 함수 객체가 아니므로 생성자로 사용할 수 없습니다.

## 설명

다른 대부분의 전역 객체와 다르게, `Reflect`는 생성자가 아닙니다. 따라서 함수처럼 호출하거나 new 연산자로 인스턴스를 만들 수 없습니다. `Math` 객체처럼, `Reflect`의 모든 속성과 메서드는 정적입니다.

`Reflect` 객체의 정적 메서드 이름은 프록시 처리기 메서드의 이름과 같습니다.

일부 메서드는 `Object`에도 존재하는 메서드이지만 약간의 차이가 있습니다.

## 정적 메서드

### Reflect.apply()

대상 함수를 주어진 매개변수로 호출합니다.

### Reflect.construct()

함수로 사용하는 new 연산자입니다. `new target(...args)`을 호출하는 것과 같습니다. 다른 프로토타입을 지정하는 추가 기능도 가지고 있습니다.

### Reflect.defineProperty()

`Object.defineProperty()`와 비슷합니다. `Boolean`을 반환합니다.

### Reflect.deleteProperty()

함수로 사용하는 `delete` 연산자입니다. `delete target[name]`을 호출하는 것과 같습니다.

### Reflect.get()

대상 속성의 값을 반환하는 함수입니다.

### Reflect.getOwnPropertyDescriptor()

`Object.getOwnPropertyDescriptor()`와 비슷합니다. 주어진 속성이 대상 객체에 존재하면, 그 속성의 서술자를 반환합니다. 그렇지 않으면 undefined를 반환합니다.

### Reflect.getPrototypeOf()

`Object.getPrototypeOf()`와 같습니다.

### Reflect.has()

함수로 사용하는 `in` 연산자입니다. 자신의, 혹은 상속한 속성이 존재하는지 나타내는 `Boolean`을 반환합니다.

### Reflect.isExtensible()

`Object.isExtensible()`과 같습니다.

### Reflect.ownKeys()

대상 객체의 자체 키(상속하지 않은 키) 목록을 `배열`로 반환합니다.

### Reflect.preventExtensions()

`Object.preventExtensions()`와 비슷합니다. `Boolean`을 반환합니다.

### Reflect.set()

속성에 값을 할당하는 함수입니다. 할당 성공 여부를 나타내는 `Boolean`을 반환합니다.

### Reflect.setPrototypeOf()

객체의 프로토타입을 지정하는 함수입니다. 지정 성공 여부를 나타내는 `Boolean`을 반환합니다.
