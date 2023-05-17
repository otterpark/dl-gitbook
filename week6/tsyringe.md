# Tsyinge

생성자 주입을 위한 타입스크립트/자바스크립트용 경량 의존성 주입 컨테이너입니다.

간단하게 하면, TypeScript용 DI 도구(IoC Container)이며, External Store를 관리하는데 활용할 수 있다. React Component 입장에서는 `전역`처럼 느껴진다. `Props Drilling`을 해결할 수 있는 방법 중 하나이다.

> React에서는 Context를 사용하여 해결 가능하다. (전역에 Context 지정 후 Component를 Context provider로 감싼 후 value 값을 넘겨주고 사용하고 싶은 Component에서 useContext를 사용하여 값을 가져올 수 있다.)

```bash
npm i tsyringe
```

## reflect-metadata

`Tsyinge`에 Reflect API에 대한 Polyfill을 추가해줘야 하는데 대표적으로 `relflect-metadata`를 사용한다.

대체할 수 있는 Reflect API

- core-js (core-js/es7/reflect)
- reflection

Reflect polyfill import는 DI를 사용하기 전에 한 번만 추가해주면 된다.

```bash
npm i reflect-metadata
```

```tsx
import "reflect-metadata";
```

> 🚨 reflect-metadata를 import할 때, 주의해야할 점은 `모든 프로그램이 시작하는 곳`에 import를 실행해야한다.

## DI(Dependency Injection) - 의존관계 주입

"A와 B를 의존한다"를 표현하면 어떤 의미를 가질까?  추상적이지만 토비의 스프링에서는 다음과 같이 정의한다고 한다.

> 의존 대상 B가 변하면, 그것이 A에 영향을 미친다.
>
> => 이일민, 토비의 스프링

이 말은 즉, B의 기능이 추가 또는 변경되거나 형식이 바뀌면 그 영향이 A에 미친다.

DI란 강한 결합을 느슨한 결합으로 전환시키는 방법이며, 제어의 역전(IoC)의 기술 중 하나입니다.

```tsx
class Employee {
  constructor(name) {
    this.name = name;
  }
  call() {
    console.log("calling: ", this.name);
  }
}

class Boss {
  employee = new Employee('Park');

  call() {
    this.employee.call();
  }
}

const boss = new Boss();
boss.call();
```

여기서 핵심 로직은 `Person` 클래스에 있으며, 이 클래스는 종속 요소인 `Boss`가 있습니다. `boss.call()` 메소드는 직원을 부릅니다. 하지만 여기에 유영성 및 테스트 등 몇 가지 문제가 있습니다.

위 코드는 유연성이 떨어집니다. 보스가 다른 직원을 부르려면 하드코딩을 해야하는 상황이 나옵니다. `DI`는 클래스를 종속성으로 분리하여 필요한 종속성을 제공함으로써 이 문제를 해결 할 수 있습니다.

```tsx
class Employee {
  constructor(name) {
    this.name = name;
  }

  call() {
    console.log("Calling: ", this.name);
  }

  changeCall(name) {
    this.name = name;
    this.call();
  }

}

class Boss {
  constructor(employee) {
    this.employee = employee;
  }

  call() {
    this.employee.call();
  }

  callAnotherEmployee(employee) {
    this.employee.changeCall(employee);
  }
}

const person = new Employee('Park');
const boss = new Boss(person);

boss.call();
boss.callAnotherEmployee('Ho');
```

위와 같이 클래스를 분리시키면 하드 코딩없이 `Employee` 인스턴스를 생성하여 `Boss`에 전달하는 작업은 의존성 주입 공급자에게 맡기면 됩니다.

이로 인해 특정 클래스에 필요한 클래스의 인스턴스를 생성하는 것에 걱정할 필요가 없어졌습니다.

### DI(Dependency Injection) 장점

1. `의존성이 줄어든다` - 의존대상의 변화하면 변화에 매우 취약하다. 주입 받는 대상이 변하더라도 그 구현 자체 수정할 일이 없어지거나 줄어든다.
2. `재사용성이 높은 코드가 된다` - 기존 `Boss` 클래스에서만 사용되었던 `call`을 별도로 구분하여 구현하면, 다른 클래스에서 재사용이 가능하다.
3. `테스트하기 좋은 코드가 된다` - 서로 다른 `Boss`와 `Employee`의 테스트를 분리하여 진행할 수 있다.
4. `가독성이 높아진다` - 자연스럽게 기능들을 별도로 분리하게 되어 자연스럽게 가동성이 높아진다.

## 싱글톤 패턴(SingleTon pattern)

```
소프트웨어 디자인 패턴에서 싱글턴 패턴(Singleton pattern)을 따르는 클래스는, 생성자가 여러 차례 호출되더라도 실제로 생성되는 객체는 하나이고 최초 생성 이후에 호출된 생성자는 최초의 생성자가 생성한 객체를 리턴한다. 이와 같은 디자인 유형을 싱글턴 패턴이라고 한다. 주로 공통된 객체를 여러개 생성해서 사용하는 DBCP(DataBase Connection Pool)와 같은 상황에서 많이 사용된다.

- 위키피디아
```

간단하게 설명하면 싱글톤 패턴은 객체의 인스턴스를 한개만 생성되게 하는 패턴입니다.

주로 이러한 패턴은 주로 프로그램 내에서 하나로 공유 해야하는 객체가 존재할 때 해당 객체를 싱글톤으로 구현하여 모든 유저 또는 프로그램들이 해당 객체를 공윻며 사용하도록 할 때 사용됩니다.

보통 아래에 같은 상황에 사용을 합니다.

- 프로그램 내에서 하나의 객체만 존재해야 한다.
- 프로그램 내에서 여러 부분에서 해당 객체를 공유하여 사용해야한다.

정리해보면, 싱글톤 패턴은 `메모리`, `속도`, `데이터 공유` 측면에서 이점이 있습니다. 하지만 그렇다고 해서 싱글톤 패턴이 무조건 좋은게 아니며, 해당 객체의 인스턴스가 한 개만 존재해야 하는지, 사용 시 동시성 문제가 발생하지 않는지를 체크하며 사용해야 합니다.
