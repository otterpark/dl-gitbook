# SRP(단일 책임 원칙)

SRP에 대해서 조금 더 자세히 알기 위해, 객체지향의 원칙인 `SOLID`에 대해 알아보자!

## SOLID 원칙

- SRP(단일 책임 원칙)
- OCP(개방-폐쇄 원칙)
- LSP(리스코프 치환 법칙)
- DIP(의존 역전 원칙)
- ISP(인터페이스 분리 원칙)

위 원칙들의 앞 글자를 따서 `SOLID` 원칙이라고 부르며, 프로그래머가 시간이 지나도 유지보수와 확장이 쉬운 소프트웨어를 만드는데 도움을 줍니다.

## SRP(Single Responsibility Principle)란?

단일 책임 원칙은 `클래스는 단 한개의 책임을 가져야 한다` 를 의미합니다. 클래스가 여러 책임을 가지게 되면 각 책임마다 변경되는 이유가 발생하기에 클래스는 한 개의 책임만 가진다라는 원칙입니다. 여기서 책임이란 하나의 `기능 담당`으로 보면 됩니다.
> 클래스를 변경하는 이유는 단 **한 개**여야 합니다.

이러한 SRP를 잘 따르면 `한 책임의 변경으로부터 다른 책임의 변경으로의 연쇄작용`에서 자유로울 수 있게 됩니다.

- 코드 가독성 향상
- 유지보수 용이