# Exception ? (Error vs Exception)
### Exception
- 프로그래밍에서 예외란 `입력 값에 대한 처리가 불가능`하거나, 프로그램 실행중에 `참조된 값이 잘못된 경우` 등 `정상적인 흐름에서 어긋난 것`을 말함.
- java 에서는 `개발자가` 직접 예외 상항을 `미리 예측하여 핸들링 할 수 있음`.
- 예외는 개발자가 구현한 로직에서 발생. 즉, 예외는 개발자가 처리할 수 있기 때문에 

### Error
- `오류`는 시스템에 무엇인가 `비정상적인 상황이 생겼을 경우`에 발생됨.
- 이는 시스템 레벨에서 발생하기 때문에 심각한 수준의 오류이다.
- 개발자가 미리 예측하여 처리할 수 없음.
- OutOfMemoryError나 ThreadDeath 같은 에러는 catch 블록으로 잡아봤자 대응 방법이 없음.

# Exception Class
- 모든 예외 클래스는 `Throwable 클래스를 상속` 받고 있다.
- Throwable은  최상위 클래스 `Object의 자식 클래스`이다.

## Checked Exception vs Unchecked Exception
- 간단하게 `RuntimeException`을 `상속하지 않은 클래스는 Checked Exception`, 반대로 `상속한 클래스는 Unchecked Exception`으로 분류.
- Checked Exception과 Unchecked Exception의 가장 명확한 구분 기준은 `'꼭 처리를 해야 하느냐'`이다.

### Exception과 체크 예외
- Exception 클래스와 그 서브클래스로 정의되는 예외들은 에러와 달리 개발자들이 만든 애플리케이션 코드의 작업 중에 예외상황이 발생했을 경우 사용된다.
- 일반적으로 예외라고 하면 `RuntimeException을 상속하지 않은` 것만을 말하는 체크 예외라고 생각해도 된다.
- `체크예외가 발생할 수 있는` 메소드라면 반드시 로직을 try/catch로 감싸거나 throw로 던져서 처리해야 한다. 그렇지 않으면 컴파일 에러가 발생한다.
- 자바 언어와 JDK 초기 설계자들은 체크 예외를 발생 가능한 예외에 모두 적용하려 했던 것 같다. 그래서 IOException이나 SQLException을 비롯해서 예외적인 상황에서 `던져질 가능성이 있는것들은 대부분 체크 예외로 만들어져 있다.`
- `컴파일 단계`에서 `명확하게 Exception 체크가 가능한것`을 `Checked Exception`이라 한다.

### RuntimeException과 언체크/런타임 예외
- RuntimeException 클래스를 상속한 예외들은 `명시적인 예외처리를 강제 하지 않기 때문에` 언체크 예외라 불린다. 또는 대표 클래스 이름을 따서 런타임 예외라고도 한다.
- 런타임 예외는 주로 프로그램의 오류가 있을 때 발생하도록 의도 되었다.
- 대표적으로 오브젝트를 할당하지 않은 레퍼런스 변수를 사용하려 시도했을 때 발생하는 NullPointerException, 허용되지 않은 값을 사용해서 메서드를 호출할 때 발생하는 IllegalArgumentException 등이 있다.
- 이렇게 개발자가 부주의해서 발생할 수 있는 경우에 발생하도록 만든 것이 런타임 예외다.
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
- 예외가 발생하면 다른 작업 흐름으로 유도한다.
- 예외사항을 파악하고 문제를 해결해서 정상 상태로 돌려놓는 것이다.
- 예외 상황이 발생했을 때 사용자에게 상황을 알려주고 다른 방법을 안내해서 예외상황을 해결할 수 있다. 
- 단, 에러 메세지가 사용자에게 그냥 던져지는 것은 예외 복구라고 볼 수 없다.
- 예외가 처리됐으면 비록 기능적으로는 사용자에게 예외상황으로 비쳐도 애플리케이션에서는 정상적으로 `설계된 흐름을 따라 진행돼야 한다.`

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
- 예외복구의 핵심은 `예외가 발생하여도` 애플리케이션은 `정상적인 흐름으로 진행`된다는 것이다.
- 위 예제는 네트워크 환경이 좋지 않아서 서버에 접속이 안되는 상황의 시스템에 적용하면 효율적이다.
- 예외가 발생하면 일정 시간만큼 대기하고 다시 재시도를 반복한다.
- 최대 재시도 횟수를 넘기면 예외를 발생시킨다.

### 예외 처리 회피
- 예외처리를 하지 않고 호출한 쪽으로 던져버린다.
- 예외처리를 회피하려면 반드시 다른 오브젝트나 메서드가 예외를 처리할 수 있도록 던져줘야 한다.

