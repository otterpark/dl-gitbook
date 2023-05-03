# usehooks-ts

React Custom Hook 라이브러리이며, Custom Hook을 만들기 전 참고하기 좋은 라이브러리이다.

## useBoolean

참/거짓을 다룰 땐 toggle 같이 의도가 명확한 함수를 쓰는 게 좋다.

```tsx
import { Dispatch, SetStateAction, useCallback, useState } from 'react'

interface UseBooleanOutput {
  value: boolean
  setValue: Dispatch<SetStateAction<boolean>>
  setTrue: () => void
  setFalse: () => void
  toggle: () => void
}

function useBoolean(defaultValue?: boolean): UseBooleanOutput {
  const [value, setValue] = useState(!!defaultValue)

  const setTrue = useCallback(() => setValue(true), [])
  const setFalse = useCallback(() => setValue(false), [])
  const toggle = useCallback(() => setValue(x => !x), [])

  return { value, setValue, setTrue, setFalse, toggle }
}

export default useBoolean
```

## useEffectOnce

기존 `useEffect` 의존성 배열을 빈 배열로 넣어서 한 번만 실행할 때가 많은데, 이걸 쓰면 더 명확히 드러난다.

```tsx
import { EffectCallback, useEffect } from 'react'

function useEffectOnce(effect: EffectCallback) {
  // eslint-disable-next-line react-hooks/exhaustive-deps
  useEffect(effect, [])
}

export default useEffectOnce
```

## useFetch

Fetch API를 사용하여 데이터를 검색하는 것을 목표로 하는 React Hook 입니다.
상태 로직을 분리하고 함수형 스타일을 통해 테스트를 단순화하기 위해 리듀서를 사용했으며, 수신된 데이터는 useRef를 통해 애플리케이션에 저장(캐시)되지만, 데이터를 지속시키기 위해 LocalStorage(useLocalStorage() 참조) 또는 캐싱 솔루션을 사용할 수 있습니다.

- SSR에서 사용하려면 window.fetch.polyfill을 사용하는 것을 고려하세요.
- 기본적인 사용 사례와 학습 목적으로 사용하기에 매우 간단한 페치 훅입니다. 고급 사용 및 최적화를 위해서는 `useSWR`, `useQuery`와 같은 더 강력한 후크를 참조하거나 `Redux 툴킷을 사용`하는 경우 `RTK Query`를 고려해 보세요.

## useInterval

React에서 setInterval 등을 쓸 때 주의해야 할 부분이 있어 Custom Hook을 만들어서 해결

```tsx
import { useEffect, useRef } from 'react'

import { useIsomorphicLayoutEffect } from 'usehooks-ts'

function useInterval(callback: () => void, delay: number | null) {
  const savedCallback = useRef(callback)

  // Remember the latest callback if it changes.
  useIsomorphicLayoutEffect(() => {
    savedCallback.current = callback
  }, [callback])

  // Set up the interval.
  useEffect(() => {
    // Don't schedule if no delay is specified.
    // Note: 0 is a valid value for delay.
    if (!delay && delay !== 0) {
      return
    }

    const id = setInterval(() => savedCallback.current(), delay)

    return () => clearInterval(id)
  }, [delay])
}

export default useInterval
```

### useEventListener(`강력 추천`)

모든 종류의 이벤트를 확인할 수 있음. 특히 dispatchEvent로 전달되는 커스텀 이벤트에 반응하기 좋다.

```tsx
import { RefObject, useEffect, useRef } from 'react'

import { useIsomorphicLayoutEffect } from 'usehooks-ts'

// MediaQueryList Event based useEventListener interface
function useEventListener<K extends keyof MediaQueryListEventMap>(
  eventName: K,
  handler: (event: MediaQueryListEventMap[K]) => void,
  element: RefObject<MediaQueryList>,
  options?: boolean | AddEventListenerOptions,
): void

// Window Event based useEventListener interface
function useEventListener<K extends keyof WindowEventMap>(
  eventName: K,
  handler: (event: WindowEventMap[K]) => void,
  element?: undefined,
  options?: boolean | AddEventListenerOptions,
): void

// Element Event based useEventListener interface
function useEventListener<
  K extends keyof HTMLElementEventMap,
  T extends HTMLElement = HTMLDivElement,
>(
  eventName: K,
  handler: (event: HTMLElementEventMap[K]) => void,
  element: RefObject<T>,
  options?: boolean | AddEventListenerOptions,
): void

// Document Event based useEventListener interface
function useEventListener<K extends keyof DocumentEventMap>(
  eventName: K,
  handler: (event: DocumentEventMap[K]) => void,
  element: RefObject<Document>,
  options?: boolean | AddEventListenerOptions,
): void

function useEventListener<
  KW extends keyof WindowEventMap,
  KH extends keyof HTMLElementEventMap,
  KM extends keyof MediaQueryListEventMap,
  T extends HTMLElement | MediaQueryList | void = void,
>(
  eventName: KW | KH | KM,
  handler: (
    event:
      | WindowEventMap[KW]
      | HTMLElementEventMap[KH]
      | MediaQueryListEventMap[KM]
      | Event,
  ) => void,
  element?: RefObject<T>,
  options?: boolean | AddEventListenerOptions,
) {
  // Create a ref that stores handler
  const savedHandler = useRef(handler)

  useIsomorphicLayoutEffect(() => {
    savedHandler.current = handler
  }, [handler])

  useEffect(() => {
    // Define the listening target
    const targetElement: T | Window = element?.current ?? window

    if (!(targetElement && targetElement.addEventListener)) return

    // Create event listener that calls handler function stored in ref
    const listener: typeof handler = event => savedHandler.current(event)

    targetElement.addEventListener(eventName, listener, options)

    // Remove event listener on cleanup
    return () => {
      targetElement.removeEventListener(eventName, listener, options)
    }
  }, [eventName, element, options])
}

export default useEventListener
```

### useLocalStorage

localStorage와 JSON으로 객체 영속화한다. 페이지가 새로 고침 후에도 로컬 저장소로 상태를 유지할 수 있으며, `다크모드`에 유용하다.

- 이벤트를 통해(dispatchEvent + useEventListener) 다른 컴포넌트와 동기화하는 게 매우 중요한 특징.
- LocalStorage에서 읽기만 하려면 `useReadLocalStorage()`를 참조

### useDarkMode

React Hook은 어두훈 테마 모드를 활성화, 비활성화, 토글 및 읽을 수 있는 인터페이스를 제공한다. return 값은 로직에 사용할 수 있는 `boolean` 값이다.

```tsx
import { useLocalStorage, useMediaQuery, useUpdateEffect } from 'usehooks-ts'

const COLOR_SCHEME_QUERY = '(prefers-color-scheme: dark)'

interface UseDarkModeOutput {
  isDarkMode: boolean
  toggle: () => void
  enable: () => void
  disable: () => void
}

function useDarkMode(defaultValue?: boolean): UseDarkModeOutput {
  const isDarkOS = useMediaQuery(COLOR_SCHEME_QUERY)
  const [isDarkMode, setDarkMode] = useLocalStorage<boolean>(
    'usehooks-ts-dark-mode',
    defaultValue ?? isDarkOS ?? false,
  )

  // Update darkMode if os prefers changes
  useUpdateEffect(() => {
    setDarkMode(isDarkOS)
    // eslint-disable-next-line react-hooks/exhaustive-deps
  }, [isDarkOS])

  return {
    isDarkMode,
    toggle: () => setDarkMode(prev => !prev),
    enable: () => setDarkMode(true),
    disable: () => setDarkMode(false),
  }
}

export default useDarkMode
```