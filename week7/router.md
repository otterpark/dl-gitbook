# Router

네트워크와 네트워크 간의 경로(Route)를 설정하고 가장 빠른 길로 트래픽을 이끌어주는 네트워크 장치이다.

> 패킷의 위치를 추출하여, 그 위치에 대한 최적의 경로를 지정하며, 이 경로에 따라 데이터 패킷을 다음 장치로 전향시키는 장치

![Router](./img/router.png)

## Routing이란?

사용자가 요청한 URL에 따라 해당 URL에 맞는 페이지를 모여주는 것

기존 웹 페이지 처럼 여러개의 페이지를 소용하는데 새로운 페이지를 로드하는 방식이 아닌 하나의 페이지 안에서 데이터만 가져오는 형태이다.

Routing 관련 많은 라이브러리가 이지만, 이 중에서 가장 많이 쓰이는 `React Router`가 있다.

## React Router란?

사용자가 신규 페이지를 불러오지 않은 상황에서 각각의 url에 따라 선택된 데이터를 하나의 페이지에서 렌더링 해주는 라이브러리이다.

사용자가 입력한 주소를 감지하여, 여러 환경에서 동작할 수 있도록 여러 종류의 라우터 컴포넌트를 제공한다.

`Context API`를 기반으로 한 라이브러리로 컨포넌트들에게 동일한 Context를 제공하고 한 번에 값을 받아와서 사용한다.

### BrowserRouter

URL을 사용하여 브라우저의 주소 표시줄에 현재 위치를 저장하고 브라우저의 내장 기록 스택(document's `defaultView`)을 사용하여 탐색합니다.

> HTML5를 지원하는 브라우저의 주소를 감지

```tsx
import * as React from "react";
import { createRoot } from "react-dom/client";
import { BrowserRouter } from "react-router-dom";

const root = createRoot(document.getElementById("root"));

root.render(
  <BrowserRouter>
    {/* The rest of your app goes here */}
  </BrowserRouter>
);
```

### `Route`

**URL 세그먼트와 컴포넌트, 데이터 로딩 및 데이터 변형을 연결**합니다. 경로 중첩을 통해 **복잡한 애플리케이션 레이아웃과 데이터 종속성을 단순하고 선언적**으로 만들 수 있습니다.

> 라우터는 라우터 생성 함수에 전달되는 객체입니다

```tsx
const router = createBrowserRouter(
  createRoutesFromElements(
    <Route
      element={<Team />}
      path="teams/:teamId"
      loader={async ({ params }) => {
        return fetch(
          `/fake/api/teams/${params.teamId}.json`
        );
      }}
      action={async ({ request }) => {
        return updateFakeTeam(await request.formData());
      }}
      errorElement={<ErrorBoundary />}
    />
  )
);
```

### `MemoryRouter`

내부적으로 배열에 위치를 저장합니다. `<BrowserHistory>` 와 `<HashHistory>`와 달리 브라우저의 히스트리 스택과 같이 외부 소스에 연결되지 않습니다. 따라서 테스트 코드를 작성할 때 히스토리 스택을 완벽하게 제어해야 하는 시나리오가 제일 이상적이다.

- `<MemoryRouter initialEntries>` - 기본값은 ["/"](루트/URL에 있는 단일 항목)입니다.
- `<MemoryRouter initialIndex>` - 초기 항목의 마지막 인덱스를 기본값으로 한다.

#### 💡 TIP

대부분의 React 라우터 테스트는 `<MemoryRouter>`를 소스로 사용하여 작성되었으므로, 테스트를 살펴보는 것만으로도 훌륭한 사용 예시를 확인할 수 있습니다.

```tsx
import * as React from "react";
import { create } from "react-test-renderer";
import {
  MemoryRouter,
  Routes,
  Route,
} from "react-router-dom";

describe("My app", () => {
  it("renders correctly", () => {
    let renderer = create(
      <MemoryRouter initialEntries={["/users/mjackson"]}>
        <Routes>
          <Route path="users" element={<Users />}>
            <Route path=":id" element={<UserProfile />} />
          </Route>
        </Routes>
      </MemoryRouter>
    );

    expect(renderer.toJSON()).toMatchSnapshot();
  });
});
```
