# REST(Representational State Transfer)
---
### 개념
자원을 이름으로 구분하고 자원의 상태를 원하는 형태로 주고 받는 모든 것을 의미한다.  
HTTP URI에 자원을 표현하고 Method(GET, POST, PUT, DELETE)를 통해 해당 자원을 처리한다.  

### 구성 요소
- Resource(자원)
    - 모든 자원에 대한 고유값인 ID가 존재
    - 자원을 구별하는 ID는 URI
    - 클라이언트는 URI를 통해 자원을 명시하고 자원에 대한 상태 조작을 서버에 요청
- Verb(행위)
    - GET(조회)
    - POST(추가)
    - PUT(수정)
    - DELETE(삭제)
- Representation of Resource(표현)
    - 클라이언트의 요청에 서버는 응답을 보낸다
    - JSON, XML의 형태로 나타낸다.

### 특징
##### 1. Client-Server 구조
클라이언트에서 서버로 자원을 요청하는 구조
- REST Server: API를 제공하며 비즈니스 로직을 수행한다.
- Client: 인증과 context(세션, 로그인정보) 관리한다.

##### 2. Stateless(무상태)
- HTTP 프로토콜에 기반하여 REST도 Stateless이다
- context를 서버에 저장하지 않는다.
- 서버는 각 요청에 대해 독립적으로 인식하고 처리한다.

##### 3. Cacheable(캐시 처리)
HTTP 프로토콜을 그대로 사용하므로 HTTP의 캐싱 기능을 사용할 수 있다.
- 대량 요청에 대한 성능을 위한 캐싱이 가능하다.
- 서비스의 대부분의 트렌젝션이 조회이므로 캐싱 기능이 성능 향상이 가능하다.

##### 4. Layered System(계층화)
- REST Server는 다중 계층 구조 가능
- PROXY, Gateway와 같은 middleware 사용할 수 있다.

##### 5. Uniform Interface(인터페이스 일관성)
HTTP 프로토콜을 사용하는 모든 플랫폼에서 사용 가능하다.

# REST API
### API(Application Programming Interface)
데이터와 기능을 프로그램 간에 통신할 수 있게 해주는 매개체

### REST API
- REST 기반으로 API를 구현
- MSA와 OpenAPI 등이 REST API 기반으로 만들어진 프로그램

### API 설계
- URI
    - Resource는 동사보단 명사로 표현한다.
    - 대문자보다는 소문자를 사용한다.
    - 리소스간 관계를 "/"로 표현한다.
    Ex) "song"이 가지고 디바이스 목록 -> /users/song/devices
    - 밑줄(_)은 사용하지 않는다.
    - 확장자는 사용하지 않는다.
    - URI 마지막에 슬래시(/)를 넣지 않는다.
- Method
    - Method는 URI에 들어가면 안된다.
    Ex) GET /users/delete/song (X) -> DELETE /users/song (O)
    - 상태에 대한 동사 표현이 들어가면 안된다.
    Ex) GET /users/get (X) -> GET /users (O)

### 상태 코드
- 2XX: 요청 성공
- 4XX: 클라이언트 오류
    - 400: Bad Request : 필드 유효성 실패
    - 401: Unauthorized : 인증 실패
    - 404: Not Found: 해당 리소스 없음
- 5XX: 서버 오류
    -500: Internal Server Error: 서버 에러

