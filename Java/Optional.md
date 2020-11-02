# Optional 
Optional<T> 클래스는 'T' 타입의 객체를 포장해 주는 래퍼 클래스 이다.
따라서 Optinal 인스턴스는 모든 타입의 참조 변수를 저장할 수 있다.

# Why
Optional 클래스는 어떤 이유에서 생겨나게 되었을까?

## Java 8 Optional
Optional은 Java 8 에서 최초로 도입 되었다. 도입된 이유는 바로 null 때문이다. null은 프로그래머에게 편안한 보다는 불편함을 더 많이 제공 한다. 

아래 코드를 보면 User 클래스는 한 사람의 정보를 표현 한다. 

```java
public void test(Long id) {
    User user = userRepository.findById(id);
}
```

아이디에 해당하는 사용자가 있다면 잘 실행 될것이다. 그런데 만약 사용자가 없다면 어떻게 될까?

위 코드를 실행하게 되면 NPE 예외가 일어나서 프로그램이 제대로 수행되지 않게 된다.

# How
Optional 클래스는 어떻게 사용할 수 있을까?

아래 코드와 같이 작성할 수 있으며 null 값으로 인해 발생하는 예외를 처리할 수 있다.

```java
public void test(Long id) {
    Optional<User> user = userRepository.findById(id).orElseThrow(new Exception());
}
```