# Exception 처리
안정적인 프로그램이 될수 있도록 프로그램 실행중 발생한 에러 처리에 대해 작성

## Controller Test Code
에러를 발생 시켜 정상적으로 작동하는지 테스트 한다.

```java
@Test
public void test() {
    //찾는 데이터가 없을때 Exception Class 호출
    given(testService.getResource(404L)).willThrow(new TestNotFoundException(404L));
    mvc.perfom(get("/test/404"))
        .andExpect(status().isNotFound())
        .andExpect(content().string(containsString("Colud Not Found")));
}
```

## Exception Class
에러 발생시 처리할 코드를 작성 한다.

```java
//RuntimeException -> 프로그램 실행중 발생하는 Exception
public class TestNotFoundException extends RuntimeException{
    public TestNotFoundException(String msg, Throwbale t) {
        super(msg, t);
    }
    public TestNotFoundException(String msg) {
        super(msg);
    }
    public TestNotFoundException() {
        super();
    }
    public TestNotFoundException(Long id) {
        //RuntimeException 객체로 메세지를 전달할 수 있다.
        super("{Colud Not Found ID: }" + id);
    }
}
```

## Advice Class
Controller 전역에 작성된 Exception Class를 공통으로 관리 한다.

```java
//Controller 전역에 적용되는 코드를 작성 할 수 있다.
//@ControllerAdvice
//ControllerAdvice 와 Responsebody 가 합쳐진 어노테이션으로 Responsebody를 개별적으로 선언하지 않아도 된다.
@RestControllerAdvice
public class TestExceptionAdvice {

    // @Responsebody
    //Http 응답코드를 지정한 NOT_FOUND(404) 코드로 바꿔준다.
    @ResponseStatus(HttpStatus.NOT_FOUND)
    //Controller, RestController 가 적용된 Bean 내에서만 발생하는 예외를 잡아 메서드에서 처리해주는 기능 이다.
    //인자 class는 하나 이상 등록 가능 하다.
    //e.g.) @ExceptionHandler(TestNotFoundException.class, TestNullPointException.class)
    @ExceptionHandler(TestNotFoundException.class)
    public String handleNotFound(Exception e) {
        return "{" + e.getMessage() + "}";
    }
}
```

## Service Test Code
```java
@Test(expected = TestNotFoundException.class)
public void getResourceWithNotExisted() {
    testService.getResource(404L);
}
```

## Service Class
TDD 호출 메서드
```java
@Service
public class TestService {
    public String getResource(Long id) {
        return testRepository.findById(id).orElseThrow(() -> new TestNotFoundException.class);
    }
}
```