```java
//예시 1
public void add() throws SQLException {
    ...
}

//예시 2
public void add() throws SQLException {
    try {

    } catch (SQLException e) {
        // 다른 처리를 하고 다시 예외를 던진다.
        throw e;
    }    
}
```

- 위 예제는 간단해 보이지만 아주 신중해야하는 로직이다.
- 예외가 발생하면 throws를 통해 호출한쪽으로 예외를 던지고 그 처리를 회피한다.
- 무책임하게 던지는 것은 위험하며 호출한 쪽에서 다시 예외를 받아 처리하도록 하거나, 해당 메소드에서 이 예외를 던지는 것이 최선의 방법이라는 확신이 있을 때만 사용해야 한다.
- 예외를 회피하는 것은 예외를 복구하는 것처럼 의도가 분명해야 한다.
- 구체적인 예외를 던지기 귀찮아서 모든 예외를 생각없이 던지게 하는 throws Exception 사용을 피해야 한다.

### 예외 전환
- 예외를 처리하는 방법은 예외 전환을 하는 것이다.
- 발생한 예외를 그대로 던지는게 아니라 `적절한 예외(명확한 의미를 가진)로 전환하여 던지는` 특징이 있다.

```java
// 조금 더 명확한 예외로 던진다.
public void add(User user) throws DuplicateUserIdException, SQLException {
    try {
        ...
    } catch (SQLException e) {
        // ErrorCode가 MySQL의 "Duplicate Entry(1062)"이면 예외 전환
        if (e.gerErrorCode() == MysqlErrorNumbers.ER_DUP_ENTRY) {
            throw DuplicateUserIdException();
        } else {
            throw e; // 그 외의 경우는 SQLException 그대로
        }
    }
}
```

- 위 예제는 사용자 등록을 시도했을 때 같은 사용자가 있어서 DB 에러가 발생하여 SQLException이 발생하였다.
- 서비스 계층에 그대로 SQLException을 던질 경우 왜 예외가 발생했는지 쉽게 알 방법이 없다.
- 이럴때 의미를 분명하게 이해할 수 있는 DuplicateUserIdException을 던져 주면 적절한 복구 작업을 시도할 수 있다.
- 서비스 계층에서 SQLException의 원인을 해석해서 대응하는 것도 불가능하지 않지만, 특정 기술의 정보를 해석하는 코드를 비즈니스 로직에 담는 것은 어색하다.

```java
// 예외를 단순하게 포장한다.
public void someMethod() {
    try {
        ...
    } catch (SQLException se) {
        throw new EJBException(se);
    } catch (RemoteException re) {
        throw new EJBException(re);
    }
}
```

- 예외처리 회피와 비슷하게 메서드 밖으로 예외를 던지지만, 그냥 던지지 않고 적절한 예외로 전환하여 넘기는 방법이다.
- 명확한 의미로 전달되기 위해 적합한 의미를 가진 예외로 변경한다.
- 예외 처리를 단순하게 만들기 위해 포장(Wrap) 할 수도 있다.
- 하지만 의미를 명확하게 하려고 다른 예외로 전환하는 것이 아니다. 주로 예외처리를 강제하는 체크 예외를 언체크 예외인 런타임 예외로 바꾸는 경우에 사용한다.
- SQLException이 웹 컨트롤러 메서드까지 명시적으로 전달되는것 보다 복구가 불가능한 예외라면 가능한 한 빨리 런타임 예외로 포장해서 던지는게 좋다. 다른 계층의 메서드를 작성할 때 불필요한 throws 선언이 들어가지 않도록 해줘야 한다.
- 복구하지 못할 예외라면 런타임 예외로 포장해서 던져버리고, 예외처리 서비스 등을 이용하여 자세한 로그를 남기고, 관리자에게는 메일 등으로 통보해주고, 사용자에게는 친절한 안내 메시지를 보여주는 식으로 처리하는게 바람직하다.

<br>

## 나쁜 습관

<br>

```java
try {
    ...
} catch (SQLException e) {

}
```

- 위 예제를 보면 try/catch를 사용해서 하였지만 예외 발생시 아무것도 하지 않고 그냥 넘어가 버렸다. 
- 이렇게 그냥 넘어가는것은 위험하다. 왜냐하면 프로그램 실행중 오류가 있어서 예외가 발생하였는데 그것을 무시하고 계속 진행해버리기 때문이다.

## 참고
- [자바 예외 구분](https://madplay.github.io/post/java-checked-unchecked-exceptions)
- [Java 예외 처리에 대한 작은 생각](https://www.nextree.co.kr/p3239/)
- 토비의 스프링