# Wath is java.util.function.Function
Funtion<T,R>은 Java 8에 도입된 내장 기능 인터페이스다. Function<T,R>이 생성된 주된 목적은 시나리오 매핑을 위한 것이다.

즉, 어떤 유형의 객체를 입력으로 가져가고 다른 형식으로 변환(또는 매핑)하는 경우.

## 기본 구조
```java
public interface Function<T, R> {
    R apply(T val1);
}
```

## 예시
```java
public class FunctionTest {
    private Function<String, Long> idExtractor;

    public FunctionTest(Function<String, Long> idExtractor) {
        this.idExtractor = idExtractor;
    }

    public test() {
        Id<User, Long> testId = idExtractor.apply("test"); //String 타입의 매개변수를 넘겨 Long 타입의 결과를 반환한다.

        if(testId.value() == 1L) {
            return true;
        }
    }
}

public class FunctionCall {
    public FunctionTest function() {
        return new FunctionTest((String text) -> {
            Long id = text.equals("test") ? 1L : 0L;
            return Id.of(User.class, id);
        });
    }
}
```


- https://www.javabrahman.com/java-8/java-8-java-util-function-function-tutorial-with-examples/
