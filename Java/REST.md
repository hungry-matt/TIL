# RESTful API
- `REST` 란, Representational State Transfer 의 약자이다. 
- 여기에 ~ful 이라는 형용사형 어미를 붙여 ~한 API 라는 표현으로 사용된다. 
- 즉, REST 의 기본 원칙을 성실히 지킨 서비스 디자인은 'RESTful' 하다 라고 표현할 수 있다.
- `REST` 는 ROA(`Resource Oriented Architecture`) 이다. API 설계의 중심에 자원(Resource)이 있고 HTTP Method 를 통해 자원을 처리하도록 설게하는 것이다.

## REST 6가지 원칙
- Uniform Interface
- Stateless
- Caching
- Client-server
- Hierarchical system
- Code on demand

## RESTful 하게 API 를 디자인 한다는것은 무엇을 의미하는가.
1. `리소스`와 `행위`를 명시적이고 직관적으로 분리한다.
- 리소스는 `URI` 로 표현되는데 리소스가 가리키는 것은 `명사`로 표현되어야 한다.
- 행위는 `HTTP Method` 로 표현하고, `GET(조회)`, `POST(생성)`, `PUT(기존 entity 전체 수정)`, `PATCH(기존 entity 일부 수정)`, `DELETE(삭제)` 을 분명한 목적으로 사용한다.