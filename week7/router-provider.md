# ReactRouter

## RouterProvider

모든 데이터 라우터 객체는 컴포넌트로 전달되어 앱을 렌더링하고 나머지 데이터 API를 활성화합니다.

```tsx
import {
  createBrowserRouter,
  RouterProvider,
} from "react-router-dom";

const router = createBrowserRouter([
  {
    path: "/",
    element: <Root />,
    children: [
      {
        path: "dashboard",
        element: <Dashboard />,
      },
      {
        path: "about",
        element: <About />,
      },
    ],
  },
]);

ReactDOM.createRoot(document.getElementById("root")).render(
  <RouterProvider
    router={router}
    fallbackElement={<BigSpinner />}
  />
);
```

## fallbackElement

앱을 서버 렌더링하지 않는 경우, `createBrowserRouter`는 마운트할 때 일치하는 모든 경로 로더를 시작합니다. 이 시간 동안 사용자에게 앱이 작동 중이라는 표시를 제공하기 위해 폴백 엘리먼트를 제공할 수 있습니다. 

> 정적 호스팅 `TTFB`를 활용하는게 좋다.

```tsx
<RouterProvider
  router={router}
  fallbackElement={<SpinnerOfDoom />}
/>
```

## Test

테스트 시에는 아래와 같이 `createMemoryRouter`를 통해서 테스트를 진행하면 된다.

### App.tsx

```tsx
import { createBrowserRouter, RouterProvider } from 'react-router-dom';

import routes from './routes';

const router = createBrowserRouter(routes);

root.render((
 <React.StrictMode>
  <RouterProvider router={router} />
 </React.StrictMode>
));
```

### App.test.tsx

```tsx
describe('routes', () => { 
 function renderRouter(path: string) {
  const router = createMemoryRouter(routes, { initialEntries: [path] });
  render(<RouterProvider router={router} />);
 }
 
 context('when the current path is “/”', () => {
  it('renders the home page', () => {
   renderRouter('/');
 
   screen.getByText(/Hello/);
  });
 });
 
 context('when the current path is “/about”', () => {
  it('renders the about page', () => {
   renderRouter('/about');
 
   screen.getByText(/About/);
  });
 });
});
```
