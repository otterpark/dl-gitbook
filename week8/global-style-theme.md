# Global Style & Theme

## CSS Reset

각 브라우저마다 default 값으로 스타일들이 적용되어 있는데 이 default 값을 동일한 CSS 스타일을 보여주기 위해 초기화 시켜줘야 한다. 이를 reset CSS를 적용함으로써 해결한다.

예전에는 Eric Meyer's CSS Reset이 많이 사용되었지만 최근에는 브라우저 호환성이 좋아져 불필요한 부분을 줄이고 최신 웹 개발 트랜드를 반영한 Elad Shechter's CSS Reset가 인기를 끌고 있다고 한다.

<https://elad2412.github.io/the-new-css-reset/>

## `box-sizing` 속성

`box-sizing` CSS 속성은 요소의 전체 너비와 높이가 계산되는 방식을 설정한다.

기본적으로 CSS 상자 모델에서 요소에 할당하는 너비와 높이는 요소의 콘텐츠 상자에만 적용됩니다. 요소에 테두리나 패딩이 있는 경우 너비와 높이에 이를 더하여 화면에 렌더링되는 상자의 크기에 도달합니다. 즉, 너비와 높이를 설정할 때 추가될 수 있는 테두리 또는 패딩을 허용하도록 값을 조정해야 합니다.

## `word-break` 속성

`word-break` 속성은 텍스트가 콘텐츠 상자를 넘길 때마다 줄 바꿈이 표시될지 여부를 설정합니다.

```css
word-break: normal;
word-break: break-all;
word-break: keep-all;
word-break: break-word;
```

## `Theming`

styled-component는 `<ThemeProvider>` wrapper 컴포넌트를 내보냄으로써 전역 테마를 지원합니다. 이 컴포넌트는 컨텍스트 API를 통해 그 아래에 있는 모든 React 컴포넌트에 테마를 제공합니다. useContext와 동일하게  렌더링 트리에서 모든 스타일 컴포넌트는 제공된 테마에 접근할 수 있다.

```tsx
const Button = styled.button`
  font-size: 1em;
  margin: 1em;
  padding: 0.25em 1em;
  border-radius: 3px;

  /* Color the border and text with theme.main */
  color: ${props => props.theme.color};
  border: 2px solid ${props => props.theme.border};
`;

<ThemeProvider theme={theme}>
  <Button>Themed</Button>
</ThemeProvider>
```
