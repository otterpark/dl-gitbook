# HTML DOM API

## Location

`Window.location` 프로퍼티에 접근하면 읽기 전용인 `Location` 오브젝트를 얻어올 수 있습니다. 이는 현재 `document`의 `location`에 대한 정보를 담고 있습니다.

`Location 인터페이스`는 객체가 연결된 `장소(URL)`를 표현합니다. `Location 인터페이스`에 변경을 가하면 연결된 객체에도 반영되는데, `Document`와 `Window` 인터페이스가 이런 `Location`을 가지고 있습니다. 각각 `Document.location`과 `Window.location`으로 접근할 수 있습니다.

```js
Window.location
Document.location
```

## pathname

URL 인터페이스의 `pathname` 속성은 URL의 경로와 그 앞의 `/`로 이루어진 `USVString`을 반환합니다. 경로가 없는 경우 빈 문자열을 반환합니다.

일반적인 웹 사이트는 URL에 따라 다른 웹 페이지를 보여준다. 하나의 웹 페이지를 하나의 컴포넌트로 만들고, URL에 따라 적절한 컴포넌트가 보이게 함으로써 구현 가능하다.

```tsx
function App() {
 const { pathname } = window.location;

 return (
  <div>
   <Header />
   <main>
    {pathname === '/' && <HomePage />}
    {pathname === '/about' && <AboutPage />}
   </main>
   <Footer />
  </div>
 );
}
```

### Value

`URL`의 경로의 `/`로 이루어진 `USVString`을 반환

> 없을 시 빈 문자열 반환
