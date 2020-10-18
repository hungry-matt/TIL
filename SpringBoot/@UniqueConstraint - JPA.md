# @UniqueConstraints
JPA 에서 Entity 클래스 Unique key 설정은 아래와 같다.

```java
@Column(name="column", unique=true)
Long id;
```

하지만 위 방식은 두개 이상의 컬럼을 Unique key 로 설정할 수 없다.

따라서 @Table 에 UniqueConstraints를 걸어주면 해결 된다.

```java
@Table(
    name="columne"
    , uniqueConstraints = {
        @UniqueConstraint(
            conlumnNames = {"column1", "column2"}
        )
    }
)
public class Test {
    @Column(name="column1")
    private String name;

    @Column(name="column2")
    private String email;
}
```
