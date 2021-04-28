# Mock Annotaion 을 사용중인 field 초기화
Mockito 에서 제공하는 @Mock, @Spy, @InjectMocks 과 같은 annotation을 사용하는 field를 초기화 하는 방법은 아래와 같다.

```java
@RunWith(MockitoRunner.class)
public class test {

}
```

```java
public class test {
    @Before
    public void setup() {
        MockitoAnnotaion.initMocks(this);
    }
}
```

