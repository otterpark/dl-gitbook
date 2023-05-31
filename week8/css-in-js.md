# CSS in JS

## CSS in JS란?

이름 그대로 CSS-in-JS를 사용하면 JavaScript 또는 TypeScript 코드에 직접 CSS를 작성하여 리엑트 컴포넌트 스타일을 지정할 수 있습니다.

```tsx
function ErrorMessage({ children }) {
  return (
    <div
      css={{
        color: "red",
        fontWeight: "bold",
      }}
    >
      {children}
    </div>
  );
}

// styled-components 또는 @emotion/styled, 문자열 styles를 사용
const ErrorMessage = styled.div`
  color: red;
  font-weight: bold;
`;
```

### 장점

1. `지역 스코프 스타일`: 기본적으로 스타일을 지역 스코프로 지정하여 클래스 이름 충돌이 없어진다.
2. `코로케이션`: 단일 컴포넌트에 관련된 모든 것을 같은 위치에 둘 수 있으며, 스타일을 사용하는 리엑트 컴포넌트 내부에 직접 스타일을 작성할 수 있다.
3. JavaScript 변수를 style에 사용할 수 있다.

### 단점

1. `런타임 오버헤드`: 컴포넌트 렌더링 시 CSS-in-JS 라이브러리는 document에 삽입할 수 있는 일반 CSS로 스타일을 `직렬화` 해야합니다.
2. `CSS-in-JS`는 번틀 크기가 크다. `react + react-dom`의 크기가 44.5kB지만 styled-components는 12.7kB이다.
3. `React DevTools`를 어지럽힌다. 

## CSS Flex

항목 간의 공간을 보다 효율적으로 배치하며, 정렬 및 분배하는 방법을 제공하는 데 목적이 있다. Flex Layout의 기본 개념은 컨테이너의 항목의 너비/높이를 변경하여 사용 가능한 공간을 잘 채울 수 있는 기능을 제공하는 것이다.

### Properties for the Parent

#### `display`

![flex-container](./img/flex-container.svg)

flex container를 정의합니다. 모든 직접 자식에 대해 flex context를 활성화합니다.

```css
.container {
  display: flex; /* or inline-flex */
}
```

#### `flex-direction`

![flex-direction](./img/flex-direction.svg)

주축을 기준으로 flex 항목이 배치되는 방향이 정의됩니다. Flexbox는 단일 방향 레이아웃 개념이며, 주로 가로 행 또는 세로 열에 배치된다.

```css
.container {
  flex-direction: row | row-reverse | column | column-reverse;
}
```

#### `flex-wrap`

![flex-wrap](./img/flex-wrap.svg)

flex 항목을 모두 한줄에 맞추려고 하지만 flex-wrap 속성을 사용하여 변경하고 필요에 따라 줄 바꿈을 허용할 수 있다.

```css
.container {
  flex-wrap: nowrap | wrap | wrap-reverse;
}
```

#### `flex-flow`

flex-direction과 flex-wrap을 한번에 정의할 수 있습니다.

```css
.container {
  flex-flow: column wrap;
}
```

#### `justify-content`

![justify-content](./img/justify-content.svg)

주축을 따라 정렬을 합니다. 한 줄의 모든 flex 항목이 유연하지 않거나 유연하지만 최대 크기에 도달했을 때 남은 여유 공간을 분배하는 데 도움이 됩니다.

```css
.container {
  justify-content: flex-start | flex-end | center | space-between | space-around | space-evenly | start | end | left | right ... + safe | unsafe;
}
```

- `flex-start (default)`: 플렉스 방향의 시작 부분을 향해 패킹
- `flex-end`: 플렉스 방향의 끝을 향해 패킹
- `start, end, left, right`: 각 방향에 맞게 패킹
- `center`: 줄에 따라 중앙에 배치
- `space-between`: 첫 번째 항목은 시작 라인, 마지막 항목은 끝라인으로 사이 정렬
- `space-around`: 항목이 줄에 균등하게 분포되어 있으며, 모든 항목의 양쪽 공간이 동일하다.(약간 각 item에 margin:0 20px을 준 느낌이다)
- `space-evenly`: space-around와 다르게 두 항목 사이의 간격이 동일하도록 한다.

