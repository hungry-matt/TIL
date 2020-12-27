# Builder pattern
>복합 객체의 생성 과정과 표현 방법을 분리하여 동일한 생성 절차에서 서로 다른 표현 결과를 만들 수 있게 하는 패턴
><br> (출처:위키백과)

위 설명을 풀어 보자면 아래와 같다.

### 동일한 생성 절차와 서로 다른 표현 결과
```java
public class Test {
    private String name;
    private int age;

    private Test(String name, int age) {
        this.name = name;
        this.age = age;
    }

    static public class Builder {
        private String name;
        private int age;

        public Builder() {}

        public Builder name(String name) {
            this.name = name;
            return this;
        }

        public Builder age(int age) {
            this.age = age;
            return this;
        }

        public Test build() {
            return new Test(name, age);
        }
    }

    public void main(String[] agrs) {
        //동일한 생성 절차
        //서로 다른 표현 결과 -> name : tester, age : 20
        Test tester1 = Test.Builder()
            .name("tester")
            .age(20)
            .build();
        
        //동일한 생성 절차
        //서로 다른 표현 결과 -> name : test, age : null
        Test tester2 = Test.Builder()
            .name("test")
            .build();
    }
}
```

빌더 패턴을 사용하면 어떤 필드에 어떤 인자를 넣을지 명확하게 알 수 있고 setter를 남용하지 않는 불변 객체로 생성 할 수 있다는 점에서 빌더 패턴을 사용하고 있다.

### 빌더 패턴의 장점
1. 객체 마다 들어가야할 인자가 각 각 다를 때 유연하게 사용.
2. setter 생성을 방지하고 불변객체 생성.
3. 필수 인자를 지정 가능.

필수 인자 지정
```java
static public class Builder {
    private Long id;

    //default constructor
    public Builder(Long id) {
        if (id == null) {
            throw new IllegalArgumentException("필수 값 누락");
        } else {
            this.id = id;
        }
    }

    public Test build() {
        return new Test(id);
    }
}
```

## Lombok @Builder
빌더 패턴을 직접 작성하지 않고 자동으로 생성해준다.

### 사용법
```java
@Builder
public class Test() {
    private name;

    public void main(String[] args) {
        Test.builder()
            .name("test")
            .build();
    }
}
```

### @Builder 사용시 주의사항
1. @Builder 사용시 모든 필드를 갖는 private 생성자를 기본 생성자로 생성.
1-1. 그래서 public getter, setter가 있어도 필드 초기화 할 수 없음.
1-2. Controller에서 인자값으로 받는 Dto로 활용시 오류 발생. (no Creators, like default construct, exist)
2. 직접 기본 생성자 정의시 @Builder가 모든 필드를 갖는 private 생성자를 생성 하지 않음.
2-1. 모든 필드를 갖는 생성자를 추가 하지 않으면 오류 발생.

### 기본 생성자 정의시 왜 @Builder가 private 생성자를 만들어 주지 않을까?
>일단, 의미 상 빌더 패턴을 생각해 보았을 때, 아무것도 없는 생성자는 필요가 없다.
><br>빌더는 필드의 초기화 작업을 도와주는 역할이기 때문에.
><br>또한, @Builder 사용 시, 생성한 생성자가 없다면 @AllArgsConstructor(access=AccessLevel.PACKAGE)가 암묵적으로 적용 된다.
><br>Lombok 공식사이트 - @Builder 설명 중

### @Builder 필수 값 적용
```java
@Builder(builderMethodName = "TestBuilder")
public class Test {
    private String name;

    private int age;

    public static TestBuilder builder(String name) {
        return TestBuilder().namn(name);
    }

    public void main(String[] args) {
        Test test = Test.builder("tester") // 필수 인자가 없으면 생성 되지 않음
            .age(20)
            .build();
    }
}
```