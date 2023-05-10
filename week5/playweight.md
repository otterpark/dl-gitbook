# Playweight

## E2E(End-to-End) Test

`E2E(End-to-End) Test`는 애플리케이션이 예상대로 작동하고 **모든 종류의 사용자 작업 및 프로세스에 대해 데이터 흐름이 유지**되는지 확인하는 방법이다. 이러한 유형의 테스트 접근 방식은 최종 사용자의 관점에서 시작하여 실제 `시나리오`를 시뮬레이션합니다.

## Headless Chrome

Chrome 59 버전부터는 명령행에서 옵션으로 실행할 수 있는 `Headless` 모드가 추가되었습니다. 여기서 `Headless` 모드란 별도의 GUI 창이 뜨지 않고 사이트에 접속해서 페이지를 받는 등의 작업을 실행할 수 있습니다.

정리해보면, **브라우저를 사용할 때처럼 화면에 창이 시각적으로 보이지 않지만 실제 띄워진 화면에서 화면 테스트를 하듯 테스트**를 할 수 있다.

> 실제 E2E 테스트 시 내가 작업하는 도중 브라우저가 띄워지고 후다닥 테스트 하는 모습을 보기 싫다면 `Headless` 모드로 설정한 후 테스트를 진행하면 된다.

## Puppeteer

웹 테스트 및 자동화를 위한 프레임워크이며, 프레임워크 사용 시 단일 API로  `Chromium`, `Firefox` 및 `WebKit`을 테스트할 수 있다. 

> 빠른 크로스 브라우저 웹 자동화를 지원

## Playwright

`Playwright` 테스트는 `E2E(End-to-End) Test`의 요구 사항을 수용하기 위해 특별히 개발되었습니다. `Playwright`는 `Chromium`, `WebKit`, `Firefox`를 포함한 **모든 최신 렌더링 엔진을 지원**합니다. 

```tsx
import { test, expect } from '@playwright/test';

test('basic test', async ({ page }) => {
  await page.goto('https://playwright.dev/');
  const name = await page.innerText('.navbar__title');
  expect(name).toBe('Playwright');
});
```

## CodeceptJS

CodeceptJS는 특별한 BDD 스타일 구문을 사용하는 `E2E(End-to-End) Test` 프레임워크입니다. 테스트는 사이트에서 사용자의 동작에 대한 선형 시나리오로 작성됩니다.

```tsx
Feature('CodeceptJS demo');

Scenario('check Welcome page on site', ({ I }) => {
  I.amOnPage('/');
  I.see('Welcome');
});
```

`Playwright` 보다는 조금 더 인간 친화적인 `E2E Testing` 도구로 사용되고 있다. 결국 프론트엔드는 백엔드 및 기획자와 소통이 필요한데 인간 친화적이라 소통에 도움이 된다.
