# @WithMockUser
Spring Security 사용 시 인증되지 않은 사용자의 요청은 이동된다.

그래서 임의로 인증된 사용자들 추가 하여 API 테스트 코드를 작성하기 위해 사용한다.

WithMockUser 어노테이션을 사용하기 위해 다음과 같이 의존성을 추가해 준다.
```gradle
testCompile('org.springframework.security:spring-security-test)
```

```java
public class Test {
    @Test
    @WithMockUser(roles="USER")
    public void test() throws Exception {
        ...
    }
}
```
- 인증된 모의(가짜) 사용자를 만들어서 사용.
- roles 권한을 추가할 수 있음.
- 즉, ROLE_USER 권한을 가진 사용자가 API를 요청한것과 동일한 효과를 가짐.