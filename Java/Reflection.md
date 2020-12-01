## Reflection
자바의 리플렉션은 클래스, 인터페이스, 메소드들을 찾거나 객체를 생성하고 변수를 변경하며 메소드를 호출할 수도 있습니다.

### Class 호출
````java
Class clazz = Date.class;
System.out.println(clazz.getName()); //java.util.Date 
````

```java
Class clazz = Class.forName("java.util.Date");
System.out.println(clazz.getName()); //java.util.Date
```

### Contructor 호출
```java
Constructor constructor = clazz.getDeclaredConstructor(); //default 생성자 호출
Constructor constructor2 = clazz.getDeclaredConstructor(Date.class); //인자를 넣으면 그 타입과 일치하는 생성자를 찾음

System.out.println(constructor.getName()); //java.util.Date
```

### 참고
- [Reflection 예제](https://codechacha.com/ko/reflection/)