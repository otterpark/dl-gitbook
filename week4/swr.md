# SWR

```tsx
import useSWR from 'swr'
 
function Profile() {
  const { data, error, isLoading } = useSWR('/api/user', fetcher)
 
  if (error) return <div>failed to load</div>
  if (isLoading) return <div>loading...</div>
  return <div>hello {data.name}!</div>
}
```

이 예시에서, `useSWR` hook은 `key` 문자열과 `fetcher` 함수를 받습니다. `key`는 데이터의 고유한 식별자이며(일반적으로 API URL) `fetcher`로 전달될 것입니다. `fetcher`는 데이터를 반환하는 어떠한 비동기 함수도 될 수 있습니다. 네이티브 `fetch` 또는 `Axios`와 같은 도구를 사용할 수 있습니다.

hook은 두 개의 값을 반환합니다: 요청의 상태에 기반한 `data`와 `error`.

## 기능

- 빠르고, 가볍고, 재사용 가능한 데이터 가져오기
- 내장된 캐시 및 요청 중복 제거
- 실시간 경험
- 전송 및 프로토콜에 구애받지 않음
- SSR / ISR / SSG support
- TypeScript 준비
- React Native