#### `align-items`

![align-items](./img/align-items.svg)

가로축에 따라 정렬을 합니다. justify-content의 가로축 버전이다.

```css
.container {
  align-items: stretch | flex-start | flex-end | center | baseline | first baseline | last baseline | start | end | self-start | self-end + ... safe | unsafe;
}
```

- `stretch(기본값)`: 컨테이너를 채우기 위해 늘이기(여전히 최소 너비/최대 너비 준수)
- `flex-start / start / self-start`: 항목이 교차 축의 시작 부분에 배치됩니다.
- `flex-end / end / self-end`: 항목이 교차 축의 끝에 배치됩니다.
- `center`: 항목이 교차 축의 중앙에 배치됩니다.
- `baseline`: 항목이 기준선 정렬과 같이 정렬됩니다.

#### `align-content`

![align-content](./img/align-content.svg)

가로축에 여분의 공간이 있을 때 flex container의 줄을 정렬하는 것으로, 콘텐츠 맞춤이 주축 내에서 개별 항목을 정렬하는 방식과 유사합니다.

> flex-wrap에 wrap 또는 wrap-reverse 속성이 들어가 있을 경우에 사용 가능하며, 하나의 라인으로 되어 있을 시 작동하지 않는다.

```css
.container {
  align-content: flex-start | flex-end | center | space-between | space-around | space-evenly | stretch | start | end | baseline | first baseline | last baseline + ... safe | unsafe;
}
```

- `normal (default)`: 값이 설정되지 않은 것처럼 항목이 기본 위치에 패킹
- `flex-start / start`: 항목이 컨테이너의 시작 부분에 패킹
- `flex-end / end`:  컨테이너 끝으로 패킹된 항목
- `center`: 컨테이너 중앙에 항목 배치
- `space-between`: 항목이 균등하게 분포되어 있으며, 첫 번째 줄은 컨테이너의 시작 부분에 있고 마지막 줄은 끝에 있습니다
- `space-around`: 각 줄 주위에 동일한 간격으로 항목이 고르게 분포
- `space-evenly`: 항목은 주변에 동일한 공간으로 균등하게 배치
- `stretch`: 선이 늘어나서 남은 공간을 차지

#### `gap, row-gap, column-gap`

![gap](./img/gap.svg)

플렉스 항목 사이의 간격을 명시적으로 제어합니다. 바깥쪽 가장자리에 있지 않은 항목 사이에만 해당 간격을 적용합니다.

```css
.container {
  display: flex;
  ...
  gap: 10px;
  gap: 10px 20px; /* row-gap column gap */
  row-gap: 10px;
  column-gap: 20px;
}
```

최소 간격으로 생각하면되며, 간격이 justify-content: space-between;
로 인해서 작아질 때만 동작한다.

### Properties for the children

![children-items](./img/children-items.svg)

#### `order`

![order](./img/order.svg)

플렉스 항목은 소스 순서대로 배치됩니다. 그러나 순서 속성은 플렉스 컨테이너에 표시되는 순서를 제어합니다.

```css
.item {
  order: 5; /* default is 0 */
}
```

#### `flex-grow`

![flex-grow](./img/flex-grow.svg)

플렉스 컨테이너 내부의 사용 가능한 공간 중 해당 항목이 차지해야 하는 공간을 지정합니다. 모든 항목의 플렉스 크기가 1로 설정된 경우 컨테이너의 남은 공간은 모든 자식에게 균등하게 분배됩니다. 자식 중 하나의 값이 2인 경우 해당 자식은 다른 자식보다 두 배의 공간을 차지합니다.

```css
.item {
  flex-grow: 4; /* default 0 */
}
```

#### `flex-shrink`

필요한 경우 플렉스 항목을 축소할 수 있는 기능을 정의합니다.

