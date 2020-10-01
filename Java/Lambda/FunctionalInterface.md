# FunctionalInterface
FunctionalInterface는 일반적으로 '구현해야 할 추상 메소드가 하나만 정의된 인터페이스'를 가르킨다.

```
A functional interface is an interface that has just one abstract method (aside from the methods of Object), and thus represents a single function contract.

Functional Interface는 (Object 클래스의 메소드를 제외하고) 단 하나의 추상 메소드만을 가진 인터페이스를 의미하며, 그런 이유로 단 하나의 기능적 계약을 표상하게 된다.
```

위 내용과 같이 'Object 클래스의 메소드를 제외하고'는 자바에서 사용되는 모든 객체들이 Object 객체를 상속하고 있다는 것을 기억하면 쉽게 이해할 수 있다.

결과적으로 인터페이스 구현체들이 Object 객체의 메소드를 재정의 하지 않아도 사용할 수 있으므로, Functional Interface의 대상이 되지 않는다.

```java
public interface NotFunctional {
    public boolean equals(Object obj);
}

public interface NotFunctional {
    public String toString();
    public void sum(int x, int y);
}

public interface Functional {
    public String toString();
}
```

### FunctionalInterface Annotation
Java SDK 8에서는 @FunctionalInterface 라고 하는 Annotation을 제공하여 작성한 인터페이스가 Functinal Interface 인지 확인할 수 있도록 하고 있다.

```java
@FuncationalInterface
public interface Functional {
    public void StringConcat(String str1, String str2);
}
```
