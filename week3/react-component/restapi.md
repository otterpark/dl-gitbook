# REST API

- GET, POST, PUT/PATCH, DELETE (CRUD)
- Resource 중심

두 컴퓨터 시스템이 인터넷을 통해 정보를 안전하게 교환하기 위해 사용하는 인터페이스(`API`)입니다. `RESTful API`는 안전하고 신뢰할 수 있으며 효율적인 소프트웨어 통신 표준을 따르므로 이러한 정보 교환을 지원합니다.

## API란?

애플리케이션 프로그래밍 인터페이스(API)는 다른 소프트웨어 시스템과 통신하기 위해 따라야 하는 규칙을 정의합니다.

웹 API는 클라이언트와 웹 리소스 사이의 게이트웨이라고 생각할 수 있습니다.

### 클라이언트

웹에서 정보를 엑세스하려는 사용자입니다. 클라이언트는 API를 사용하는 사람이거나 소프트웨어 시스템일 수 있습니다.

### 리소스

리소스는 다양한 애플리케이션이 클라이언트에게 제공하는 정보입니다. 리소스 자체는 이미지, 동영상, 텍스트, 숫자 또는 모든 유형의 데이터 일 수 있습니다. 클라이언트에게 리소스를 제공하는 시스템을 `서버`라고 합니다.

- API를 사용해 리소스를 공유하고, 보안,  제어 및 인증을 유지하면서 웹 서비스를 제공
- 특정 내부 리소스에 엑세스할 수 있는 클라이언트를 결정하는데 도움을 줌

## REST(Representational State Transfer)란?

REST는 API 작동 방식에 대한 조건을 부과하는 소프트웨어 아키텍처입니다. REST 기반 아키텍처를 사용하여 대규모의 고성능 통신을 안정적으로 지원할 수 있습니다. REST 아키텍처 스타일을 따르는 API를 REST API라고 부르며, REST 아키텍쳐를 구현하는 웹 서비스를 RESTful 웹 서비스라고 합니다.

그럼 몇 가지 `REST 아키텍처 스타일의 원칙`을 알아보자!

### 균일한 인터페이스

균일한 인터페이스는 서버가 표준 형식으로 정보를 전송함을 나타내며, 모든 RESTful 웹 서비스 디자인의 기본입니다. 형식이 지정된 리소스를 REST에서 표현이라고 부르며, 이 형식은 서버 애플리케이션에 있는 리소스의 내부 표현과 다를 수 있습니다.

1. 요청은 리소스를 식별해야하고, 이를 위해 균일한 리소스 식별자를 사용합니다.
2. 클라이언트는 원하는 경우 리소스를 수정하거나 삭제하기에 충분한 정보를 리소스 표현에서 가지고 있습니다. 서버는 리소스를 자세히 설명하는 메타데이터를 전송하여 이 조건을 충족합니다.
3. 클라이언트는 표현을 추가로 처리하는 방법에 대한 정보를 수신합니다. 이를 위해 서버는 클라이언트가 리소스를 적절하게 사용할 수 있는 방법에 대한 메타데이터가 포함된 명확한 메시지를 전송합니다.
4. 클라이언트는 작업을 완료하는 데 필요한 다른 모든 관련 리소스에 대한 정보를 수신합니다. 이를 위해 서버는 클라이언트가 더 많은 리소스를 동적으로 검색할 수 있도록 표현에 하이퍼링크를 넣어 전송합니다.

### 무상태

서버가 이전의 모든 요청과 독립적으로 모든 클라이언트 요청을 완료하는 통신 방법이다. 클라이언트는 임의의 순서로 리소스를 요청할 수 있으며, 모든 요청은 무상태이거나 다른 요청과 분리됩니다. REST API 설계 제약 조건은 서버가 매번 요청을 완전히 이해해서 이행할 수 있음을 의미합니다.

### 계층화 시스템

계층화된 시스템 아키텍처에서 클라이언트는 클라이언트와 서버 사이의 다른 승인된 중개자에게 연결할 수 있으며 여전히 서버로부터도 응답을 받습니다. 서버는 요청을 다른 서버로 전달할 수도 있습니다. 클라이언트 요청을 이행하기 위해 함께 작동하는 보안, 애플리케이션 및 비즈니스 로직과 같은 여러 계층으로 여러 서버에서 실행되도록 RESTful 웹 서비스를 설계할 수 있습니다. 이러한 계층은 클라이언트에 보이지 않는 상태로 유지됩니다.

### 캐시 가능성

RESTful 웹 서비스는 서버 응답 시간을 개선하기 위해 클라이언트 또는 중개자에 일부 응답을 저장하는 프로세스인 캐싱을 지원합니다. 예를 들어 모든 페이지에 공통 머리글 및 바닥글 이미지가 있는 웹 사이트를 방문한다고 가정해 보겠습니다. 새로운 웹 사이트 페이지를 방문할 때마다 서버는 동일한 이미지를 다시 전송해야 합니다. 이를 피하기 위해 클라이언트는 첫 번째 응답 후에 해당 이미지를 캐싱하거나 저장한 다음 캐시에서 직접 이미지를 사용합니다. RESTful 웹 서비스는 캐시 가능 또는 캐시 불가능으로 정의되는 API 응답을 사용하여 캐싱을 제어합니다.

### 온디맨드 코드

REST 아키텍처 스타일에서 서버는 소프트웨어 프로그래밍 코드를 클라이언트에 전송하여 클라이언트 기능을 일시적으로 확장하거나 사용자 지정할 수 있습니다. 예를 들어, 웹 사이트에서 등록 양식을 작성하면 브라우저는 잘못된 전화번호와 같은 실수를 즉시 강조 표시합니다. 서버에서 전송한 코드로 인해 이 작업을 수행할 수 있습니다.

## RESTful API를 사용하면 어떤 장점이 있나요?

### 확장성

REST API를 구현하는 시스템은 REST가 클라이언트-서버 상호 작용을 최적화하기 때문에 효율적으로 크기 조정할 수 있습니다. 무상태는 서버가 과거 클라이언트 요청 정보를 유지할 필요가 없기 때문에 서버 로드를 제거합니다. 잘 관리된 캐싱은 일부 클라이언트-서버 상호 작용을 부분적으로 또는 완전히 제거합니다. 이러한 모든 기능은 성능을 저하시키는 통신 병목 현상을 일으키지 않으면서 확장성을 지원합니다.

### 유연성

RESTful 웹 서비스는 완전한 클라이언트-서버 분리를 지원합니다. 각 부분이 독립적으로 발전할 수 있도록 다양한 서버 구성 요소를 단순화하고 분리합니다. 서버 애플리케이션의 플랫폼 또는 기술 변경은 클라이언트 애플리케이션에 영향을 주지 않습니다. 애플리케이션 함수를 계층화하는 기능은 유연성을 더욱 향상시킵니다. 예를 들어, 개발자는 애플리케이션 로직을 다시 작성하지 않고도 데이터베이스 계층을 변경할 수 있습니다.

### 독립성

REST API는 사용되는 기술과 독립적입니다. API 설계에 영향을 주지 않고 다양한 프로그래밍 언어로 클라이언트 및 서버 애플리케이션을 모두 작성할 수 있습니다. 또한 통신에 영향을 주지 않고 양쪽의 기본 기술을 변경할 수 있습니다.

