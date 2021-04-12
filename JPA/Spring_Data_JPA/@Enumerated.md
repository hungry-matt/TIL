# @Enumerated
```java
@Entity
public class ... {
    @Enumerated(EnumType.STRING)
    @Column(nullable = false)
    private Role role;
}

public enum Role {
    ...
}

```
- JPA로 데이터베이스에 저장할 때 Enum 값을 어떤 형태로 저장할지 결정.
- 기본적으로 int로 된 숫자가 저장.
- 숫자로 저장되면 데이베이스로 확인할 때 그 값이 무슨 코드를 의미하는 알 수가 없음.
- 그래서 문자열(EnumType.STRING)로 저장될 수 있도록 선언.