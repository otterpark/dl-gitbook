# React query

웹 애플리케이션에서 서버 상태를 가져오고, 캐싱하고, 동기화하고, 업데이트하는 작업을 손쉽게 해줍니다.

React Query는 서버 상태 관리를 위한 최고의 라이브러리 중 하나이다. 별도의 설정없이 바로 사용 가능하며, 애플리케이션이 성장함에 따라 원하는 대로 커스터마이징이 가능합니다.

- 애플리케이션에서 복잡하고 오해의 소지가 있는 여러 줄의 코드를 제거하고 몇 줄의 React Query 로직으로 대체할 수 있습니다.
- 새로운 서버 상태 데이터 소스를 연결할 걱정 없이 애플리케이션의 유지보수를 개선하고 - 새로운 기능을 더 쉽게 구축할 수 있습니다.
- 애플리케이션의 속도와 반응성이 그 어느 때보다 빨라져 최종 사용자에게 직접적인 영향을 미칩니다.
- 잠재적으로 대역폭을 절약하고 메모리 성능을 향상시킬 수 있습니다.

```tsx

  QueryClient,
  QueryClientProvider,
  useQuery,
} from '@tanstack/react-query'

const queryClient = new QueryClient()

export default function App() {
  return (
    <QueryClientProvider client={queryClient}>
      <Example />
    </QueryClientProvider>
  )
}

function Example() {
  const { isLoading, error, data } = useQuery({
    queryKey: ['repoData'],
    queryFn: () =>
      fetch('https://api.github.com/repos/tannerlinsley/react-query').then(
        (res) => res.json(),
      ),
  })

  if (isLoading) return 'Loading...'

  if (error) return 'An error has occurred: ' + error.message

  return (
    <div>
      <h1>{data.name}</h1>
      <p>{data.description}</p>
      <strong>👀 {data.subscribers_count}</strong>{' '}
      <strong>✨ {data.stargazers_count}</strong>{' '}
      <strong>🍴 {data.forks_count}</strong>
    </div>
  )
}
```