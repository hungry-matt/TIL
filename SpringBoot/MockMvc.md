# MockMvc
테스트에 필요한 기능만 가지는 가짜 객체를 만들어서 스프링 MVC 동작을 재현할 수 있는 클래스를 의미.

## perform()
- 요청을 전송하는 역할을 한다. 결과로 ResultActions 객체를 받으며, ResultActions 객체는 리턴 값을 검증하고 확인 할 수 있는 andExpect() 메소드를 제공 한다.

## get("/hello")
- HTTP 메소드를 결정 할 수 있다. (get(), post(), put(), delete())
- 인자로는 경로를 보내준다.

## params(info)
- 키=값의 파라미터를 전달할 수 있다.
- 여러 개일 때는 params()를, 하나일 때에는 param()을 사용 한다.

## andExpect()
- 응답을 검증하는 역할을 한다.
- status() 
    - isOk() : 200
    - isNotFound() : 404
    - isMethodNotAllowed() : 405
    - isInternalServerError() : 500
    - is(int status) : status 상태 코드
- view()
    - 리턴하는 뷰 이름을 검증.
    - view().name("test")
- redirect()
    - 리다이렉트 응답을 검증.
    - redirectUrl("/test")
- model()
    - 컨트롤러에서 저장한 모델들의 정보 검증
- content()
    - 응답에 대한 정보를 검증

## andDo(print())
- 요청/응답 전체 메세지를 확인할 수 있다.