# Exception ? (Error vs Exception)
### Exception
- 프로그래밍에서 예외란 `입력 값에 대한 처리가 불가능`하거나, 프로그램 실행중에 `참조된 값이 잘못된 경우` 등 `정상적인 흐름에서 어긋난 것`을 말함.
- java 에서는 `개발자가` 직접 예외 상항을 `미리 예측하여 핸들링 할 수 있음`.
- 예외는 개발자가 구현한 로직에서 발생. 즉, 예외는 개발자가 처리할 수 있기 때문에 

### Error
- `오류`는 시스템에 무엇인가 `비정상적인 상황이 생겼을 경우`에 발생됨.
- 이는 시스템 레벨에서 발생하기 때문에 심각한 수준의 오류이다.
- 개발자가 미리 예측하여 처리할 수 없음.

# Exception Class
- 모든 예외 클래스는 `Throwable 클래스를 상속` 받고 있다.
- Throwable은  최상위 클래스 `Object의 자식 클래스`이다.

## Checked Exception vs Unchecked Exception
- 간단하게 `RuntimeException`을 `상속하지 않은 클래스는 Checked Exception`, 반대로 `상속한 클래스는 Unchecked Exception`으로 분류.
- Checked Exception과 Unchecked Exception의 가장 명확한 구분 기준은 '꼭 처리를 해야 하느냐'이다.
- Checked Exception이 발생할 가능성이 있는 메소드라면 반드시 로직을 try/catch로 감싸거나 throw로 던져서 처리해야 한다.
- `컴파일 단계`에서 `명확하게 Exception 체크가 가능한것`을 `Checked Exception`이라 한다.
- `실행과정 중` 어떠한 `특정 논리에 의해 발견되는 Exception`을 `Unchecked Exception`이라 한다.

구분 | Checked Exception | Unchecked Exception
---|---|---
처리 여부 | 반드시 예외를 처리 | 예외 처리를 강제하지 않음
확인 시점 | 컴파일 단계 | 실행(Runtime) 단계
예외 발생시 트랜잭션 처리 | Roll-Back 하지 않음 | Roll-Back 함
예외 종류 | RuntimeException을 제외한 모든 예외(IOException, ClassNotFountException 등) | RuntimeException 하위 예외(NullPointerException, ClassCastException 등)

## 예외 처리
예외를 처리하는 방법에는 `예외 복구`, `예외 처리 회피`, `예외 전환` 방법이 있다.

### 예외 복구
예외가 발생하면 다른 작업 흐름으로 유도한다.

```java
final int MAX_RETRY = 100;

public Object someMethod() {
    int maxRetry = MAX_RETRY;

    while(maxRetry > 0) {
        try {
            // 예외가 발생할 가능성이 있는 시도
        } catch (SomeException e) {
            // 로그 출력. 정해진 시간만큼 대기
        } finally {
            // 리소스 반납 및 정리 작업
        }
    }

    // 최대 재시도 횟수를 넘기면 직접 예외를 발생시킨다.
    throw new RetryFailedException();
}
```
- 예외복구의 핵심은 예외가 발생하여도 애플리케이션은 정장적인 흐름으로 진행된다는 것이다.
- 위 예제는 네트워크 환경이 좋지 않아서 서버에 접속이 안되는 상황의 시스템에 적용하면 효율적이다.
- 예외가 발생하면 일정 시간만큼 대기하고 다시 재시도를 반복한다.
- 최대 재시도 횟수를 넘기면 예외를 발생시킨다.

### 예외 처리 회피
처리를 하지 않고 호출한 쪽으로 던져버린다.

### 예외 전환
호출한 쪽으로 던질 때 명확한 의미를 전달하기 위해 다른 예외로 전환하여 던진다.


## 참고
- [자바 예외 구분](https://madplay.github.io/post/java-checked-unchecked-exceptions)
- [Java 예외 처리에 대한 작은 생각](https://www.nextree.co.kr/p3239/)