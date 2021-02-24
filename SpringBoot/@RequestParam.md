# RequestParam
RequestParam 어노테이션은 단일 [파라미터를 전달 받을 때] 사용 된다.

> 단일 HTTP 요청 파라미터를 메소드 파라미터로 넣어주는 애노테이션이다.

### 기본 작성 방식

```java
@PostMapping("/test")
public void test(@RequestParam("name") String name) {};
```

#### required, defaultValue
지정된 RequestParam 값이 넘어 오지 않을 경우 400 (Bad Request) 에러가 발생 한다. 이를 방지 하기 위해 아래와 같이 작성 한다.

```java
@PostMapping("/test")
public void test(@RequestParam(value="name", required=false, defaultValue="none") String name) {};
```

### 멀티 파라미터
여러개의 파라미터를 한꺼번에 넘길 경우 Map 사용한다.

```java
@PostMapping("/test")
public void test(@RequestParam Map<String, Object> paramMap) {};
```