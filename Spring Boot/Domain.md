# 도메인 모델에서 왜 set 메서드 사용을 지양 하는가?
의도치 않은 곳에서 데이터가 변경 되는걸 방지 하기 위해 set 메서드 사용을 지양해야 한다.

# 그럼 set 메서드를 사용하지 않고 어떻게 처리 해야 하는가?

1. 아래와 같은 set 메서드 사용을 지양 한다.
```java
User user =  new User();
user.setName("name");
```

2. 생성자를 통해서 필요한 데이터를 의존성 주입을 받아 처리 해야 한다.
```java
public class User {
    private final Long id;
    private String name;
    private int age;

    public User(Long id, String name) {
        this.id = id;
        this.name = name;
    }
}
```