```css
.item {
  flex-shrink: 3; /* default 1 */
}
```

#### `flex-basis`

남은 공간이 분배되기 전 요소의 기본 크기를 정의합니다. 길이(예: 20%, 5rem 등) 또는 키워드가 될 수 있습니다. 자동 키워드는 "내 너비 또는 높이 속성을 확인"을 의미합니다.

```css
.item {
  flex-basis:  | auto; /* default auto */
}
```

0으로 설정하면 콘텐츠 주변의 추가 공간이 고려되지 않습니다. 자동으로 설정하면 플렉스 성장 값에 따라 추가 공간이 분배됩니다.

## CSS grid

CSS Grid Layout은 사용자 인터페이스 디자인 방식의 2차원 그리드 기반 레이아웃 시스템입니다.

시작하려면 컨테이너 요소를 디스플레이가 있는 그리드로 정의하고 `grid-template-column` 및 `grid-template-rows`로 열과 행 크기를 설정한 다음 `grid-column` 및 `grid-row`를 사용하여 그리드에 자식 요소를 배치해야 합니다. 플렉스박스와 마찬가지로 그리드 항목의 소스 순서는 중요하지 않습니다. CSS는 어떤 순서로든 배치할 수 있으므로 미디어 쿼리를 사용하여 그리드를 매우 쉽게 재정렬할 수 있습니다.

### Grid Container

그리드가 적용되는 요소입니다. 모든 그리드 항목의 직접적인 부모입니다. 이 예제에서는 컨테이너가 그리드 컨테이너입니다.

```html
<div class="container">
  <div class="item item-1"> </div>
  <div class="item item-2"> </div>
  <div class="item item-3"> </div>
</div>
```

### Grid Line

격자 구조를 구성하는 구분선입니다. 세로("열 격자선") 또는 가로("행 격자선")일 수 있으며 행 또는 열의 양쪽에 위치할 수 있습니다. 여기서 노란색 선은 열 격자선의 예입니다.

![grid-line](./img/terms-grid-line.svg)

### Grid Track

두 그리드 선 사이의 공간입니다. 그리드의 열 또는 행이라고 생각하면 됩니다. 다음은 두 번째 행과 세 번째 행 그리드 선 사이의 그리드 트랙입니다.

![grid-track](./img/terms-grid-track.svg)

### Grid Area

4개의 그리드 선으로 둘러싸인 전체 공간입니다. 그리드 영역은 그리드 셀의 개수에 관계없이 구성할 수 있습니다. 다음은 행 그리드 라인 1과 3, 열 그리드 라인 1과 3 사이의 그리드 영역입니다.

![grid-area](./img/terms-grid-area.svg)

### Grid Item

그리드 컨테이너의 자식(즉, 직계 자손)입니다. 여기서 항목 요소는 그리드 항목이지만 하위 항목은 그렇지 않습니다.

```html
<div class="container">
  <div class="item"> </div>
  <div class="item">
    <p class="sub-item"> </p>
  </div>
  <div class="item"> </div>
</div>
```

### Grid Cell

인접한 두 행과 인접한 두 열 격자선 사이의 공간입니다. 그리드의 단일 "단위"입니다. 다음은 행 격자선 1과 2, 열 격자선 2와 3 사이의 격자 셀입니다.

![grid-cell](./img/terms-grid-cell.svg)

## Flex와 Grid의 차이

Flex는 1차원적인 부분만 고려한 레이아웃이며, Grid는 2차원적인 부분도 고려한 레이아웃이다. Grid가 조금 더 포괄적인 느낌이다.

Flex는 Flex 컨테이너를 중심으로 Flex 아이템을 중앙 정렬 또는 균등하게 표현하기에 좋으며, 복잡한 레이아웃도 적은 코드로 간결하게 설정이 가능하다.

Grid는 카드형식으로 되어있는 신문형식의 레이아웃을 쉽게 만들 수 있고 여백을 쉽게 조절 가능하다.

> grid는 flex와 row, column 방향이 반대이다.
