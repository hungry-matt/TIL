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