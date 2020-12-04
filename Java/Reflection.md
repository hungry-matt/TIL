## Reflection
자바의 리플렉션은 클래스, 인터페이스, 메소드들을 찾거나 객체를 생성하고 변수를 변경하며 메소드를 호출할 수도 있습니다.

### Class 호출
- 클래스 Class 객체는 클래스 또는 인터페이스를 가리킨다.
- java.lang.Class 이며 import 하지 않고 사용 가능하다. 
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
메소드 | 기능
---|---
getDeclaredConstructors() | 클래스의 private, public 등의 모든 생성자를 리턴
getConstructor() | public 생성자만 리턴

### Method 찾기
```java
Class clazz = Class.forName("test.class")
Method method1 = clazz.getDeclaredMethod("method4", int.class) //(메소드명, 타입)
//public int test.class.method4(int)
```
> 함수명에 Declared 가 들어가면 super 클래스의 정보를 가져오지 않는다.

인자가 없을시 null 전달하며 두개 이상이라면 아래처럼 클래스 배열을 만든다.
```java
Class clazz = Class.forName("test.class");
Class partypes[] = new Class[1];
partypes[0] = int.class;
Method mehtod = clazz.getDeclaredMethod("method4", partypes);
```

메소드 | 기능
---|---
getDeclareMethods() | 모든 메소드의 정보를 리턴
getMethods() | public 메소드와 상속받은 메소드를 리턴

### Field 찾기
```java
Class clazz = Class.forName("test.class");
Field field = clazz.getDeclaredField("str1"); //public java.lang.String test.class.str1
```
메소드 | 기능
---|---
getDeclaredFields() | 객체에 선언된 모든 Field를 리턴
getFields() | public Field를 리턴

### Method 호출
클래스로부터 메소드 정보를 가져와, 객체의 메소드를 호출할 수 있다.

### 참고
- [Reflection 예제](https://codechacha.com/ko/reflection/)