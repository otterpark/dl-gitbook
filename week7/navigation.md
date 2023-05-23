# Navigation

## Web APIs - History

History API 사용자의 기록을 앞뒤로 탐색하고 기록 스택의 내용을 조작할 수 있는 유용한 메서드와 프로퍼티를 노출합니다.

### History.back()

브라우저가 세션 기록의 바로 뒤 페이지로 이동하게 지시합니다.

> 이전 페이지가 없을 경우 아무것도 하지 않습니다.

```js
history.back()
```

### History.forward()

브라우저가 세션 기록의 바로 앞 페이지로 이동하게 지시합니다.

> 다음 페이지가 없을 경우 아무것도 하지 않습니다.

```js
history.forward()
```

### History.go()

`history` 세션에서 특정한 페이지를 로딩합니다. 인자로 전달하는 파라미터 값에 따라 history를 통해서 페이지를 앞 뒤로 이동한다.

> 이 메서드는 `비동기`로 동작합니다.

```js
history.go([delta])
```

여기서 `delta` 현재 페이지에서 이동하려고 하는 history의 위치 값

### History.pushState()

브라우저의 세션 기록 스택에 상태를 추가합니다.

- 상태
- 제목
- URL

```js
const state = {};
const title = '';
const url = '/about';

history.pushState(state, title, url);
```

### History.replaceState()

현재 `history`를 수정해 메소드의 매개 변수에 전달 된 `stateObj`, `title`, `URL`로 대체합니다. `History.pushState()`의 업데이트 버전입니다.

```js
history.replaceState(stateObj, title[, url])
```

## React Router - NavLink, Link, Navigate, useNavigate

### NavLink

`<NavLink>`는 `active` 또는 `pending` 여부를 알 수 있는 특별한 종류의 `<Link>`입니다. 이는 현재 선택된 router의 탭을 표시하려는 이동 경로 및 탐색 메뉴를 만들 때 유용합니다. 또한 `screen readers`와 같은 보조 기술에 유용한 컨텍스트를 제공합니다.

```tsx
function Header() {
 return (
  <header>
   <nav>
    <ul>
     <li><NavLink to="/">Home</NavLink></li>
     <li><NavLink to="/about">About</NavLink></li>
    </ul>
   </nav>
  </header>
 );
}
```

### Link

사용자가 클릭하거나 탭하여 다른 페이지로 이동할 수 있게 해주는 요소입니다. 실제 `react-router-dom`에서 `<Link>`는 링크하는 리소스를 가리키는 실제 `<a>` 엘리먼트를 렌더링 합니다.

> 기존 <a> 태그 속성 처럼 라우트 동작을 빼고 싶다면 `<Link reloadDocument>`를 사용하면 된다.

```tsx
import { NavLink } from "react-router-dom";

<NavLink
  to="/messages"
  className={({ isActive, isPending }) =>
    isPending ? "pending" : isActive ? "active" : ""
  }
>
  Messages
</NavLink>
```

`<Link to>`는 상위 경로를 기준으로 해당 `<Link>`를 렌더링한 경로와 일치하는 URL 경로를 기반으로 한다.

### Navigate

`<Navigate>` 요소는 렌더링될 때 현재 위치를 변경합니다. 이 요소는 `useNavigate`를 둘러싼 컴포넌트 래퍼이며 프로퍼티와 동일한 인수를 모두 허용합니다.

> 컴포넌트 기반 버전의 useNavigate Hook을 사용하면 Hook을 사용할 수 없는 React.Component 하위 클래스에서 이 기능을 더 쉽게 사용할 수 있습니다.

```tsx
import { Navigate } from 'react-router-dom';

export default function LoginPage() {
 return (
  <Navigate to="/" />
 );
}
```

테스트 시 `“ReferenceError: Request is not defined”` 에러가 나면 `“whatwg-fetch”`를 임포트해서 해결할 수 있다.

### useNavigate

`useNavigate Hook`은 `effect`에서 프로그래밍 방식으로 탐색할 수 있는 함수를 반환합니다.

#### 🚨 일반적으로 `useNavigate`보다 `loaders`와 `actions`에 Fetch Utillites의 `redirect`를 사용하는 것이 좋습니다.

```tsx
import { useNavigate } from 'react-router-dom';

export default function Footer() {
 const navigate = useNavigate();
 
 const handleClick = () => {
  navigate('/about');
 };
 
 return (
  <footer>
   <button type="button" onClick={handleClick}>
    Press
   </button>
  </footer>
 );
}
```

### redirect

`loaders`와 `actions`에서 **응답을 반환하거나 던질 수 있으므로** `redirect`를 사용하여 다른 경로로 리디렉션할 수 있습니다.

```tsx
import { redirect } from "react-router-dom";

const loader = async () => {
  const user = await getUser();
  if (!user) {
    return redirect("/login");
  }
  return null;
};
```

실제 `redirect`에 대한 바로가기 예시입니다.

```tsx
new Response("", {
  status: 302,
  headers: {
    Location: someUrl,
  },
});
```

`redirect`가 데이터에 대한 응답일 때는 컴포넌트에서 내비게이트를 사용하는 것보다 `loaders`와 `actions`에 `redirect`를 사용하는 것이 좋습니다.

참고용으로 좋은 문서 

- [Returning Responses from Loaders]('https://reactrouter.com/en/main/route/loader#returning-responses')
