# 직렬화란 ?
자바에서 입출력을 할 때 `스트림` 이라는 통로를 통해 데이터가 이동합니다. 하지만 `객체`는 바이트형이 아니라서 스트림을 통해 파일에 저장하거나 네트워크로 전송할 수 없습니다.

따라서 객체를 스트림을 통해 입출력하려면 `바이트 배열로 변환` 하는 것이 필요한데, 이를 `직렬화` 라고 합니다. 반대로 스트림을 통해 받은 직렬화된 객체를 원래 모양으로 만드는 과정을 `역직렬화` 라고 합니다.

# 박싱과 언박싱이란?
기본 자료형(Primitive data type)을 Wrapper class 로 바꾸어 주는 것을 `박싱`, Wrapper class 를 기본 자료형(Primitive data type)으로 바꿔주는 것을 `언박싱` 이라고 합니다.

# HashMap vs HashTable vs ConcurrentHashMap
- HashMap
    - 주요 메서드에 `synchronized 키워드`가 `없습니다`.
    - key, value에 null을 입력할 수 있습니다.
    
- HashTable
    - 주요 메서드에 `synchronized 키워드`가 선언되어 `있습니다.`
    - key, value에 null을 허용하지 않습니다.

- ConcurrentHashMap
    - HashMap을 thread-safe 하도록 만든 클래스
    - key, value에 null을 허용하지 않습니다.
    
# 접근 제어자
- public : 어디서든 접근이 가능합니다.
- protected : 동일 패키지 혹은 상속받은 외부 패키지 클래스에서 사용 가능합니다.
- (default) : 동일 패키지 내에서만 접근 가능합니다.
- private : 해당 클래스 내에서만 접근 가능합니다.

# interface vs abstract
- inteface
    - 다중 상속
    - 추상 메서드, 상수만 선언 가능
    - 생성자, 일반 변수를 가질수 없음
- abstract
    - 다중 상속 불가
    - 추상 메서드 1개 이상, 일반 변수, 일반 메서드 선언 가능
    - 생성자, 일반 변수 가질 수 있음
    - 메서드의 부분 구현이 가능
    
# String vs StringBuffer vs StringBuilder
- String
    - immutable(불변)
    - 객체를 한 번 할당시 메모리 공간에 변동이 없다. (할당시 Heap String Pool 영역에 생성되어 그 값을 계속 사용한다.)
    - 동기화를 신경쓰지 않아도 된다.
    - 엄청나게 많은 문자열을 선언 및 연산시 성능 저하를 고려해야 한다.
- StringBuffer
    - mutable(가변)
    - 각 메서드별로 Synchronized Keyword가 존재 한다.
    - 멀티 스레드 환경에서도 동기화를 지원 한다. (thread-safe)
- StringBuilder
    - mutable(가변)
    - 동기화를 지원하지 않는다.

# try-with-resources ?
- try-with-resources는 `자동으로 자원을 해제` 해주는 기능이다.
- try에서 선언된 객체가 AutoCloseable을 구현했다면 Java는 try구문이 종료될 때 객체의 close() 메서드를 호출한다.

# Synchronized ?
- 여러 개의 스레드가 하나의 자원에 접근하려 할 때 단 `하나의 스레드`만 접근 가능하도록 하는 것이다.
- 공동의 자원을 다른 스레드가 동시에 수정하게 되면 심각한 문제가 발생할 수 있다.

# Synchronized를 하기 위한 방법
- synchronized 함수를 만들어 사용한다.
```java
synchrozined public void set() {
    ...
}
```

- synchronized 블록을 사용한다.
```java
public void set() {
    synchronized (this) {
        ...
    }
}
```

# 자바의 메모리 영역
- 메서드 영역
    - 자바 프로그램에서 사용되는 `Class 정보`, `클래스 변수(static variable)`가 `저장되는 영역`이다.
    - JVM은 특정 클래스가 사용되면 해당 클래스의 `클래스 파일(*.class)를 읽어들여`, 해당 클래스에 대한 정보를 `메소드 영역에 저장`한다.
- 힙(Heap)
    - 자바 프로그램에서 `사용되는 모든 인스턴스 변수`가 `저장되는 영역`이다.
    - JVM은 new 키워드를 사용하여 `인스턴스가 생성되면`, 해당 인스턴스의 정보를 `힙 영역에 저장`한다.
    - 가비지 컬렉션에 의해 메모리가 관리된다.
- 스택(Stack)
    - 메서드가 호출될 때 메서드의 스택 프레임이 저장되는 영역이다.
    - 스택 영역에 저장되는 메서드의 호출 정보를 스택 프레임이라 한다.
    - JVM은 `메서드가 호출 되면`, 메서드의 호출과 관련되는 `지역변수, 매개변수`를 `스택 영역에 저장`한다.
    - 스택 영역은 `메서드의 호출`과 함께 할당되며 메서드 `호출이 완료되면 소멸한다`.
    - 스택은 후입선출(LIFO, Last-In First-Out) 방식에 따라 동작하므로, 가장 늦게 저장된 데이터가 가장 먼저 인출 된다.

<img src="https://user-images.githubusercontent.com/45548349/113164917-83d05280-927c-11eb-9240-ffa679953a72.jpg" width="400" height="400">

# 컬렉션 프레임워크란?
- `다수의 데이터`를 쉽고 효과적으로 처리할 수 있는 표준화된 방법을 제공하는 `클래스의 집합`을 의미한다.
- 컬렉션 프레임워크에서는 데이터를 저장하는 자료 구조에 따라 다음과 같은 핵심이 되는 주요 인터페이스를 정의하고 있다.

1. List Interface
2. Set Interface
3. Map Interface

이 중에서 `List와 Set` 인터페이스는 모두 Collection 인터페이스를 상속 받지만, 구조상의 차이로 인해 `Map` 인터페이스는 별도로 정의 한다.

따라서 List 인터페이스와 Set 인터페이스의 공통된 부분을 Collection 인터페이스에서 정의하고 있다.

인터페이스 | 설명 | 구현 클래스
---|---|---
List | 순서가 있는 데이터의 집합. 데이터의 중복을 허용. | Vector, ArrayList, LinkedList, Stack, Queue
Set | 순서가 없는 데이터의 집합. 데이터의 중복을 허용하지 않음. | HashSet, TreeSet
Map<K, V> | 키와 값의 쌍으로 이루어지는 데이터의 집합. 순서가 없음. 키는 중복을 허용하지 않지만, 값은 중복 허용. | HashMap, TreeMap, HashTable, Properties