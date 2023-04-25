# REST API vs Graphql

REST API는 URL, METHOD 등을 조합하기 때문에 다양한 `EndPoint`가 존재합니다. 반면 GraphQL은 단 하나의 `EndPoint`가 존재합니다. 또한 GraphQL API에서 불러오는 데이터 종류를 쿼리 조합을 통해 결정합니다.

- `REST API` - 각 EndPoint마다 데이터베이스 SQL 쿼리가 달라진다.
- `GraphQL API` - GraphQL 스키마의 타입마다 데이터베이스 SQL 쿼리가 달라진다.

![graphql-stack](/week3/img/graphql-stack.png)

![graphql-mobile-api](/week3/img/graphql-mobile-api.png)

위 그림처럼 Graphql API를 사용하면 여러번 네트워크 호출을 할 필요 없이, 한번에 네트워크 호출로 처리할 수 있습니다.
