## HandlerMethodArgumentResolver

> Strategy interface for resolving method paramters into argument values in the context of a given request.
>
> 컨트롤러에 들어오는 파라미터를 커스터마이징 할때 사용할 수 있는 인터페이스로, 공통적으로 수행해야 하는 작업을 수행한 후 해당 Object를 반환함으로써 코드의 중복을 줄일 수 있다. 클라이언트의 요청이 담긴 파라미터를 컨트롤러보다 먼저 받아서 작업을 수행한다.

Instance Method | Description
---|:---|
Object resolveArgument(MethodParameter parameter, ModelAndViewContainer mavContainer, NativeWebRequest webRequest,WebDataBinderFactory binderFactory) | 공통작업 수행 후 리턴
boolean supportsParameter(MethodParameter parameter) | parameter가 해당 resolver에 의해 수행될 수 있는 타입인지 true/false로 리턴. 이 메소드가 먼저 수행되고 true일 시 resolveArgument를 수행한다.