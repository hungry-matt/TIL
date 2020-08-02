# Dependency Injection

- 하나의 객체를 다른 객체에 의존성을 제공 한다.

- 의존대상(사용할 객체)을 주입을 통해 받는 방식.

- 느슨한 결합 상식.

## 주입 방식

### 생성자
- 스프링 4.3 부터는 @Autowired 생략 가능 (단 생성자 클래스와 주입 받을 객체가 bean으로 등록 됬을시에만)

```java
class OwnerController {
    @Autowired
    public OwnerController(OwnerRepository repository) {
        this.owners = repository;
    }
}

```

### 필드

- 지양해야 하는 이유
    - 단일 책임의 원칙 위반
    - 객체가 변할수 있음

```java
@Autowired
private OwnerRepository owners;
```

### Setter

- IoC 컨테이너가 인스턴스를 만들고 나서 setter를 찾아 의존성을 주입 해준다.

```java
@Autowired
public void setOwners(OwnerRepository owners) {
    this.owners = owners;
}
```

