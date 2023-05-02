# DRY 원칙

DRY는 Don't Repeat Yourself의 약자로 정보의 반복을 줄이는 것을 목표로 하는 소프트웨어 개발의 기본 원칙입니다.

> "모든 지식 조각은 시스템 내에서 하나의 모호하지 않고 권위있는 표현을 가져야합니다"

즉, DRY 원칙을 준수한다는 것은 같은 코드나 로직을 반복해서 작성하거나 복사하여 붙여넣기 하는 행위를 하지 말아야합니다.

## DRY 원칙을 준수해야하는 이유

- 코드가 단순해지며, 한번만 작성할 수 있다.
- 한 곳에서만 코드를 변경하고 모든 인스턴스들에서 변경사항만 확인할 수 있다.
- 시간과 노력이 절약되고 유지 관리가 쉬우며 버그 가능성도 줄어든다.

## DRY 원칙을 준수하는 방법

- 코드와 로직을 재사용 가능한 더 작은 단위로 나누고 원하는 위치에서 해당 코드를 호출하여 사용
- 비즈니스 룰, 긴 표현식, if문, 수학 공식, 메타데이터 등을 한 곳에 모으자.