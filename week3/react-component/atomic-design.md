# Atomic design

## 디자인 시스템과 Atomic 디자인

brad frost에 따르면 디자인 시스템은 어떤 조직이 디지털 인터페이스를 디자인하고 구축하는 방식에 대한 이야기라고 말합니다. 디자인 시스템은 여러가지 하위 시스템을 포함하는데, UI 컴포넌트와 variants, 타이포그래피 시스템, 컬러 팔레트 시스템, 레이아웃 / 그리드 시스템 등이 있습니다. 아토믹 디자인은 디자인 시스템을 만드는 방법론입니다.

## Atomic 디자인

![Atomic design](/week3/img/atomic-design-flow.png)

모든 것은 `atom(원자)`로 구성되어있고 `atom(원자)`들이 서로 결합하여 `molecule(분자)`이 되고, `molecule(분자)`는 더 복잡한 orginism(유기체)으로 결합하여 궁극적으로 모든 물질을 생성합니다.

Atomic 디자인은 이 개념을 차용해 컴포넌트를 atom, molecule, organism, template, page의 5가지 레벨로 나눕니다.

Atomic 디자인은 단계별 기준을 가지고 있으며, 단계별로 추상적인 것에 대해 구체화하는 단계를 가집니다. 이러한 과정을 통해 일관성을 가지고 확장하면서 최종 컨텐츠를 보여줄 수 있습니다.

### 1. Atom

![Atomic design Atom](/week3/img/atoms-form-elements.png)

`Atom`은 더 이상 분해할 수 없는 기본 컴포넌트입니다. 예를 들어 `label`, `input`, `button`과 같이 더 이상 세분화할 수 없는 기본 HTML 요소가 포함됩니다.

### 2. Molecule

![Atomic design Molecule](/week3/img/molecule-search-form.png)

`Molecule`은 여러 개의 `Atom`을 결합하여 자신의 고유한 특성을 가집니다. `Molecule`은 단순한 UI 요소 그룹입니다. 예를 들어 `양식 레이블`, `검색 입력`, `버튼`을 함께 결합하여 검색 양식 `Molecule`을 만들 수 있습니다.

이렇게 결합을 하게되면 하나의 목적을 가지게 됩니다. 버튼을 클릭 시 양식이 제출되며, 검색 기능이 필요한 곳 어디든 배치할 수 있는 재사용 가능한 컴포넌트가 탄생했습니다.

단순한 컴포넌트를 만들면 UI 디자이너와 개발자가 `한 가지 일을 제대로 하라!`는 단일 책임 원칙을 준수하는데 도움이 됩니다. 단순한 UI `Molecule`을 만들면 테스트가 쉬워지고 재사용성이 향상되며 인터페이스 전반의 일관성을 높일 수 있습니다.

### 3. Organisms

![Atomic design Organisms](/week3/img/organism-header.png)

`Atom` and/or `Molecule` and/or 기타 `Organisms` 그룹으로 구성된 비교적 복잡한 UI 구성요소 입니다. 인터페이스의 뚜렷한 섹션을 형성합니다. `Organisms`는 더 작고 단순한 구성 요소가 작동하는 모습을 보여주며, 반복해서 사용할 수 있는 뚜렷한 패턴 역할을 합니다. `Organisms`은 `카테고리 목록`, `검색 결과`, `관련 제품`에 이르기까지 제품 그룹을 표시해야 하는 모든 곳에 사용할 수 있습니다.

### 4. Templates

![Atomic design Templates](/week3/img/template.png)

`Templates`는 레이아웃에 컴포넌트를 배치하고 디자인의 기본 콘텐츠 구조를 명확하게 표현하는 페이지 수준 개체입니다. 홈페이지 `Templates`은 필요한 모든 페이지 구성 요소와 함께 작동하는 모습을 표시하여 비교적 추상적인 `Molecule`과 `Organisms`에 대한 컨텍스트를 제공합니다. `Templates`의 또 다른 중요한 특징은 페이지의 최종 컨텐츠가 아닌 페이지의 기본 컨텐츠 구조에 초점을 맞춘다는 점입니다. `이미지 크기`, `제목 및 텍스트 구절의 문자 길이`와 같은 구성 요소의 중요한 속성을 명확하게 표현하는 것이 유용합니다.

### 5. Pages

![Atomic design Page](/week3/img/page.png)

`Pages`는 `Templates`의 특정 인스턴스로, 살제 대표 컨텐츠가 배치된 UI 모습을 보여줍니다. 이전 예제 기반으로 `Templates`를 가져온 뒤 `Templates`에 대표적인 텍스트, 이미지 및 미디어를 추가하여 실제 컨텐츠가 작동하는 모습을 보여줄 수 있습니다. 재사용 가능한 디자인 패턴을 설정하고 그 패턴 안에 넣는 컨텐츠의 현실을 정확하게 반영하는 시스템을 만들어야 합니다.

## Atomic design 장점

- 컴포넌트 재사용성이 극대화될 수 있습니다.
- 컴포넌트의 계층 구조를 알아보기 쉬워 설계 변경이 필요 시 빠르게 변경할 수 있습니다.
- 디자인 요소가 재사용될 컴포넌트에 일괄 적용되므로 styles 적용 및 변경이 쉽습니다.

## Atomic design 단점

- 컴포넌트가 적절하게 분리되지 않으면 오히려 컴포넌트의 복잡도가 높아져 유지보수가 까다롭습니다.
- Page부터 Atom까지 너무 많은 props drilling(props를 최하위 컴포넌트로 전달하기 위해 여러 컴포넌트를 거져가는 것)이 일어나 복잡한 상태 관리로 개발 피로도가 증가합니다.
