# Stream
- 파일 I/O에서 사용되는 스트림과 다르다.
- Stream은 데이터를 추상화하고, 데이터 연산에 자주 사용하는 메서드를 정의해 놓았다.
- 데이터를 추상화 한다는것은, 데이터가 무엇이든 같은 방식으로 연산하여 코드의 재사용성을 높아진다는 것을 의미 한다.

## Stream의 특징

- Stream은 데이터 소스를 변경하지 않는다.
스트림은 데이터로 부터 데이터를 읽기만할 뿐, 데이터를 변경하지 않는다.필요하다면, 결과를 컬렉션이나 배열에 담아서 반환 한다.

```java
List<String> sortList = listStream.stream().sorted().collect(Collections.toList());
```

- Stream은 일회용이다.
Stream은 Iterator처럼 일회용이다. Iterator로 컬렉션의 요소를 읽고 나면 다시 사용 할 수 없는 것처럼, Stream도 한번 사용하면 닫혀서 다시 사용할 수 없다. 필요하다면 다시 Stream 생성.
